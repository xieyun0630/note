## zookeeper应用场景与安装 [	](zookeeper_20201124103028937)
### zookeeper应用场景 [	](zookeeper_20201124103028939)

+ 维护配置信息
+ 分布式锁服务
+ 集群管理
+ 生成分布式唯一ID

### zookeeper的linux安装 [	](zookeeper_20201124103028941)
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

## zookeeper常用Shell命令 [	](zookeeper_20201124103028944)

### 查看节点属性/状态命令 [	](zookeeper_20201124103028946)
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

### 新增节点命令 [	](zookeeper_20201124103028949)

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

### 更新节点命令 [	](zookeeper_20201124103028951)
+ 语法： {{c1:: `set path data [version]` }}
+ 例：
  1. 不指定版本号：{{c1:: `set /hadoop "345"` }}
  2. 指定版本号：{{c1:: `set /hadoop "3456" 1` }}
  + 注意：{{c1:: 每修改成功一次版本号会加1 }}

### 删除节点命令 [	](zookeeper_20201124103028955)

+ 删除语法： {{c1:: `delete path [version]` }}
+ 删除某个节点及其所有后代节点:`rmr path`

### 查看节点列表命令 [	](zookeeper_20201124103028957)
+ 语法：{{c1:: `ls path 和 ls2 path` }}
+ 解释：{{c1:: 后者是前者的增强，不仅可以查看指定路径下的所有节点，还可以查看当前节点的信息 }}

### 监听器命令 [	](zookeeper_20201124103028959)
+ `get path [watch]`: {{c1:: 使用 get path [watch] 注册的监听器能够在节点内容发生改变的时候，向客户端发出通知。 }}
+ `stat path [watch]`:{{c1:: 使用 stat path [watch] 注册的监听器能够在节点状态发生改变的时候，向客户端发出通知 }}
+ `ls\ls2 path [watch]`:{{c1:: 使用 ls path [watch] 或 ls2 path [watch] 注册的监听器能够监听该节点下所有子节点的增加和删除操作。 }}
+ 注意：在zookeeper中，一个监听器的注册只能使用一次

### zookeeper的acl权限控制命令 [	](zookeeper_20201124103028961)

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

### 授权的相关命令命令 [	](zookeeper_20201124103028963)
| 权限    | ACL简写 | 描述         |
| :------ | :------ | :----------- |
| `getAcl`  | `getAcl path`  | {{c1:: 读取ACL权限 }} |
| `setAcl`  | `setAcl path acl` | {{c1:: 设置ACL权限 }} |
| `addauth` | `addauth scheme auth` | {{c1:: 添加认证用户}} |

### acl权限控制案例： [	](zookeeper_20201124103028967)
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
+ 多种模式授权：{{c1:: `setAcl /node5 ip:192.168.60.129:cdra,auth:itcast:cdrwa,digest:itheima:qlzQzCLKhBROghkooLvb+Mlwv4A=:cdrwa` }}

### acl 超级管理员配置命令 [	](zookeeper_20201124103028970)
1. 那么打开zookeeper目录下的/bin/zkServer.sh服务器脚本文件，找到如下一行：
  + `nohup $JAVA "-Dzookeeper.log.dir=${ZOO_LOG_DIR}" "-Dzookeeper.root.logger=${ZOO_LOG4J_PROP}"`
2. 需要加一个超管的配置项:
  + `"-Dzookeeper.DigestAuthenticationProvider.uperDigest=super:xQJmxLMiHGwaqBvst5y6rkB6HQs="`
  + 注意这里密码是md5加密后密码，可以自定义
+ 之后启动zookeeper,输入如下命令添加权限:`addauth digest super:admin`
+ 理解：{{c1::标签}}

## zookeeper JavaAPI [	](zookeeper_20201124103028973)

### JavaAPI:连接zookeeper [	](zookeeper_20201124103028976)

```Java
//{{c1::
// 计数器对象
CountDownLatch countDownLatch=new CountDownLatch(1);
// arg1:服务器的ip和端口
// arg2:客户端与服务器之间的会话超时时间  以毫秒为单位的
// arg3:监视器对象
ZooKeeper zooKeeper=new ZooKeeper("192.168.60.130:2181,192.168.60.130:2182,192.168.60.130:2183", 5000, new Watcher() {
  @Override
  public void process(WatchedEvent event) {
    if(event.getState()==Event.KeeperState.SyncConnected) {
      System.out.println("连接创建成功!");
      countDownLatch.countDown();
    }
  }
});
// 主线程阻塞等待连接对象的创建成功
countDownLatch.await();
// 会话编号
System.out.println(zooKeeper.getSessionId());
zooKeeper.close();
//}}
```

### JavaAPI:新增节点 [	](zookeeper_20201124103028978)

+ world授权模式
  ```Java
  //{{c1::
  //world:anyone:cdrwa
  zooKeeper.create("/create/node1","node1".getBytes(), ZooDefs.Ids.OPEN_ACL_UNSAFE, CreateMode.PERSISTENT);

  //world:anyone:r
  zooKeeper.create("/create/node2", "node2".getBytes(), ZooDefs.Ids.READ_ACL_UNSAFE, CreateMode.PERSISTENT);

  // world:anyone:rw
  // 权限列表
  List<ACL> acls = new ArrayList<ACL>();
  // 授权模式和授权对象
  Id id = new Id("world", "anyone");
  // 权限设置
  acls.add(new ACL(ZooDefs.Perms.READ, id));
  acls.add(new ACL(ZooDefs.Perms.WRITE, id));
  zooKeeper.create("/create/node3", "node3".getBytes(), acls, CreateMode.PERSISTENT);
  //}}
  ```
+ IP授权模式
  ```Java
  //{{c1::
  List<ACL> acls = new ArrayList<ACL>();
  // 授权模式和授权对象
  Id id = new Id("ip", "192.168.60.130");
  // 权限设置
  acls.add(new ACL(ZooDefs.Perms.ALL, id));
  zooKeeper.create("/create/node4", "node4".getBytes(), acls, CreateMode.PERSISTENT);
  //}}
  ```
+ Auth授权模式
  ```Java
  //{{c1::
  // auth授权模式
  // 添加授权用户
  zooKeeper.addAuthInfo("digest", "itcast:123456".getBytes());
  // 权限列表
  List<ACL> acls = new ArrayList<ACL>();
  // 授权模式和授权对象
  Id id = new Id("auth", "itcast");
  // 权限设置
  acls.add(new ACL(ZooDefs.Perms.READ, id));
  zooKeeper.create("/create/node6", "node6".getBytes(), acls, CreateMode.PERSISTENT);
  //}}
  ```
+ Digest授权模式
  ```Java
  //{{c1::
  // digest授权模式
  // 权限列表
  List<ACL> acls = new ArrayList<ACL>();
  // 授权模式和授权对象
  Id id = new Id("digest", "itheima:qlzQzCLKhBROghkooLvb+Mlwv4A=");
  // 权限设置
  acls.add(new ACL(ZooDefs.Perms.ALL, id));
  zooKeeper.create("/create/node7", "node7".getBytes(), acls, CreateMode.PERSISTENT);
  //}}
  ```
+ 持久化顺序节点：{{c1:: `zooKeeper.create("/create/node8", "node8".getBytes(), ZooDefs.Ids.OPEN_ACL_UNSAFE, CreateMode.PERSISTENT_SEQUENTIAL);` }}
+ 临时节点:{{c1:: `zooKeeper.create("/create/node9", "node9".getBytes(), ZooDefs.Ids.OPEN_ACL_UNSAFE, CreateMode.EPHEMERAL);` }}
+ 临时顺序节点:{{c1:: `zooKeeper.create("/create/node10", "node10".getBytes(), ZooDefs.Ids.OPEN_ACL_UNSAFE, CreateMode.EPHEMERAL_SEQUENTIAL);` }}
+ 异步方式创建节点:
  ```Java
  //{{c1::
  zooKeeper.create("/create/node11", "node11".getBytes(), ZooDefs.Ids.OPEN_ACL_UNSAFE, CreateMode.PERSISTENT, new AsyncCallback.StringCallback() {
    @Override
    public void processResult(int rc, String path, Object ctx, String name) {
        // 0 代表创建成功
        System.out.println(rc);
        // 节点的路径
        System.out.println(path);
        // 节点的路径
        System.out.println(name);
        // 上下文参数
        System.out.println(ctx);

    }
  }, "I am context");
  Thread.sleep(10000);
  System.out.println("结束");
  //}}
  ```
### JavaAPI:更新/删除节点 [	](zookeeper_20201124103028980)
+ 更新节点
  + 同步方式：{{c1:: `setData(String path, byte[] data, int version)` }}
  + 异步方式：{{c1:: `setData(String path, byte[] data, int version,AsyncCallback.StatCallback callBack,Object ctx)` }}
+ 删除节点
  + 同步方式:{{c1:: `delete(String path, int version)` }}
  + 异步方式:{{c1:: `delete(String path, int version, AsyncCallback.VoidCallback callBack,Object ctx)` }}
+ 参数：
  + `path`： {{c1:: znode路径 }}
  + `data`： {{c1:: 要存储在指定znode路径中的数据。 }}
  + `version`： {{c1:: -1表示版本号不参与更新，znode的当前版本。每当数据更改时，ZooKeeper会更新znode的版本号。 }}
  + `callBack`：{{c1:: 异步回调接口 }}
  + `ctx`：{{c1:: 传递上下文参数 }}
+ 例：
  ```Java
  //{{c1::
  Stat stat=zookeeper.setData("/set/node1","node13".getBytes(),2);
  // 节点的版本号
  System.out.println(stat.getVersion());
  // 节点的创建时间
  System.out.println(stat.getCtime());
  //异步方式删除
  zooKeeper.setData("/set/node1", "node14".getBytes(), -1, new AsyncCallback.StatCallback() {
      @Override
      public void processResult(int rc, String path, Object ctx, Stat stat) {
          // 0代表修改成功
          System.out.println(rc);
          // 节点的路径
          System.out.println(path);
          // 上下文参数对象
          System.out.println(ctx);
          // 属性描述对象
          System.out.println(stat.getVersion());
      }
  }, "I am Context");
  Thread.sleep(10000);
  System.out.println("结束");
  //}}
  ```

### JavaAPI:查看节点 [	](zookeeper_20201124103028983)
+ 查看节点
  + 同步方式：{{c1:: `getData(String path, boolean b, Stat stat)` }}
  + 异步方式：{{c1:: `getData(String path, boolean b，AsyncCallback.DataCallback callBack，Object ctx)` }}
+ 查看子节点
  + 同步方式: {{c1:: `getChildren(String path, boolean b)` }}
  + 异步方式: {{c1:: `getChildren(String path, boolean b,AsyncCallback.ChildrenCallback callBack,Object ctx)` }}
+ 检查节点是否存在
  + 同步方式: {{c1:: `exists(String path, boolean b)` }}
  + 异步方式: {{c1:: `exists(String path, boolean b，AsyncCallback.StatCallback callBack,Object ctx)` }}
+ 参数:
  + `b`:{{c1:: 是否使用连接对象中注册的监视器。 }}



### watcher接口

+ 作用：{{c1:: 任何实现了`Watcher`接口的类就是一个新的`Watcher`。`Watcher`内部包含了两个枚举类：`KeeperState`、`EventType` }}
+ `KeeperState`各枚举值含义：
  1. `SyncConnected`: {{c1:: 客户端与服务器正常连接时 }}
  2. `Disconnected`: {{c1:: 客户端与服务器断开连接时 }}
  3. `Expired`: {{c1:: 会话session失效时 }}
  4. `AuthFailed`: {{c1:: 身份认证失败时 }}
+ `EventType`各枚举值含义：
  1. `None`：{{c1:: 无 }}
  2. `NodeCreated`：{{c1:: Watcher监听的数据节点被创建时 }}
  3. `NodeDeleted`：{{c1:: Watcher监听的数据节点被删除时 }}
  4. `NoNodeDataChangedne`：{{c1:: Watcher监听的数据节点内容发生变更时(无论内容数据是否变化) }}
  5. `NodeChildrenChanged`：{{c1:: Watcher监听的数据节点的子节点列表发生变更时 }}
+ 类结构图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201124171834.png) }}

### watcher特性

1. **一次性**:{{c1:: watcher是一次性的，一旦被触发就会移除，再次使用时需要重新注册 }}
2. **客户端顺序回调**:{{c1:: watcher回调是顺序串行化执行的，只有回调后客户端才能看到最新的数据状态。一个watcher回调逻辑不应该太多，以免影响别的watcher执行 }}
3. **轻量级**:{{c1:: WatchEvent是最小的通信单元，结构上只包含通知状态、事件类型和节点路径，并不会告诉数据节点变化前后的具体内容； }}
4. **时效性**:{{c1:: watcher只有在当前session彻底失效时才会无效，若在session有效期内快速重连成功，则watcher依然存在，仍可接收到通知； }}

### 注册watcher的方法以及可监听事件

+ `new ZooKeeper("192.168.60.130:2181", 5000, new Watcher());`：{{c1:: None }}
+ `zooKeeper.exists(String path, Watcher w)`：{{c1:: `Created` `Changed` `Deleted` }}
+ `zooKeeper.getData(String path, Watcher w, Stat stat)`：{{c1:: `Changed` `Deleted` }}
+ `zooKeeper.getChildren(String path, Watcher w)`：{{c1:: `Created`
`Deleted` }}

