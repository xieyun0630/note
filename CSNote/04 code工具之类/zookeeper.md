## zookeeper应用场景与安装 [	](zookeeper_20201124103028937)
### zookeeper应用场景 [	](zookeeper_20201124103028939)

1. {{c1:: 维护配置信息 }}
2. {{c1:: 分布式锁服务 }}
3. {{c1:: 集群管理 }}
4. {{c1:: 生成分布式唯一ID }}

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
+ 删除某个节点及其所有后代节点: {{c1:: `rmr path` }}

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

### 授权的相关命令 [	](zookeeper_20201124103028963)
| 权限    | ACL简写 | 描述         |
| :------ | :------ | :----------- |
| `getAcl`  | `getAcl path`  | {{c1:: 读取ACL权限 }} |
| `setAcl`  | `setAcl path acl` | {{c1:: 设置ACL权限 }} |
| `addauth` | `addauth digest <user>:<password> ` | {{c1:: 添加认证用户}} |

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
  + 例：
    1. {{c1:: `setAcl /node4 digest:itheima:qlzQzCLKhBROghkooLvb+Mlwv4A=:cdrwa`:使用密文授权 }}
    2. {{c1:: `addauth digest itheima:123456 `:使用明文登录 }}
    3. {{c1:: `get /node4`：正常获取权限 }}
+ 多种模式授权：{{c1:: `setAcl /node5 ip:192.168.60.129:cdra,auth:itcast:cdrwa,digest:itheima:qlzQzCLKhBROghkooLvb+Mlwv4A=:cdrwa` }}

### zookeeper添加超级管理员 [	](zookeeper_20201124103028970)
1. 那么打开zookeeper目录下的/bin/zkServer.sh服务器脚本文件，找到如下一行：
  + `nohup $JAVA "-Dzookeeper.log.dir=${ZOO_LOG_DIR}" "-Dzookeeper.root.logger=${ZOO_LOG4J_PROP}"`
2. 需要加一个超管的配置项:
  + `"-Dzookeeper.DigestAuthenticationProvider.uperDigest=super:xQJmxLMiHGwaqBvst5y6rkB6HQs="`
  + 注意：这里是md5加密后密码，可以自定义
+ 之后启动zookeeper,输入如下命令添加权限:`addauth digest super:admin`
+ 理解：{{c1::标签}}

## zookeeper JavaAPI [	](zookeeper_20201124103028973)

### JavaAPI:连接zookeeper [	](zookeeper_20201124103028976)
```Java
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
```
+ 理解：{{c1:: 标签 }}

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
  + 同步方式： `getData(String path, boolean b, Stat stat)` 
  + 异步方式： `getData(String path, boolean b，AsyncCallback.DataCallback callBack，Object ctx)` 
+ 查看子节点
  + 同步方式:  `getChildren(String path, boolean b)` 
  + 异步方式:  `getChildren(String path, boolean b,AsyncCallback.ChildrenCallback callBack,Object ctx)` 
+ 检查节点是否存在
  + 同步方式:  `exists(String path, boolean b)` 
  + 异步方式:  `exists(String path, boolean b，AsyncCallback.StatCallback callBack,Object ctx)` 
+ 参数:
  + `b`:{{c1:: 是否使用连接对象中注册的监视器。 }}
+ 标签：{{c1:: 理解 }}


### watcher接口 [	](zookeeper_20201125093504164)

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
  4. `NodeDataChanged`：{{c1:: Watcher监听的数据节点内容发生变更时(无论内容数据是否变化) }}
  5. `NodeChildrenChanged`：{{c1:: Watcher监听的数据节点的子节点列表发生变更时 }}
+ 类结构图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201124171834.png) }}

### watcher特性 [	](zookeeper_20201125093504166)

1. **一次性**:{{c1:: watcher是一次性的，一旦被触发就会移除，再次使用时需要重新注册 }}
2. **客户端顺序回调**:{{c1:: watcher回调是顺序串行化执行的，只有回调后客户端才能看到最新的数据状态。一个watcher回调逻辑不应该太多，以免影响别的watcher执行 }}
3. **轻量级**:{{c1:: WatchEvent是最小的通信单元，结构上只包含通知状态、事件类型和节点路径，并不会告诉数据节点变化前后的具体内容； }}
4. **时效性**:{{c1:: watcher只有在当前session彻底失效时才会无效，若在session有效期内快速重连成功，则watcher依然存在，仍可接收到通知； }}

### 注册watcher的方法以及可监听事件 [	](zookeeper_20201125093504168)

+ `new ZooKeeper("192.168.60.130:2181", 5000, new Watcher());`：{{c1:: None }}
+ `zooKeeper.exists(String path, Watcher w)`：{{c1:: `Created` `Changed` `Deleted` }}
+ `zooKeeper.getData(String path, Watcher w, Stat stat)`：{{c1:: `Changed` `Deleted` }}
+ `zooKeeper.getChildren(String path, Watcher w)`：{{c1:: `Created`
`Deleted` }}
## zookeeper使用案例 [	](zookeeper_20201125093504172)

### 配置中心案例 [	](zookeeper_20201125093504175)

+ 工作中有这样的一个场景:数据库用户名和密码信息放在一个配置文件中，应用读取该配置文件.
+ `zookeeper`保存配置信息设计思路：
  1. {{c1:: 连接`zookeeper`服务器 }}
  2. {{c1:: 读取`zookeeper`中的配置信息，注册`watcher`监听器，存入本地变量 }}
  3. {{c1:: 当`zookeeper`中的配置信息发生变化时，通过`watcher`的回调方法捕获数据变化事件 }}
  4. {{c1:: 重新获取配置信息 }}

### 生成分布式唯一ID [	](zookeeper_20201125093504179)
+ 设计思路：
  1. {{c1:: 连接zookeeper服务器 }}
  2. {{c1:: 指定路径生成临时有序节点 }}
  3. {{c1:: 取序列号及为分布式环境下的唯一ID }}

### 分布式锁 [	](zookeeper_20201125093504181)
+ 设计思路：
  1. 每个客户端往`/Locks`下创建临时有序节点`/Locks/Lock_`,创建成功后`/Locks`下面会有每个客户端对应的节点，如`/Locks/Lock_000000001`
  2. 客户端取得`/Locks`下子节点，并进行排序，判断排在最前面的是否为自己，如果自己的锁节点在第一位，代表获取锁成功
  3. 如果自己的锁节点不在第一位，则监听自己前一位的锁节点。例如，自己锁节点`Lock_000000002`,那么则监听`Lock000000001`
  4. 当前一位锁节点（`Lock_000000001`)对应的客户端执行完成，释放了锁，将会触发监听客户端（`Lock_000000002`)的逻辑
  5. 监听客户端重新执行第2步逻辑，判断自己是否获得了锁
+ 主要代码：
  ```Java
      //ZooKeeper配置信息
    private static final String LOCK_ROOT_PATH = "/Locks";
    private static final String LOCK_NODE_NAME = "Lock_";
     //获取锁
    public void acquireLock() throws Exception {
        createLock();
        attemptLock();
    }

    //创建锁节点
    private void createLock() throws Exception {
        //判断Locks是否存在，不存在创建
        Stat stat = zooKeeper.exists(LOCK_ROOT_PATH, false);
        if (stat == null) {
            zooKeeper.create(LOCK_ROOT_PATH, new byte[0], ZooDefs.Ids.OPEN_ACL_UNSAFE, CreateMode.PERSISTENT);
        }
        // 创建临时有序节点
        lockPath = zooKeeper.create(LOCK_ROOT_PATH + "/" + LOCK_NODE_NAME, new byte[0], ZooDefs.Ids.OPEN_ACL_UNSAFE, CreateMode.EPHEMERAL_SEQUENTIAL);
        System.out.println("节点创建成功:" + lockPath);
    }

    //监视器对象，监视上一个节点是否被删除
    Watcher watcher = new Watcher() {
        @Override
        public void process(WatchedEvent event) {
            if (event.getType() == Event.EventType.NodeDeleted) {
                synchronized (this) {
                    notifyAll();
                }
            }
        }
    };

    //尝试获取锁
    private void attemptLock() throws Exception {
        // 获取Locks节点下的所有子节点
        List<String> list = zooKeeper.getChildren(LOCK_ROOT_PATH, false);
        // 对子节点进行排序
        Collections.sort(list);
        // /Locks/Lock_000000001
        int index = list.indexOf(lockPath.substring(LOCK_ROOT_PATH.length() + 1));
        if (index == 0) {
            System.out.println("获取锁成功!");
            return;
        } else {
            // 上一个节点的路径
            String path = list.get(index - 1);
            Stat stat = zooKeeper.exists(LOCK_ROOT_PATH + "/" + path, watcher);
            if (stat == null) {
                attemptLock();
            } else {
                synchronized (watcher) {
                    watcher.wait();
                }
                attemptLock();
            }
        }
    }

    //释放锁
    public void releaseLock() throws Exception {
            //删除临时有序节点
            zooKeeper.delete(this.lockPath,-1);
            zooKeeper.close();
            System.out.println("锁已经释放:"+this.lockPath);
    }
  ```
## zookeeper集群 [	](zookeeper_20201126080456391)
### zookeeper集群搭建 [	](zookeeper_20201126080456393)

+ 要求：单机环境下，jdk、zookeeper 安装完毕，进行zookeeper伪集群搭建，zookeeper集群中包含3个节点，节点对外提供服务端口号分别为`2181、2182、2183`
+ 基于`zookeeper-3.4.10`复制三份`zookeeper`安装好的服务器文件
  ```shell
    cp ‐r zookeeper‐3.4.10 zookeeper2181
    cp ‐r zookeeper‐3.4.10 zookeeper2182
    cp ‐r zookeeper‐3.4.10 zookeeper2183
  ```
+ 修改zookeeper服务器conf目录下对应配置文件：`zoo.cfg`
  ```properties
  #服务器对应端口号
  clientPort=2181
  #数据快照文件所在路径
  dataDir=/home/zookeeper/zookeeper2181/data
  #集群配置信息
  #server.A=B:C:D
  #A：是一个数字，表示这个是服务器的编号
  #B：是这个服务器的ip地址
  #C：Zookeeper服务器之间的通信端口
  #D：Leader选举的端口
  server.1=192.168.60.130:2287:3387
  server.2=192.168.60.130:2288:3388
  server.3=192.168.60.130:2289:3389
  ```
+ 在上一步`dataDir`指定的目录下，创建`myid`文件:
  ```shell
  #zookeeper2181对应的数字为1
  #/home/zookeeper/zookeeper2181/data目录下执行命令
  echo "1" > myid
  ```
+ 分别启动三台服务器，检验集群状态:
  ```
  ./zkCli.sh ‐server 192.168.60.130:2181
  ./zkCli.sh ‐server 192.168.60.130:2182
  ./zkCli.sh ‐server 192.168.60.130:2183
  ```
+ 理解：{{c1:: 标签 }}

### 一致性协议:zab协议 [	](zookeeper_20201126080456395)
+ 作用：{{c1:: 来保证分布式事务的最终一致性 }}
+ zab协议全称：{{c1:: `Zookeeper Atomic Broadcast`（zookeeper原子广播）。 }}
+ zookeeper集群中的角色主要有以下三类，如下表所示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201126160334.png) }}

### zab广播模式工作原理 [	](zookeeper_20201126080456397)
+ 如图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201126160510.png)
+ 工作流程：
  1. {{c1:: `leader`从客户端收到一个写请求 }}
  2. {{c1:: `leader`生成一个新的事务并为这个事务生成一个唯一的`ZXID` }}
  3. {{c1:: `leader`将这个事务提议(`propose`)发送给所有的`follows`节点 }}
  4. {{c1:: `follower`节点将收到的事务请求加入到历史队列(`history queue`)中,并发送ack给`leader` }}
  5. {{c1:: 当`leader`收到大多数`follower`（半数以上节点）的`ack`消息，`leader`会发送`commit`请求 }}
  6. {{c1:: 当`follower`收到`commit`请求时，从历史队列中将事务请求`commit` }}

## zookeeper集群的leader选举 [	](zookeeper_20201126080456401)
### zookeeper服务器4种状态 [	](zookeeper_20201126080456404)
+ `looking`：{{c1:: 寻找leader状态。当服务器处于该状态时，它会认为当前集群中没有leader，因此需要进入leader选举状态。 }}
+ `leading`：{{c1::  领导者状态。表明当前服务器角色是leader。 }}
+ `following`：{{c1::  跟随者状态。表明当前服务器角色是follower。 }}
+ `observing`：{{c1:: 观察者状态。表明当前服务器角色是observer。 }}
+ 查看状态命令：{{c1:: `zkServer.sh status` }}

### 集群leader选举 [	](zookeeper_20201126080456407)
+ 服务器启动时期的leader选举过程：
  1. {{c1:: 每个server发出一个投票。使用(myid, zxid)来表示， }}
  2. {{c1:: 集群中的每台服务器接收来自集群中各个服务器的投票。 }}
  3. {{c1:: 处理投票。pk规则如下 }}
     1. {{c1:: 优先检查zxid。zxid比较大的服务器优先作为leader。 }}
     2. {{c1:: 如果zxid相同，那么就比较myid。myid较大的服务器作为leader服务器。 }}
  4. {{c1:: 统计投票。 }}
  5. {{c1:: 改变服务器状态。 }}
+ 服务器运行时期的Leader选举过程:
  1. {{c1:: 变更状态。leader挂后，余下的服务器都会将自己的服务器状态变更为looking，然后开始进入leader选举过程。 }}
  2. {{c1:: 每个server会发出一个投票。}}
  3. {{c1:: 集群中的每台服务器接收来自集群中各个服务器的投票。在运行期间，每个服务器上的zxid可能不同 }}
  4. {{c1:: 处理投票。pk规则如下 }}
     1. {{c1:: 优先检查zxid。zxid比较大的服务器优先作为leader。 }}
     2. {{c1:: 如果zxid相同，那么就比较myid。myid较大的服务器作为leader服务器。 }}
  5. {{c1:: 统计投票。 }}
  6. {{c1:: 改变服务器状态。 }}

### observer角色及其配置 [	](zookeeper_20201126080456410)
+ observer角色特点：
  + {{c1:: 不参与集群的leader选举 }}
  + {{c1:: 不参与集群中写数据时的ack反馈 }}
+ 在任何想变成observer角色的配置文件中加入：
  ```properties
    peerType=observer #注意位置应该不同
    server.3=192.168.60.130:2289:3389:observer
  ```

### zookeeperAPI连接集群 [	](zookeeper_20201126080456412)

+ 思路：{{c1:: 在Zookeeper对象第一个参数中罗列出集群ip即可 }}
```java
// {{c1::
ZooKeeper zooKeeper=new
ZooKeeper("192.168.60.130:2181,192.168.60.130:2182,192.168.60.130:2183",
5000,null)
//}}
```

## zookeeper开源客户端curator [	](zookeeper_20201127124859778)

### curator的Maven依赖 [	](zookeeper_20201127124859780)
+ 主要artifactId：`curator-framework` `zookeeper` `curator-recipes`
```xml
    <dependency>
        <groupId>org.apache.curator</groupId>
        <artifactId>curator-framework</artifactId>
        <version>2.6.0</version>
        <type>jar</type>
        <exclusions>
            <exclusion>
                <groupId>org.apache.zookeeper</groupId>
                <artifactId>zookeeper</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.apache.zookeeper</groupId>
        <artifactId>zookeeper</artifactId>
        <version>3.4.10</version>
        <type>jar</type>
    </dependency>
    <dependency>
        <groupId>org.apache.curator</groupId>
        <artifactId>curator-recipes</artifactId>
        <version>2.6.0</version>
        <type>jar</type>
    </dependency>
```
+ 理解：{{c1:: 标签 }}
### curator连接到ZooKeeper [	](zookeeper_20201127124859782)
```java
  // 创建连接对象
  //{{c1::
  CuratorFramework client= CuratorFrameworkFactory.builder()
  //}}
          // IP地址端口号
          //{{c1::
          .connectString("192.168.60.130:2181,192.168.60.130:2182,192.168.60.130:2183")
          //}}
          // 会话超时时间
          //{{c1::
          .sessionTimeoutMs(5000)
          //}}
          // 重连机制
          //{{c1::
          .retryPolicy(retryPolicy)
          //}}
          // 命名空间
          //{{c1::
          .namespace("create")
          //}}
          // 构建连接对象
          //{{c1::
          .build();
          //}}
  // 打开连接
  //{{c1::
  client.start();
  System.out.println(client.isStarted());
  // 关闭连接
  client.close();
  //}}
```

### curator的session重连策略 [	](zookeeper_20201127124859784)
+ 3秒后重连一次，只重连1次:{{c1:: `RetryPolicy retryPolicy = new RetryOneTime(3000);` }}
+ 每3秒重连一次，重连3次:{{c1:: `RetryPolicy retryPolicy = new RetryNTimes(3,3000);` }}
+ 每3秒重连一次，总等待时间超过10秒后停止重连:{{c1:: `RetryPolicy retryPolicy=new RetryUntilElapsed(10000,3000);` }}

### curator新增zookeeper节点 [	](zookeeper_20201127124859785)
+ 新增节点:
  ```java
  //{{c1::
    client.create()
            // 节点的类型
            .withMode(CreateMode.PERSISTENT)
            // 节点的权限列表 world:anyone:cdrwa
            .withACL(ZooDefs.Ids.OPEN_ACL_UNSAFE)
            // arg1:节点的路径 arg2:节点的数据
            .forPath("/node1", "node1".getBytes());
  //}}
  ```
### curator的client.create()调用链常用方法解释： [	](zookeeper_20201127124859788)
+ `.creatingParentsIfNeeded()`:{{c1:: 递归创建节点树 }}
+ `.withMode(CreateMode.PERSISTENT)`:{{c1:: 指定节点的类型 }}
+ `.withACL(ZooDefs.Ids.OPEN_ACL_UNSAFE)`:{{c1:: 节点的权限列表 world:anyone:cdrwa }}
  + 可指定自定义权限列表：
    ```java
      //{{c1::
      List<ACL> list = new ArrayList<ACL>();
      Id id = new Id("ip", "192.168.60.130");
      list.add(new ACL(ZooDefs.Perms.ALL, id));
      //.withACL(list)
      //}}
    ```
+ 异步方式创建节点：`.inBackground((client,event)-> System.out.println(event.getPath()))`
+ 指定节点的路径，与节点数据:{{c1:: `.forPath("/node1", "node1".getBytes());` }}

### curator的client.setData()调用链： [	](zookeeper_20201127124859790)
+ 指定节点版本号：{{c1:: `.withVersion(2)`}}
+ 异步方式更新节点：{{c1:: `.inBackground((client,event)-> System.out.println(event.getPath()))`}}
+ 指定节点的路径，与节点数据:{{c1:: `.forPath("/node1", "node11".getBytes());`}}


### curator的client.delete()调用链： [	](zookeeper_20201127124859793)
+ 删除包含子节点的节点：{{c1:: `.deletingChildrenIfNeeded()`}}
+ 指定节点版本号：{{c1:: `.withVersion(2)`}}
+ 异步方式删除节点：{{c1:: `.inBackground((client,event)-> System.out.println(event.getPath()))`}}
+ 指定需删除节点的路径:{{c1:: `.forPath("/node1");`}}

### curator的client.getData()调用链： [	](zookeeper_20201127124859795)
+ 读取节点属性：{{c1:: `Stat stat = new Stat();` `.storingStatIn(stat)` }}
+ 异步方式读取节点：{{c1:: `.inBackground((client,event)-> System.out.println(event.getPath()))`}}
+ 指定需查询节点的路径:{{c1:: `.forPath("/node1");`}}
### curator的client.getChildren()调用链： [	](zookeeper_20201127124859798)

+ 异步方式读取子节点：`.inBackground((curatorFramework,  curatorEvent)-> curatorEvent.getChildren())`
+ 指定需查询节点的路径:{{c1:: `.forPath("/father");`}}

### curator的client.checkExists()调用链： [	](zookeeper_20201127124859801)

+ 异步判断节点：{{c1:: `.inBackground((client,event)-> System.out.println(event.getPath()))`}}
+ 指定需判断节点的路径:{{c1:: `.forPath("/node2");`}}

### curator的两种wacher监听器 [	](zookeeper_20201127124859804)
+ 思路：{{c1:: 注意获取单个节点与子节点的差别 }}
+ NodeCache:{{c1:: 只是监听某一个特定的节点，监听节点的新增和修改 }}
```java
    final NodeCache nodeCache=new NodeCache(client,"/watcher1");
    nodeCache.start();
    nodeCache.getListenable().addListener(new NodeCacheListener() {
      // 节点变化时回调的方法
        public void nodeChanged() throws Exception {
          System.out.println(nodeCache.getCurrentData().getPath());
            System.out.println(new String(nodeCache.getCurrentData().getData()));
        }
    });
    Thread.sleep(100000);
    nodeCache.close();
```
+ PathChildrenCache：{{c1:: 监控一个ZNode的子节点 }}
```java
    PathChildrenCache pathChildrenCache=new PathChildrenCache(client,"/watcher1",true);
    pathChildrenCache.start();
    pathChildrenCache.getListenable().addListener(new PathChildrenCacheListener() {
      // 当子节点方法变化时回调的方法
        public void childEvent(CuratorFramework curatorFramework, PathChildrenCacheEvent pathChildrenCacheEvent) throws Exception {
          // 节点的事件类型
            System.out.println(pathChildrenCacheEvent.getType());
            // 节点的路径
            System.out.println(pathChildrenCacheEvent.getData().getPath());
            // 节点数据
            System.out.println(new String(pathChildrenCacheEvent.getData().getData()));
        }
    });
    Thread.sleep(100000);
    pathChildrenCache.close();
```
+ 理解：{{c1:: 标签 }}

### curator事务的使用 [	](zookeeper_20201127124859807)
```java
  //{{c1::
  client.inTransaction()
          .create().forPath("/node1","node1".getBytes())
          .and()
          .create().forPath("/node2","node2".getBytes())
          .and()
          .commit();
  //}}
```

### curator分布式锁 [	](zookeeper_20201127124859809)
+ 思路：{{c1:: 加锁/解锁的方式都一样，3种锁获取的方式不同 }}
+ `InterProcessLock`:{{c1:: 锁接口类 }}
+ 具有实现类：
  + `InterProcessMutex`：{{c1:: 分布式可重入排它锁 }}
  + `InterProcessReadWriteLock`：{{c1:: 分布式读写锁 }}
```java
    @Test
    public void lock1() throws Exception {
        // 排他锁
        // arg1:连接对象
        // arg2:节点路径
        InterProcessLock interProcessLock = new InterProcessMutex(client, "/lock1");
        System.out.println("等待获取锁对象!");
        // 获取锁
        interProcessLock.acquire();
        for (int i = 1; i <= 10; i++) {
            Thread.sleep(3000);
            System.out.println(i);
        }
        // 释放锁
        interProcessLock.release();
        System.out.println("等待释放锁!");
    }

    @Test
    public void lock2() throws Exception {
        // 读写锁
        InterProcessReadWriteLock interProcessReadWriteLock=new InterProcessReadWriteLock(client, "/lock1");
        // 获取读锁对象
        InterProcessLock interProcessLock=interProcessReadWriteLock.readLock();
        System.out.println("等待获取锁对象!");
        // 获取锁
        interProcessLock.acquire();
        for (int i = 1; i <= 10; i++) {
            Thread.sleep(3000);
            System.out.println(i);
        }
        // 释放锁
        interProcessLock.release();
        System.out.println("等待释放锁!");
    }

    @Test
    public void lock3() throws Exception {
        // 读写锁
        InterProcessReadWriteLock interProcessReadWriteLock=new InterProcessReadWriteLock(client, "/lock1");
        // 获取写锁对象
        InterProcessLock interProcessLock=interProcessReadWriteLock.writeLock();
        System.out.println("等待获取锁对象!");
        // 获取锁
        interProcessLock.acquire();
        for (int i = 1; i <= 10; i++) {
            Thread.sleep(3000);
            System.out.println(i);
        }
        // 释放锁
        interProcessLock.release();
        System.out.println("等待释放锁!");
    }
```
+ 理解：{{c1:: 标签 }}

## 工具 [	](zookeeper_20201202040742323)

### zookeeper四字监控命令 [	](zookeeper_20201127124859811)

+ 作用：{{c1:: 大多是查询命令，用来获取zooKeeper服务的当前状态及相关信息 }}
| 命令   | 描述                                                         |
| :----- | :----------------------------------------------------------- |
| `conf` | {{c1:: 输出相关服务配置的详细信息。比如端口、zk数据及日志配置路径、最大连接数，session超时时间、serverId等 }} |
| `cons` | {{c1:: 列出所有连接到这台服务器的客户端连接/会话的详细信息。包括“接受/发送”的包数量、session id 、操作延迟、最后的操作执行等信息 }} |
| `crst` | {{c1:: 重置当前这台服务器所有连接/会话的统计信息 }}          |
| `dump` | {{c1:: 列出未经处理的会话和临时节点 }}                       |
| `envi` | {{c1:: 输出关于服务器的环境详细信息 }}                       |
| `ruok` | {{c1:: 测试服务是否处于正确运行状态。如果正常返回"imok"，否则返回空 }} |
| `stat` | {{c1:: 输出服务器的详细信息：接收/发送包数量、连接数、模式（leader/follower）、节点总数、延迟。 所有客户端的列表 }} |
| `srst` | {{c1:: 重置server状态 }}                                     |
| `wchs` | {{c1:: 列出服务器watches的简洁信息：连接总数、watching节点总数和watches总数 }} |
| `wchc` | {{c1:: 通过session分组，列出watch的所有节点，它的输出是一个与watch相关的会话的节点列表 }} |
| `mntr` | {{c1:: 列出集群的健康状态。包括“接受/发送”的包数量、操作延迟、当前服务模式（leader/follower）、节点总数、watch总数、临时节点总数 }} |

### 2个zookeeper可视化工具: [	](zookeeper_20201127124859814)
1. {{c1::`ZooInspector`： 提供一个操作zk树的UI界面}}
2. {{c1::`taokeeper`： 监控ZK集群的状态 }}