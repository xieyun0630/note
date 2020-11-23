### zookeeper应用场景
+ 维护配置信息
+ 分布式锁服务
+ 集群管理
+ 生成分布式唯一IDd

### zookeeper的linux安装
1. 用root用户创建zookeeper用户
   1. `useradd zookeeper`
   2. `passwd zookeeper`
2. 解压zookeeper:`tar -xzvf zookeeper-3.4.10.tar.gz`
3. 为zookeeper准备配置文件
  ```shell
  // 进入conf目录
  cd /home/zookeeper/zookeeper-3.4.10/conf
  // 复制配置文件
  cp zoo_sample.cfg zoo.cfg
  // zookeeper根目录下新建data目录
  mkdir data
  // vi 修改配置文件中的dataDir
  // 此路径用于存储zookeeper中数据的内存快照、及事物日志文件
  dataDir=/home/zookeeper/zookeeper-3.4.10/data
  ```
4. 启动zookeeper
   1. 进入zookeeper的bin目录:{{c1:: `cd /home/zookeeper/zookeeper-3.4.10/bin`}}
   2. 启动：{{c1:: `zkServer.sh start` }}
   3. 停止：{{c1:: `zkServer.sh stop` }}
   4. 查看状态：{{c1:: `zkServer.sh status` }}
+ 理解：{{c1:: 标签 }}

### 查看节点属性/状态
+ `get path`： {{c1::在zookeeper shell中使用get命令查看指定路径节点的data、stat信息 }}
+ `stat path`:{{c1:: 它的返回值和 get 命令类似，但不会返回
节点数据 }}
+ 属性说明： 
  + `cZxid`： {{c1:: 数据节点创建时的事务 ID }}
  + `ctime`： {{c1:: 数据节点创建时的时间 }}
  + `mZxid`： {{c1:: 数据节点最后一次更新时的事务 ID }}
  + `mtime`： {{c1:: 数据节点最后一次更新时的时间 }}
  + `pZxid`： {{c1:: 数据节点的子节点最后一次被修改时的事务 ID }}
  + `cversion`： {{c1:: 子节点的更改次数 }}
  + `dataVersion`： {{c1:: 节点数据的更改次数 }}
  + `aclVersion`： {{c1:: 节点的 ACL 的更改次数,用于权限控制 }}
  + `ephemeralOwner`： {{c1:: 如果节点是临时节点，则表示创建该节点的会话的SessionID；如果节点是持久节点，则该属性值为 0 }}
  + `dataLength`： {{c1:: 数据内容的长度（字节数） }}
  + `numChildren`： {{c1:: 数据节点当前的子节点个数 }}

### zookeeper常用Shell命令:新增节点

+ `create [-s] [-e] path data `
  + {{c1:: `-s`：为有序节点 }}
  + {{c1:: `-e`：临时节点 }}
+ 例：
  + 创建**持久化节点**并写入数据：`create /hadoop "123456"`
  + 创建**持久化有序节点**
  + 特点：zookeeper会自动添加序列名称
  1. `create -s /a "aaa"`
  2. `create -s /b "bbb"`
  3. `create -s /c "ccc"`
  + 创建**临时节点**：`create -e /tmp "tmp"`
  + 创建**临时有序**节点
  1. `create -s -e /aa "aaa"`
  2. `create -s -e /bb "bbb"`
  3. `create -s -e /cc "ccc"`

### zookeeper常用Shell命令:更新节点
+ 语法： {{c1:: `set path data [version]` }}
+ 例：
  1. 不指定版本号：{{c1:: `set /hadoop "345"` }}
  2. 指定版本号：{{c1:: `set /hadoop "3456" 1` }}
  + 注意：{{c1:: 每修改成功一次版本号会加1 }}

### zookeeper常用Shell命令:删除节点

+ 删除语法： {{c1:: `delete path [version]` }}
+ 删除某个节点及其所有后代节点:`rmr path`

### zookeeper常用Shell命令:查看节点列表
+ 语法：{{c1:: `ls path 和 ls2 path` }}
+ 解释：{{c1:: 后者是前者的增强，不仅可以查看指定路径下的所有节点，还可以查看当前节点的信息 }}

### 监听器
+ `get path [watch]`: {{c1:: 使用 get path [watch] 注册的监听器能够在节点内容发生改变的时候，向客户端发出通知。 }}
+ `stat path [watch]`:{{c1:: 使用 stat path [watch] 注册的监听器能够在节点状态发生改变的时候，向客户端发出通知 }}
+ `ls\ls2 path [watch]`:{{c1:: 使用 ls path [watch] 或 ls2 path [watch] 注册的监听器能够监听该节点下所有子节点的增加和删除操作。 }}
+ 注意：在zookeeper中，一个监听器的注册只能使用一次

### zookeeper的acl权限控制

+ 标识:`scheme：id：permission`
  + {{c1:: 权限模式（scheme）：授权的策略 }}
  + {{c1:: 授权对象（id）：授权的对象 }}
  + {{c1:: 权限（permission）：授予的权限 }}
+ 权限模式:
  + `world`:{{c1:: 只有一个用户：`anyone`，代表登录zokeeper所有人（默认） }}
  + `ip`:{{c1:: 对客户端使用IP地址认证 }}
  + `auth`:{{c1:: 使用已添加认证的用户认证 }}
  + `digest`:{{c1:: 使用“用户名:密码”方式认证 }}
+ 授权对象ID: {{c1:: 是指，权限赋予的实体，例如：IP 地址或用户。 }}
+ 授予的权限:
  | 权限     | ACL简写 | 描述                             |
  | :------- | :------ | :------------------------------- |
  | `create` | `c`     | {{c1:: 可以创建子节点                  }} |
  | `delete` | `d`     | {{c1:: 可以删除子节点（仅下一级节点）  }} |
  | `read`   | `r`     | {{c1:: 可以读取节点数据及显示子节点列表}} |
  | `write`  | `w`     | {{c1:: 可以设置节点数据                }} |
  | `admin`  | `a`     | {{c1:: 可以设置节点访问控制列表权限    }} |
+ 例：`setAcl /test2 ip:192.168.60.130:crwda`:{{c1:: 将节点权限设置为Ip:192.168.60.130的客户端可以对节点进行增、删、改、查、管理权限 }}

### 授权的相关命令
| 权限    | ACL简写 | 描述         |
| :------ | :------ | :----------- |
| `getAcl`  | `getAcl path`  | {{c1:: 读取ACL权限 }} |
| `setAcl`  | `setAcl path acl` | {{c1:: 设置ACL权限 }} |
| `addauth` | `addauth scheme auth` | {{c1:: 添加认证用户}} |

### acl权限控制案例：
+ world授权模式：{{c1:: `setAcl <path> world:anyone:<acl>` }}
  + 例：{{c1:: `setAcl /node1 world:anyone:cdrwa` }}
+ IP授权模式：{{c1:: `setAcl <path> ip:<ip>:<acl>` }}
  + 例：{{c1:: `setAcl /node2 ip:192.168.60.129:cdrwa` }}
  + 例：{{c1:: `setAcl /node2 ip:192.168.60.129:cdrwa,ip:192.168.60.130:cdrwa` }}
  + 注意：远程登录zookeeper命令:{{c1:: `./zkCli.sh -server ip` }}
+ Auth授权模式：
  + {{c1:: `addauth digest <user>:<password> #添加认证用户` }}
  + {{c1:: `setAcl <path> auth:<user>:<acl>` }}
  + 例：
    + {{c1:: `addauth digest itcast:123456` }}
    + {{c1:: `setAcl /node3 auth:itcast:cdrwa` }}
+ Digest授权模式：{{c1:: `setAcl <path> digest:<user>:<password>:<acl>` }}
  + 这里的密码是经过SHA1及BASE64处理的密文，在SHELL中可以通过以下命令计算：
  + `echo -n <user>:<password> | openssl dgst -binary -sha1 | openssl base64`
  + 例：
    1. {{c1:: `setAcl /node4 digest:itheima:qlzQzCLKhBROghkooLvb+Mlwv4A=:cdrwa`:使用密文授权 }}
    2. {{c1:: `addauth digest itheima:123456 `:使用明文登录 }}
    3. {{c1:: `get /node4`：正常获取权限 }}