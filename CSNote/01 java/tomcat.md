### Tomcat目录结构 [	](tomcat_20201017075500785)

+ `bin`:{{c1:: 启动和关闭需要的bat文件所在的目录}}
+ `conf`:{{c1:: 配置目录}}
  + `Catalina`:{{c1:: 用于存储针对每个虚拟机的 Context配置 }}
  + `contextxml`:{{c1:: 用于定义所有web应用均需加载的 ontext配置，如果web应用指定了自己的 context.xml该文件将被覆盖 }}
  + `catalina.properties`:{{c1:: Tomcat的环境变量配置 }}
  + `catalina.policy`:{{c1:: Tomcat运行的安全策略配置 }}
  + `loggingproperties`:{{c1:: Tomcat的日志配置文件，可以通过该文件修改 Tomcat的日志级别及日志路径等 }}
  + `serverxml`:{{c1:: Tomcat服务器的核心配置文件 }}
  + `tomcat-users.xml`:{{c1:: 定义 Tomcats默认的用户及角色映射信息配置 }}
  + `web.xml`:{{c1:: Tomcat中所有应用默认的部署描述文件，主要定义了基础 Servlet和MME映射。 }}
+ `lib`:{{c1:: tomcat运行时需要的jar包所在的目录}}
+ `logs`:{{c1:: 日志文件所在的目录}}
+ `temp`:{{c1:: tomcat运行时产生的临时文件存放的目录,不需要我们管理}}
+ `webapps`:{{c1:: 开发中最常用的目录,web应用放置到此目录下浏览器可以直接访问}}
+ `work`:{{c1:: 工作目录,tomcat运行时产生的工作文件存放在这个目录中}}

## Tomcat整体架构 [	](tomcat_20201017075500787)

### 连接器:Coyote [	](tomcat_20201017075500789)

+ 作用：处理Socket连接，负责网络字节流与Request和Response对象的转化。
+ 通过在Tomcat中配置多个Service，可以实现通过不同的端口号来访问同一台机器上部署的不同应用。
+ Coyote与Catalina的交互过程
+ ![image-20201016134550413](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201016134550413.png)

###  Tomcat支持的IO模型 [	](tomcat_20201017075500792)
- Tomcat 支持的IO模型（自8.5/9.0 版本起，Tomcat 移除了 对 BIO 的支持）：
  - `NIO` :{{c1:: 非阻塞I/O，采用Java NIO类库实现。  }}
  - `NIO2` :{{c1:: 异步I/O，采用JDK 7最新的NIO2类库实现。  }}
  - `APR` :{{c1:: 采用Apache可移植运行库实现，是C/C++编写的本地库。如果选择该方 案，需要单独安装APR库。 }}

### Tomcat支持的应用层协议 [	](tomcat_20201017075500794)
+ `HTTP/1.1`:{{c1:: 这是大部分Web应用采用的访问协议。 }}
+ `AJP`:{{c1:: 用于和Web服务器集成（如Apache），以实现对静态资源的优化以及 集群部署，当前支持AJP/1.3。 }}
+ `HTTP/2`:{{c1:: HTTP 2.0大幅度的提升了Web性能。下一代HTTP协议 ， 自8.5以及9.0 版本之后支持。 }}

### 连接器（Coyote）组件工作流程（图） [	](tomcat_20201017075500796)

![image-20201016140613291](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201016140613291.png)
- 在Tomcat中没有对应的Endpoint 接口， 但是有一个抽象类 AbstractEndpoint ，其下有三个实现类：
  - NioEndpoint
  - Nio2Endpoint
  - AprEndpoint 
- Tomcat按照协议和I/O提供了6个ProtocolHandler实现类： 
  - AjpNioProtocol 
  - AjpAprProtocol
  - AjpNio2Protocol 
  - Http11NioProtocol 
  - Http11Nio2Protocol 
  - Http11AprProtocol
+ 注意：我们在配置tomcat/conf/server.xml时，至少要指定具体的ProtocolHandler,当然也可以指定协议名称

### 容器 - Catalina [	](tomcat_20201017075500799)

+ 作用：Catalina是Tomcat的servlet容器实现，是tomcat中的核心
+ Tomcat 的模块分层结构图![image-20201016141342696](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201016141342696.png)

### Catalina 的主要组件结构： [	](tomcat_20201017075500802)

![image-20201016141443250](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201016141443250.png)

+ 各个组件的职责：

| 组件      | 职责                                                         |
| --------- | ------------------------------------------------------------ |
| Catalina  | 负责解析Tomcat的配置文件 , 以此来创建服务器Server组件，并根据 命令来对其进行管理 |
| Server    | 服务器表示整个Catalina Servlet容器以及其它组件，负责组装并启动Servlet引擎,Tomcat连接器。Server通过实现Lifecycle接口，提供了 一种优雅的启动和关闭整个系统的方式 |
| Service   | 服务是Server内部的组件，一个Server包含多个Service。它将若干个 Connector组件绑定到一个Container（Engine）上 |
| Connector | 连接器，处理与客户端的通信，它负责接收客户请求，然后转给相关 的容器处理，最后向客户返回响应结果 |
| Container | 容器，负责处理用户的servlet请求，并返回对象给web用户的模块   |

### Container 结构 [	](tomcat_20201017075500803)
+ Tomcat设计了4种容器，分别是Engine、Host、Context和Wrapper。
![image-20201016142854201](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201016142854201.png)
+ 各个组件的含义 ：
| 组件    | 职责                                                         |
| ------- | ------------------------------------------------------------ |
| Engine  | 表示整个Catalina的Servlet引擎，用来管理多个虚拟站点，一个Service 最多只能有一个Engine，但是一个引擎可包含多个Host |
| Host    | 代表一个虚拟主机，或者说一个站点，可以给Tomcat配置多个虚拟主 机地址，而一个虚拟主机下可包含多个Context |
| Context | 表示一个Web应用程序， 一个Web应用可包含多个Wrapper Wrapper 表示一个Servlet， |
| Wrapper | 作为容器中的最底层，不能包含子容器                           |

### Tomcat启动流程（序列图） [	](tomcat_20201017075500806)

![image-20201016143552616](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201016143552616.png)

### Lifecycle接口 [	](tomcat_20201017075500809)

+ 由于所有的组件均存在初始化、启动、停止等生命周期方法，拥有生命周期管理的特 性， 所以Tomcat在设计的时候， 基于生命周期管理抽象成了一个接口 Lifecycle ，而组 件 Server、Service、Container、Executor、Connector 组件 ， 都实现了一个生命周期 的接口，从而具有了以下生命周期中的核心方法：
+ 1） init（）：初始化组件 
+ 2） start（）：启动组件 
+ 3） stop（）：停止组件 
+ 4） destroy（）：销毁组件

### Tomcat请求处理流程（序列图） [	](tomcat_20201017075500811)

+ Mapper组件作用：{{c1:: 将用户请求的URL定位到一个Servlet }}

![image-20201016144731840](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201016144731840.png)

+ 将用户请求的URL定位到一个Servlet流程

  ![image-20201016144801093](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201016144801093.png)