### 开启镜像代理
+ 确认RabbitMQ运行与启动：`rabbitmqctl status`
+ 停掉服务： `service rabbitmq-server stop`
+ 启动第一节点：`RABBITMQ_NODE_PORT=5673 RABBITMQ_NODENAME=rabbit1 rabbitmq-server start`
  + 注意：这是前台启动方式
+ `RABBITMQ_NODE_PORT=5674 RABBITMQ_SERVER_START_ARGS="-rabbitmq_management listener [{port,15674}]" RABBITMQ_NODENAME=rabbit2 rabbitmq-server start`
  + 注意:与前一条命令的区别，管理控制台端口，与服务端口的不同
+ 分别访问已开启2个端口的控制台。
+ rabbit1操作作为主节点：
  + `rabbitmqctl -n rabbit1 stop_app  `
  + `rabbitmqctl -n rabbit1 reset`
  + `rabbitmqctl -n rabbit1 start_app`
+ rabbit2操作为从节点：
  + `rabbitmqctl -n rabbit2 stop_app`
  + `rabbitmqctl -n rabbit2 reset`
  + `rabbitmqctl -n rabbit2 join_cluster rabbit1@'super' `
    + 注意：super是**主机名**需要换成自己的
  + `rabbitmqctl -n rabbdddit2 start_app`
+ 此时存在问题：数据是无法同步的。
+ 开启主节点网页的管理端`Admin->Policies`配置如下
  + ![1566072300852](https://gitee.com/xieyun714/nodeimage/raw/master/img/1566072300852.png)
  + 等价的命令配置：`rabbitmqctl set_policy my_ha "^" '{"ha-mode":"all"}'`
+ 理解：{{c1:: 标签 }}

### 负载均衡-HAProxy插件配置
+ 作用：{{c1:: 提供统一的端口访问各个RabbitMQ节点 }}
+ 下载依赖包:`yum install gcc vim wget`
+ 上传haproxy源码包
+ 解压：`tar -zxvf haproxy-1.6.5.tar.gz -C /usr/local`
+ 进入目录、进行编译、安装：
  + `cd /usr/local/haproxy-1.6.5`
  + `make TARGET=linux31 PREFIX=/usr/local/haproxy`
  + `make install PREFIX=/usr/local/haproxy`
+ 赋权
  + `groupadd -r -g 149 haproxy`
  + `useradd -g haproxy -r -s /sbin/nologin -u 149 haproxy`
+ 创建haproxy配置文件
  + `mkdir /etc/haproxy`
  + `vim /etc/haproxy/haproxy.cfg`
+ 配置HAProxy：
  + 主要思路:
    1. 修改rabbitmq_cluster下，绑定**对外端口号**
    2. 修改balance roundrobin下，配置**节点通信**
    3. 修改listen stats下，配置HA管理控制台端口：
  + 配置如下：
  ```yaml
  #logging options
  global
    log 127.0.0.1 local0 info
    maxconn 5120
    chroot /usr/local/haproxy
    uid 99
    gid 99
    daemon
    quiet
    nbproc 20
    pidfile /var/run/haproxy.pid

  defaults
    log global
    
    mode tcp

    option tcplog
    option dontlognull
    retries 3
    option redispatch
    maxconn 2000
    contimeout 5s
    
      clitimeout 60s

      srvtimeout 15s  
  #front-end IP for consumers and producters

  listen rabbitmq_cluster
    bind 0.0.0.0:5672
    
    mode tcp
    #balance url_param userid
    #balance url_param session_id check_post 64
    #balance hdr(User-Agent)
    #balance hdr(host)
    #balance hdr(Host) use_domain_only
    #balance rdp-cookie
    #balance leastconn
    #balance source //ip
    
    balance roundrobin
    
          server node1 127.0.0.1:5673 check inter 5000 rise 2 fall 2
          server node2 127.0.0.1:5674 check inter 5000 rise 2 fall 2

  listen stats
    bind 172.16.98.133:8100
    mode http
    option httplog
    stats enable
    stats uri /rabbitmq-stats
    stats refresh 5s
  ```
+ 指定配置文件路径启动HAproxy负载：`/usr/local/haproxy/sbin/haproxy -f /etc/haproxy/haproxy.cfg`\
+ 查看haproxy进程状态:`ps -ef | grep haproxy`
+ 访问如下地址对mq节点进行监控:`http://172.16.98.133:8100/rabbitmq-stats`
+ 理解：{{c1:: 标签 }}