### 正向代理与反向代理
+ 正向代理作用：{{c1:: 客户端必须通过代理服务器才能访问某种被限制的资源。 }}
+ 反向代理作用：{{c1:: 将请求发送到反向代理服务器，由反向代理服务器去选择目标服务器获取数据后，在返回给客户端，此时反向代理服务器和目标服务器对外就是一个服务器，暴露的是代理服务器地址，隐藏了真实服务器 IP 地址。 }}
+ 图示：
  + {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201123094212.png) }}
  + {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201123094224.png) }}

### Nginx 的常用的命令
+ 进入nginx目录中:{{c1:: `cd/usr/local/nginx/sbin` }}
+ 查看nginx版本号:{{c1:: `./nginx -v` }}
+ 启动nginx:{{c1:: `./nginx.` }}
+ 停止nginx:{{c1:: `./nginx -s stop` }}
+ 重新加载nginx:{{c1:: `./nginx -s reload` }}

### Nginx 的配置文件
+ 配置文件位置： `/etc/nginx/nginx.conf`
  + 注意：修改之后重启镜像
+ 文件结构如下
  + {{c1:: 全局块：配置服务器整体运行的配置指令  }}
    + {{c1:: 比如`worker_processes 1;`处理并发数的配置  }}
  + {{c1:: `events`块：影响 Nginx 服务器与用户的网络连接  }}
    + {{c1:: 比如`worker_connections 1024`; 支持的最大连接数为 `1024`  }}
  + {{c1:: `http`块  }}
    + {{c1:: `http`全局块  }}
    + {{c1:: `server`块  }}

### Nginx 配置实例-反向代理实例

+ 访问效果：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201123130916.png)
  + 具体配置：
    1. 添加内容在 host 文件中：{{c1::`81.69.43.171 www.123.com`}}
       1. 注意：需要访问tomcat，需port：{{c1::`www.123.com:8080/`}}
    2. 修改`nginx.conf`文件内容：
        + 如图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201123131633.png)}}
        + server_name:访问nginx的ip地址
        + location:{{c1::指定需要转发的路径}}
          + proxy_pass：{{c1::指定对应路径与端口}}
+ 访问效果：
  + 访问 http://192.168.17.129:9001/edu/ 直接跳转到 127.0.0.1:8080
  + 访问 http:// 192.168.17.129:9001/vod/ 直接跳转到 127.0.0.1:8081
  + 具体配置：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201123133348.png) }}

### Nginx 配置实例-负载均衡
+ 访问效果：浏览器地址栏输入地址 http://192.168.17.129/edu/a.html，负载均衡效果，平均 8080和 8081 端口中
+ 在 nginx 的配置文件中进行负载均衡的配置
  + ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201123133905.png)
  + upstream myserver:包含负载服务器列表，myserver是自定名字
+ nginx 分配服务器策略
  + `轮询`: {{c1:: 默认策略，每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器 down 掉，能自动剔除。 }}
  + `weight`: {{c1:: weight 代表权重默认为 1,权重越高被分配的客户端越多 }}
  + `ip_hash`: {{c1:: 每个请求按访问 ip 的 hash 结果分配，这样每个访客固定访问一个后端服务器,可以解决session问题 }}
  + `fair`: {{c1:: 按后端服务器的响应时间来分配请求，响应时间短的优先分配。 }}

### Nginx 配置实例-动静分离
+ 实现效果：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201123134958.png)
+ 具体配置：
+ 在 liunx 系统中准备静态资源，用于进行访问
  + `/data/image/`:{{c1:: 放置图片资源 }}
  + `/data/www/`:{{c1:: 放置静态资源 }}
+ 在 nginx 配置文件中进行配置
  + {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201123135600.png)}}
  + `root`：{{c1:: 指定资源地址的根路径 }}
  + `autoindex on`:{{c1:: 列出访问目录 }}
  + `expires 3d`:{{c1:: 如无变化，缓存3天 }}
    + 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201123140047.png) }}
  + 测试：`http://192.168.17.129/www/a.html`

### Nginx 配置高可用的集群
+ 实现效果：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201123140944.png)
+ 在两台服务器安装`keepalived`
  1. 注意：两台服务器是在同一局域网中
  2. `yum install keepalived -y`
  3. 安装之后，在 etc 里面生成目录 keepalived，有文件 keepalived.conf
1. 修改/etc/keepalived/keepalivec.conf 配置文件
  ```js
  global_defs {
    notification_email {
      acassen@firewall.loc
      failover@firewall.loc
      sysadmin@firewall.loc
    }
    notification_email_from Alexandre.Cassen@firewall.loc
    smtp_server 192.168.17.129
    smtp_connect_timeout 30
    router_id LVS_DEVEL #访问当前主机中hosts文件中的地址
  }
  vrrp_script chk_http_port {
    script "/usr/local/src/nginx_check.sh"
    interval 2 //（检测脚本执行的间隔）
    weight 2 //权重，脚本条件满足则设置当前服务器的权重
  }
  vrrp_instance VI_1 {
    state BACKUP // 备份服务器上将 MASTER 改为 BACKUP
    interface ens33 //网卡，linux下 ifconfig命令查看
    virtual_router_id 51 // 主、备机的 virtual_router_id 必须相同
    priority 90 // 主、备机取不同的优先级，主机值较大，备份机值较小
    advert_int 1 //检查主机是否还活着，每隔一秒检测一次
    authentication {
      auth_type PASS
      auth_pass 1111
    }
    virtual_ipaddress {
      192.168.17.50 // VRRP H 虚拟地址
    }
  }
  ```
2. 在/usr/local/src 添加检测脚本
  ```shell
  #!/bin/bash
  #!/bin/bash
  A=`ps -C nginx –no-header |wc -l`
  if [ $A -eq 0 ];then
    /usr/local/nginx/sbin/nginx
    sleep 2
    if [ `ps -C nginx --no-header |wc -l` -eq 0 ];then
      killall keepalived
    fi
  fi
   ```
3. 把两台服务器上 nginx 和 keepalived 启动
   + 启动 keepalived：`systemctl start keepalived.service`
 + 最终测试:在浏览器地址栏输入 虚拟 ip 地址 `192.168.17.50 `
+ 理解：{{c1::标签}}

## Nginx 的原理

### 一个 master 和多个 woker 有好处:
   1. {{c1:: 可以使用`nginx –s reload`热部署，利用nginx进行热部署操作 }}
   2. {{c1:: 每个`woker`是独立的进程，如果有其中的一个woker出现问题，其他woker独立的，继续进行争抢，实现请求过程，不会造成服务中断 }}
   3. 
### 设置多少个 woker 合适
+ {{c1:: worker数和服务器的cpu 数相等是最为适宜的 }}

### nginx 有一个 master，有四个 woker，每个 woker 支持最大的连接数 1024，支持的最大并发数是多少？
+ 普通的静态访问最大并发数是：{{c1:: `worker_connections * worker_processes /2` }}
+ 而如果是HTTP作为反向代理来说，最大并发数量应该是：{{c1:: `worker_connections *worker_processes/4` }}

