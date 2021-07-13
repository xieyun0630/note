## 计算机网络体系结构 [ ](ComputerNetworking_20210709091758151)

### 计算机网络概念 [ ](ComputerNetworking_20210709091758153)
+ 通信系统模型：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707144252.png)
+ 定义：{{c1::计算机网络就是**互连**的、**自治**的计算机集合。自治-无主从关系，互连-互联互通}}
+ **网络协议**：{{c1::(network protocol)，简称为协议，是为进行网络中的数据交换而建立的规则、标准或约定。协议规定了通信实体之间所交换的消息的**格式、意义、顺序**以及针对收到信息或发生的事件所采取的“**动作**”（**actions**）}}
+ 协议的三要素：
  + **语法**
    + {{c1::数据与控制信息的结构或格式}}
    + {{c1::信号电平}}
  + **语义**
    + {{c1::需要发出何种控制信息}}
    + {{c1::完成何种动作以及做出何种响应}}
    + {{c1::差错控制}}
  + **时序**
    + {{c1::事件顺序}}
    + {{c1::速度匹配}}
  + Internet协议标准
    + **RFC**: {{c1::Request for Comments}}
    + **IETF**: {{c1::互联网工程任务组（ Internet Engineering Task Force）}}

### 多路复用概念 [ ](ComputerNetworking_20210709091758155)
+ 定义：
  1. **划分**：{{c1::Multiplexing，将链路/网络资源（如带宽）划分为“资源片”}}
  2. **呼叫**：{{c1::将资源片分配给各路“呼叫”（calls）}}
  3. **独占**：{{c1::每路呼叫独占分配到的资源片进行通信}}
  4. **闲置**：{{c1::资源片可能“闲置”(idle)(无共享)}}
+ 多路复用图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707151227.png)}}
+ 典型多路复用方法:
  + 频分多路复用( frequency division multiplexing-**FDM** )：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707154158.png)}}
  + 时分多路复用( time divisionmultiplexing-**TDM** )：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707154148.png)}}
  + 波分多路复用(Wavelengthdivision multiplexing-**WDM**)：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707154107.png)}}
  + 码分多路复用( Code division multiplexing-**CDM** )：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707154128.png)}}

### 数据交换的类型 [ ](ComputerNetworking_20210709091758157)
+ {{c1::电路交换}}
+ {{c1::报文交换}}
+ {{c1::分组交换}}

### 电路交换 [ ](ComputerNetworking_20210709091758159)
  + 最典型电路交换网络：{{c1::电话网络}}
  + 电路交换的三个阶段：
    1. {{c1::建立连接（呼叫/电路建立）}}
    2. {{c1::通信}}
    3. {{c1::释放连接（拆除电路）}}
  + 独占资源
  + 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707150756.png)}}

### 报文交换与分组交换 [ ](ComputerNetworking_20210709091758161)
+ **报文**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707155527.png)}}
+ **分组**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707155626.png)}}
+ **分组交换:统计多路复用**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707161918.png)}}
+ **store-and-forward**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162002.png)}}
+ **分组传输延迟（时延）计算**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162235.png)}}

### 报文交换 vs 分组交换 [ ](ComputerNetworking_20210709091758163)
+ 问：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162320.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162410.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162524.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162548.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162608.png)}}


### 计算机网络性能相关名词:延迟/时延 [ ](ComputerNetworking_20210709091758165)
+ **延迟/时延**: {{c1::(delay或latency)}}
  + 四种分组延迟:
    + **结点处理延迟**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707163830.png)}}
    + **排队延迟**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707163844.png)}}
    + **传输延迟**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707163910.png)}}
    + **传播延迟**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707163919.png)}}
  + 四种分组延迟的关系:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707164006.png)}}
  + **流量强度**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707164221.png)}}


### 计算机网络性能相关名词 [ ](ComputerNetworking_20210709091758167)
+ **速率**：{{c1::速率即数据率(data rate)或称数据传输速率或比特率(bit rate)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707163201.png)}}
+ **带宽**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707163557.png)}}
+ **时延带宽积**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707164756.png)}}
+ **丢包率**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707164858.png)}}
+ **Throughput**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707165046.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707165103.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707165112.png)}}

### 计算机网络体系结构:OSI参考模型 [ ](ComputerNetworking_20210709091758169)
+ 名词：
  + **PDU**：{{c1::一般指协议数据单元。协议数据单元，是指在分层网络结构，例如在开放式系统互联（OSI）模型中，在传输系统的每一层都将建立协议数据单元（PDU）。}}
+ OSI参考模型解释**通信过程**示意图:![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707165615.png)
+ OSI参考模型**数据封装与通信过程**示意图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707165723.png)

### OSI参考模型：物理/数据链路/网络层功能 [ ](ComputerNetworking_20210709091758171)
+ 物理层功能图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708081415.png)}}
+ 数据链路层功能：
  1. **负责结点-结点**：{{c1::（node-to-node）数据传输}}
  2. **组帧**：{{c1::Framing}}
  3. **物理寻址**：{{c1:: （Physical addressing）,在帧头中增加发送端和/或接收端的物理地址标识数据帧的发送端和/或接收端 }}
  4. **流量控制**： {{c1::Flow control，避免淹没接收端}}
  5. **差错控制**： {{c1::Error control，检测并重传损坏或丢失帧，并避免重复帧}}
  6. **访问(接入)控制**：{{c1::Access control，在任一给定时刻决定哪个设备拥有链路（物理介质）控制使用权}}
  + 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708082419.png)}}
+ 网络层功能：
  + **负责**：{{c1::源主机到目的主机数据分组（packet）交付，可能穿越多个网络}}
  + **逻辑寻址**：{{c1::Logical addressing，全局唯一逻辑地址，确保数据分组被送达目的主机，如IP地址}}
  + **路由**：{{c1::Routing，路由器(或网关)互连网络，并路由分组至最终目的主机，路径选择}}
  + **分组转发**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708083048.png)}}

### OSI参考模型：传输/会话/表示/应用层功能 [ ](ComputerNetworking_20210709091758173)
+ 传输层功能
  + 负责：{{c1::**源-目的（端-端） （进程间） 完整报文**传输}}
  + 主要功能：{{c1::**分段与重组，SAP寻址，连接控制，流量控制，差错控制**![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708083502.png)}}
+ 会话层功能
  + 主要功能：**对话控制（dialog controlling）**，**同步(synchronization)**，最“**薄**”的一层
  + 图示：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708083641.png)
+ 表示层功能：
  + 主要功能：{{c1::数据表示转化，转换为主机独立的编码。加密/解密，压缩/解压缩。}}
  + 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708084310.png)}}
+ 应用层功能：
  + 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708084412.png)}}

### TCP/IP参考模型 [ ](ComputerNetworking_20210709091758175)
+ 体系图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708084506.png)
+ 各层功能描述：
  + 应用层:{{c1:: 支持各种网络应用，FTP, SMTP, HTTP}}
  + 传输层:{{c1:: 进程-进程的数据传输，TCP, UDP}}
  + 网络层:{{c1:: 源主机到目的主机的数据分组路由与转发，IP协议、路由协议等}}
  + 链路层:{{c1:: 相邻网络元素（主机、交换机、路由器等）的数据传输，以太网（Ethernet）、802.11 (WiFi)、PPP}}
  + 物理层:{{c1:: 比特传输}}
+ 5层模型的数据封装过程图:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708084736.png)}}


### 网络应用的体系结构 [ ](ComputerNetworking_20210709091758177)
+ **C/S**: {{c1::客户机/服务器结构(Client-Server, C/S)}}
+ **P2P**: {{c1::点对点结构(Peer-to-peer, P2P)}}
+ **Hybrid**: {{c1::混合结构(Hybrid)}}

## 应用层 [ ](ComputerNetworking_20210713081145914)


### 应用层协议的内容 [ ](ComputerNetworking_20210709091758179)
+ 消息的类型(type)
  +  {{c1::请求消息}}
  +  {{c1::响应消息}}
+ 消息的语法(syntax)/格式
  +  {{c1::消息中有哪些字段(field)？}}
  +  {{c1::每个字段如何描述}}
+ 字段的语义(semantics)
  +  {{c1::字段中信息的含义}}
+ 规则(rules)
  +  {{c1::进程何时发送/响应消息}}
  +  {{c1::进程如何发送/响应消息}}
+ 示例图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708085941.png)}}

### 网络应用对传输服务的需求 [ ](ComputerNetworking_20210709091758181)
+ 数据丢失(data loss)/可靠性(reliability)
  + {{c1::某些网络应用能够容忍一定的数据丢失：网络电话}}
  + {{c1::某些网络应用要求100%可靠的数据传输：文件传输，telnet}}
+ 时间(timing)/延迟(delay)
  + {{c1::有些应用只有在延迟足够低时才“有效”}}
  + {{c1::网络电话/网络游戏}}
+ 带宽(bandwidth)
  + {{c1::某些应用只有在带宽达到最低要求时才“有效”：网络视频}}
  + {{c1::某些应用能够适应任何带宽——弹性应用：email}}
+ TCP服务/UDP服务简介图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708090320.png)}}

### Email应用 [ ](ComputerNetworking_20210709091758183)
+ **SMTP**协议：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708111647.png)}}
+ **SMTP**交互示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708111847.png)}}
+ **SMTP消息格式**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708112058.png)}}
+ **邮件访问协议简介**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708112701.png)}}

### DNS概述 [ ](ComputerNetworking_20210709091758185)
+ DNS:{{c1:: `Domain Name System` }}
+ **顶级域名服务器(TLD, top-level domain)**: {{c1::负责com, org, net,edu等顶级域名和国家顶级域名，例如cn, uk, fr等}}
+ **权威(Authoritative)域名服务器**：{{c1::组织的域名解析服务器，提供组织内部服务器的解析服务}}
+ **本地域名解析服务器**：{{c1::当主机进行DNS查询时，查询被发送到本地域名服务器。作为代理(proxy)，将查询转发给（层级式）域名解析服务器系统}}
+ **DNS记录缓存和更新**：{{c1::只要域名解析服务器获得**域名—IP映射**，即缓存这一映射，一段时间过后，缓存条目失效（删除），本地域名服务器一般会缓存顶级域名服务器的映射，因此根域名服务器不经常被访问}}
+ DNS查询示例：
  + 迭代查询：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708133001.png)}}
  + 递归查询: {{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708133035.png)}}
+ 例题:![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708133206.png)
+ 答：{{c1::**A**}}
+ 如何注册域名:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708135156.png)}}


### DNS记录和消息格式 [ ](ComputerNetworking_20210709091758187)
+ **RR**：{{c1::资源记录(RR, resource records)}}
+ 记录格式：{{c1::`RR format: (name, value, type, ttl)`}}
+ **Type=A**
  + **Name**: {{c1::主机域名}}
  + **Value**: {{c1::IP地址}}
+ **Type=NS**
  + **Name**: {{c1::域(edu.cn)}}
  + **Value**: {{c1::该域权威域名解析服务器的主机域名}}
+ **Type=CNAME**
  + **Name**: {{c1::某一真实域名的别名}}
  + **Value**: {{c1::真实域名}}
+ **Type=MX**
  + **Value**: {{c1::是与name相对应的邮件服务器}}

### P2P概述 [ ](ComputerNetworking_20210709091758189)
+ 客户机/服务器 vs. P2P例子：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708142111.png)}}
+ BitTorrent协议：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708142216.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708142245.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210708142223.png)}}

## Socket编程 [ ](ComputerNetworking_20210713081145917)

### Socket编程-应用编程接口 [ ](ComputerNetworking_20210713081145919)
+ Socket在网络体系结构中的位置：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711121257.png)}}
+ 应用编程接口API：{{c1::就是应用进程的控制权和操作系统的控制权进行转换的一个系统调用接口.![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711121532.png)}}
+ 典型的应用编程接口：
  + **socket**：{{c1:: Berkeley UNIX 操作系统定义了一种 API，称为套接字接口(socket interface)，简称套接字（socket）。}}
  + **WINSOCK**：{{c1::微软公司在其操作系统中采用了套接字接口 API，形成了一个稍有不同的 API，并称之为Windows Socket Interface，WINSOCK。}}
  + **TLI**：{{c1::AT&T 为其 UNIX 系统 V 定义了一种 API，简写为 TLI (Transport Layer Interface)。}}

### Socket API函数总览 [ ](ComputerNetworking_20210713081145921)
+ `WSAStartup`: {{c1::初始化socket库(仅对WinSock)}}
+ `WSACleanup`: {{c1::清楚/终止socket库的使用 (仅对WinSock)}}
+ `socket`: {{c1::创建套接字}}
+ connect:{{c1::“连接”远端服务器 (仅用于客户端)}}
+ `closesocket`: {{c1::释放/关闭套接字}}
+ `bind`: {{c1::绑定套接字的本地IP地址和端口号（通常客户端不}}
需要）
+ `listen`: {{c1::置服务器端TCP套接字为监听模式，并设置队列}}
大小 (仅用于服务器端TCP套接字)
+ `accept`: {{c1::接受/提取一个连接请求，创建新套接字，通过新}}
套接 (仅用于服务器端的TCP套接字)
+ `recv`: {{c1::接收数据（用于TCP套接字或连接模式的客户端}}
UDP套接字）
+ `recvfrom`: {{c1::接收数据报（用于非连接模式的UDP套接字）}}
+ `send`: {{c1::发送数据（用于TCP套接字或连接模式的客户端}}
UDP套接字）
+ `sendto`: {{c1::发送数据报（用于非连接模式的UDP套接字）}}
+ `setsockopt`: {{c1::设置套接字选项参数}}
+ `getsockopt`: {{c1::获取套接字选项参数}}

### Socket API [ ](ComputerNetworking_20210713081145923)
+ 对外如何标识通信端点：{{c1::IP地址+端口号}}
  + `sockaddr_in`结构:![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711124901.png)
    + 作用:{{c1::使用TCP/IP协议簇的网络应用程序声明端点地址变量时，使用结构sockaddr_in}}
+ 对内操作系统/进程如何管理套接字：{{c1::使用小整数的套接字描述符（socket descriptor）![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711122306.png)}}

### Socket API函数:WSAStartup [ ](ComputerNetworking_20210713081145925)
+ API:`int WSAStartup(WORD wVersionRequested, LPWSADATA lpWSAData);`
+ 作用：{{c1::使用Socket的应用程序在使用Socket之前必须首先调用
WSAStartup函数}}
+ 两个参数:
  + `wVersionRequested`：{{c1::指明程序请求使用的WinSock版本，其中高位字节指明副版本、低位字节指明主版本.十六进制整数，例如0x102表示2.1版}}
  + `lpWSAData`:{{c1::返回实际的WinSock的版本信息。指向WSADATA结构的指针}}
+ 例：使用2.1版本的WinSock的程序代码段:
  ```cpp
    //{{c1::
    wVersionRequested=MAKEWORD(2,1);
    err=WSAStartup(wVersionRequested,&wsaData);
    //}}
  ```
### Socket API函数:WSACleanup [ ](ComputerNetworking_20210713081145927)

+ API:`int WSACleanup (void);`
+ 作用：{{c1::应用程序在完成对请求的Socket库的使用，最后要调用WSACleanup函数，**解除与Socket库的绑定**，**释放Socket库所占用的系统资源**。}}

### Socket API函数:socket [ ](ComputerNetworking_20210713081145929)
+ API:`sd = socket(protofamily,type,proto);`
+ 作用：{{c1::创建套接字，操作系统返回套接字描述符（sd）}}
+ `protofamily`: {{c1::协议族,protofamily = PF_INET（TCP/IP）}}
+ `type`: {{c1::套接字类型,`type = SOCK_STREAM,SOCK_DGRAM or SOCK_RAW`（TCP/IP）}}
  
  + Socket面向TCP/IP的服务类型:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711131611.png)}}
+ `proto`: {{c1::协议号,0为默认}}
+ 例：创建一个流套接字的代码段
  ```cpp
  //{{c1::
  struct protoent *p;
  p=getprotobyname("tcp");
  SOCKET sd=socket(PF_INET,SOCK_STREAM,p->p_proto); 
  //}}
  ```
### Socket API函数:Closesocket [ ](ComputerNetworking_20210713081145931)
+ API:`int closesocket(SOCKET sd);`
+ 作用：{{c1::关闭一个描述符为sd的套接字。如果多个进程共享一个套接字，调用closesocket将套接字引用计数减1，减至0才关闭}}
+ 返回值：
  + {{c1::0：成功}}
  + {{c1::SOCKET_ERROR：失败}}
+ 注意：{{c1::一个进程中的多线程对一个套接字的使用无计数,如果进程中的一个线程调用closesocket将一个套接字关闭，该进程中的其他线程也将不能访问该套接字}}

### Socket API函数:bind [ ](ComputerNetworking_20210713081145933)
+ API:`int bind(sd,localaddr,addrlen);`
+ 参数:
  + **sd**:{{c1:: 套接字描述符（sd）}}
  + **localaddr**:{{c1:: 端点地址（localaddr）,就是结构`sockaddr_in` }}
+ `INADDR_ANY`:{{c1:: 设置结构sockaddr_in中的IP地址为INADDR_ANY，代表绑定本地任意IP地址。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711141612.png) }}
+ 注意: {{c1::该函数通常只有服务器端调用，客户端一般由操作系统自动绑定好。}}

### Socket API函数:listen [ ](ComputerNetworking_20210713081145935)
+ API:`int listen(sd,queuesize);`
+ 作用: {{c1::设置服务器端的流套接字处于监听状态**}}
+ 使用限制:
  + {{c1::仅服务器端调用。}}
  + {{c1::仅用于面向连接的流套接字。}}
+ 参数：
  + **sd**:{{c1:: 套接字描述符（sd）}}
  + **queuesize**：{{c1::设置连接请求队列大小（queuesize）}}
+ 返回值：
  + {{c1::0：成功}}
  + {{c1::SOCKET_ERROR：失败}}


### Socket API函数:connect [ ](ComputerNetworking_20210713081145937)
+ API:`connect(sd,saddr,saddrlen);`
+ 作用:{{c1::客户程序调用connect函数来使客户套接字（sd）与特定计算机的特定端口（saddr）的套接字（服务）进行连接![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711145426.png)}}
+ 使用限制：
  + {{c1::仅用于客户端}}
  + {{c1::可用于TCP客户端也可以用于UDP客户端}}

### Socket API函数:accept [ ](ComputerNetworking_20210713081145939)
+ API:`newsock = accept(sd,caddr,caddrlen);`
+ 作用：{{c1::服务程序调用accept函数从处于监听状态的流套接字sd的客户连接请求队列中取出排在最前的一个客户请求，并且创建一个**新的套接字**来与客户套接字创建连接通道}}
+ 使用限制
  + {{c1::仅用于TCP套接字}}
  + {{c1::仅用于服务器}}
+ 图示:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711151425.png)}}


### Socket API函数:send, sendto,recv, recvfrom [ ](ComputerNetworking_20210713081145941)
+ API:
  + `send(sd,*buf,len,flags);`
  + `sendto(sd,*buf,len,flags,destaddr,addrlen);`
+ 使用场景：
  + **send**：{{c1::TCP套接字（客户与服务器）或**调用了connect函数的UDP客户端**套接字}}
  + **sendto**：{{c1::用于UDP**服务器端**套接字与**未调用**connect函数的UDP**客户端**套接字}}
+ API:
  + `recv(sd,*buffer,len,flags);`
  + `recvfrom(sd,*buf,len,flags,senderaddr,saddrlen);`
+ 使用场景：
  + **recv**：{{c1::recv函数从TCP连接的**另一端**接收数据，或者从**调用了connect函数的UDP客户端**套接字接收服务器发来的数据}}
  + **recvfrom**：{{c1::recvfrom函数用于从UDP**服务器端**套接字与**未调用**connect函数的UDP**客户端**套接字接收对端数据}}

### Socket API函数:setsockopt, getsockopt [ ](ComputerNetworking_20210713081145943)
+ API:
  + `int setsockopt(int sd, int level, int optname,*optval, int optlen);`
  + `int getsockopt(int sd, int level, int optname,*optval, socklen_t *optlen);`
+ 作用：
  + `setsockopt()`:{{c1:: 用来设置套接字sd的选项参数 }}
  + `getsockopt()`:{{c1:: 用于获取任意类型、任意状态套接口的选项当前值，并把结果存入optval }}
+ 可以实现本地字节顺序与网络字节顺序间转换的函数：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711161257.png)}}

### 网络应用的Socket API(TCP)调用基本流程 [ ](ComputerNetworking_20210713081145945)
+ 顺序图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711155908.png)}}

### Socket客户端软件设计:获取服务器相关信息函数 [ ](ComputerNetworking_20210713081145947)
+ `inet_addr( )` `gethostbyname( ) `: {{c1:: 解析服务器IP地址 ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711222923.png)}}
+ `getservbyname( )`: {{c1:: 解析服务器（熟知）端口号 ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711223742.png)}}
+ `getprotobyname( )`:{{c1:: 解析协议号 ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210711223812.png)}}

### Socket客户端软件套接字调用流程 [ ](ComputerNetworking_20210713081145949)
+ TCP客户端软件流程
  1. {{c1::确定服务器**IP地址**与**端口号**}}
  2. {{c1::创建套接字}}
  3. {{c1::分配本地端点地址（IP地址+端口号）}}
     + 注意：{{c1::这步通常由操作系统自动分配}}
  4. {{c1::连接服务器（套接字）}}
  5. {{c1::遵循应用层协议进行通信}}
  6. {{c1::关闭/释放连接}}
+ UDP客户端软件流程
  1. {{c1::确定服务器**IP地址**与**端口号**}}
  2. {{c1::创建套接字}}
  3. {{c1::分配本地端点地址（IP地址+端口号）}}
     + 注意：{{c1::这步通常由操作系统自动分配}}
  4. {{c1::指定服务器端点地址，构造UDP数据报}}
  5. {{c1::遵循应用层协议进行通信}}
  6. {{c1::关闭/释放套接字}}
+ 思考区别：{{c1::二者区别，只在于第四步，连接/直接发送数据报}}

### Socket客户端软件的实现 [ ](ComputerNetworking_20210713081145951)
+ 设计一个`connectsock`过程封装底层代码：
  ```cpp
  /* consock.cpp - connectsock */
  #include <stdlib.h>
  #include <stdio.h>
  #include <string.h>
  #include <winsock.h>
  #ifndef INADDR_NONE
  #define INADDR_NONE 0xffffffff
  #endif /* INADDR_NONE */
  void errexit(const char *, ...);
  /*-------------------------------------------------------
  * connectsock - allocate & connect a socket using TCP or UDP
  *------------------------------------------------------
  */
  SOCKET connectsock(const char *host, const char *service, const char
                    *transport )
  {
    struct hostent *phe; /* pointer to host information entry */
    struct servent *pse; /* pointer to service information entry */
    struct protoent *ppe; /* pointer to protocol information entry */
    struct sockaddr_in sin;/* an Internet endpoint address */
    int s, type; /* socket descriptor and socket type */

    memset(&sin, 0, sizeof(sin));
    sin.sin_family = AF_INET; 

    /* Map service name to port number */
    if ( pse = getservbyname(service, transport) )
    sin.sin_port = pse->s_port;
    else if ( (sin.sin_port = htons((u_short)atoi(service))) == 0 )
    errexit("can't get \"%s\" service entry\n", service);

    /* Map host name to IP address, allowing for dotted decimal */
    if ( phe = gethostbyname(host) )
    memcpy(&sin.sin_addr, phe->h_addr, phe->h_length);
    else if ( (sin.sin_addr.s_addr = inet_addr(host))==INADDR_NONE)
    errexit("can't get \"%s\" host entry\n", host);

    /* Map protocol name to protocol number */
    if ( (ppe = getprotobyname(transport)) == 0)
    errexit("can't get \"%s\" protocol entry\n", transport); 

    /* Use protocol to choose a socket type */
    if (strcmp(transport, "udp") == 0)
    type = SOCK_DGRAM;
    else
    type = SOCK_STREAM;

    /* Allocate a socket */
    s = socket(PF_INET, type, ppe->p_proto);
    if (s == INVALID_SOCKET)
    errexit("can't create socket: %d\n", GetLastError());

    /* Connect the socket */
    if (connect(s, (struct sockaddr *)&sin, sizeof(sin))==SOCKET_ERROR)
    errexit("can't connect to %s.%s: %d\n", host, service,
    GetLastError());
    return s;
  }
  ```
+ 异常处理函数`errexit`:
  ```cpp
  /* errexit.cpp - errexit */
  #include <stdarg.h>
  #include <stdio.h>
  #include <stdlib.h>
  #include <winsock.h>
  /*----------------------------------------------------------
  * errexit - print an error message and exit
  *----------------------------------------------------------
  */
  /*VARARGS1*/
  void errexit(const char *format, ...)
  { 
    va_list args;
    va_start(args, format);
    vfprintf(stderr, format, args);
    va_end(args);
    //这一步是主要，上面几行是错误消息输出
    WSACleanup();
    exit(1);
  }
  ```
+ 设计connectUDP过程用于创建连接模式客户端UDP套接字:
  ```CPP
  /* conUDP.cpp - connectUDP */
  #include <winsock.h>
  SOCKET connectsock(const char *, const char *, const char *);
  /*-------------------------------------------------------
  * connectUDP - connect to a specified UDP service
  * on a specified host
  *-----------------------------------------------------
  */
  SOCKET connectUDP(const char *host, const char *service )
  {
  return connectsock(host, service, "udp");
  }
  ```
+ 设计connectTCP过程，用于创建客户端TCP套接字:
  ```CPP
  /* conTCP.cpp - connectTCP */
  #include <winsock.h>
  SOCKET connectsock(const char *, const char *, const char *);
  /*----------------------------------------------------
  * connectTCP - connect to a specified TCP service
  * on a specified host
  *---------------------------------------------------
  */
  SOCKET connectTCP(const char *host, const char *service )
  {
    return connectsock( host, service, "tcp");
  }
  ```
+ 例1：访问DAYTIME服务的客户端（TCP）
  ```CPP 
    /* TCPdtc.cpp - main, TCPdaytime */
    #include <stdlib.h>
    #include <stdio.h>
    #include <winsock.h>
    void TCPdaytime(const char *, const char *);
    void errexit(const char *, ...);
    SOCKET connectTCP(const char *, const char *);
    #define LINELEN 128
    #define WSVERS MAKEWORD(2, 0)
    /*--------------------------------------------------------
    * main - TCP client for DAYTIME service
    *--------------------------------------------------------
    */
    int main(int argc, char *argv[])
    {
      char *host = "localhost"; /* host to use if none supplied */
      char *service = "daytime"; /* default service port */
      WSADATA wsadata;
      switch (argc) {
        case 1:
          host = "localhost";
          break;
        case 3:
          service = argv[2];
          /* FALL THROUGH */
        case 2:
          host = argv[1];
          break;
        default:
          fprintf(stderr, "usage: TCPdaytime [host [port]]\n");
          exit(1);
      }
      
      if (WSAStartup(WSVERS, &wsadata) != 0)
          errexit("WSAStartup failed\n");
        TCPdaytime(host, service);
        WSACleanup();
        return 0; /* exit */
    }
    /*-----------------------------------------------------
    * TCPdaytime - invoke Daytime on specified host and print results
    *-----------------------------------------------------
    */
    void TCPdaytime(const char *host, const char *service)
    {
      char buf[LINELEN+1]; /* buffer for one line of text */
      SOCKET s; /* socket descriptor */
      int cc; /* recv character count */
      s = connectTCP(host, service);
      cc = recv(s, buf, LINELEN, 0);
      while( cc != SOCKET_ERROR && cc > 0)
      {
        buf[cc] = '\0'; /* ensure null-termination */
        (void) fputs(buf, stdout);
        cc = recv(s, buf, LINELEN, 0);
      }
      closesocket(s);
    }
  ```
+ 例2：访问DAYTIME服务的客户端（UDP）
```CPP
  /* UDPdtc.cpp - main, UDPdaytime */
  #include <stdlib.h>
  #include <stdio.h>
  #include <winsock.h>
  void UDPdaytime(const char *, const char *);
  void errexit(const char *, ...);
  SOCKET connectUDP(const char *, const char *);
  #define LINELEN 128
  #define WSVERS MAKEWORD(2, 0)
  #define MSG “what daytime is it?\n"
  /*--------------------------------------------------------
  * main - UDP client for DAYTIME service
  *--------------------------------------------------------
  */
  int main(int argc, char *argv[])
  {
    char *host = "localhost"; /* host to use if none supplied */
    char *service = "daytime"; /* default service port */
    WSADATA wsadata;
    switch (argc) {
      case 1:
        host = "localhost";
        break;
      case 3:
        service = argv[2];
        /* FALL THROUGH */
      case 2:
        host = argv[1];
        break;
      default:
        fprintf(stderr, "usage: UDPdaytime [host [port]]\n");
        exit(1);
    }
    if (WSAStartup(WSVERS, &wsadata) != 0)
      errexit("WSAStartup failed\n");
    UDPdaytime(host, service);
    WSACleanup();
    return 0; /* exit */
  }
  void UDPdaytime(const char *host, const char *service)
  {
    char buf[LINELEN+1]; /* buffer for one line of text */
    SOCKET s;            /* socket descriptor */
    int n;               /* recv character count */
    
    s = connectUDP(host, service);
    (void) send(s, MSG, strlen(MSG), 0);
    /* Read the daytime */
    n = recv(s, buf, LINELEN, 0);
    if (n == SOCKET_ERROR)
      errexit("recv failed: recv() error %d\n", GetLastError());
    else
    {
      buf[cc] = '\0';    /* ensure null-termination */
      (void) fputs(buf, stdout);
    }
    closesocket(s);
    return 0;            /* exit */
  }
```
+ 理解：{{c1::标签}}


### Socket服务器软件设计:4种类型基本服务器 [ ](ComputerNetworking_20210713081145953)
1. 循环无连接服务器基本流程：{{c1::**Iterative connectionless**![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210713231053.png)}}
2. 循环面向连接服务器基本流程：{{c1::**Iterative connection-oriented**![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210713231346.png)}}
3. 并发无连接服务器基本流程：{{c1::**Concurrent connectionless**![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210713231403.png)}}
4. 并发面向连接服务器基本流程：{{c1::**Concurrent connection-oriented**![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210713231414.png)}}
+ 注意点:
  + `connect()` `sendto()`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210713231224.png)}}
  + 如何获取客户端点地址：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210713231317.png)}}

### Socket服务器的实现
+ 设计一个底层过程隐藏底层代码,`passivesock()`
+ 两个高层过程分别用于创建服务器端UDP套接字和TCP套接字,`passiveUDP()` `passiveTCP()`
+ `passivesock()`实现:
  ```cpp
  /* passsock.cpp - passivesock */
  #include <stdlib.h>
  #include <string.h>
  #include <winsock.h>
  void errexit(const char *, ...);
  /*-----------------------------------------------------------------------
  * passivesock - allocate & bind a server socket using TCP or UDP
  *------------------------------------------------------------------------
  */
  SOCKET passivesock(const char *service, const char *transport, int qlen)
  {
    struct servent *pse; /* pointer to service information entry */
    struct protoent *ppe; /* pointer to protocol information entry */
    struct sockaddr_in sin;/* an Internet endpoint address */
    SOCKET s; /* socket descriptor */
    int type; /* socket type (SOCK_STREAM, SOCK_DGRAM)*/

    memset(&sin, 0, sizeof(sin));
    sin.sin_family = AF_INET;
    sin.sin_addr.s_addr = INADDR_ANY;

    /* Map service name to port number */
    if ( pse = getservbyname(service, transport) )
      sin.sin_port = (u_short)pse->s_port;
    else if ( (sin.sin_port = htons((u_short)atoi(service))) == 0 )
      errexit("can't get \"%s\" service entry\n", service);

    /* Map protocol name to protocol number */
    if ( (ppe = getprotobyname(transport)) == 0)
        errexit("can't get \"%s\" protocol entry\n", transport);

    /* Use protocol to choose a socket type */
    if (strcmp(transport, "udp") == 0)
      type = SOCK_DGRAM;
    else
      type = SOCK_STREAM;

    /* Allocate a socket */
    s = socket(PF_INET, type, ppe->p_proto);
    if (s == INVALID_SOCKET)
      errexit("can't create socket: %d\n", GetLastError());

    /* Bind the socket */
    if (bind(s, (struct sockaddr *)&sin, sizeof(sin)) == SOCKET_ERROR)
      errexit("can't bind to %s port: %d\n", service,GetLastError());
    if (type == SOCK_STREAM && listen(s, qlen) == SOCKET_ERROR)
      errexit("can't listen on %s port: %d\n", service,GetLastError());
    return s;
  }
  ```
+ `passiveUDP()` `passiveTCP()`:
  ```cpp 
  /* passUDP.cpp - passiveUDP */
  #include <winsock.h>
  SOCKET passivesock(const char *, const char *, int);
  SOCKET passivesock(const char *, const char *, int);
  /*------------------------------------------------------------
  * passiveUDP - create a passive socket for use in a UDP server
  *-------------------------------------------------------------
  */
  SOCKET passiveUDP(const char *service)
  {
     return passivesock(service, "udp", 0);
  }
  /*------------------------------------------------------------
  * passiveTCP - create a passive socket for use in a TCP server
  *-------------------------------------------------------------
  */
  SOCKET passiveTCP(const char *service, int qlen)
  {
    return passivesock(service, "tcp", qlen);
  }
  ```
+ 理解:{{c1::标签}}

### socket使用案例：DAYTIME服务器
+ 例1：无连接循环DAYTIME服务器
  ```cpp
  /* UDPdtd.cpp - main, UDPdaytimed */
  #include <stdlib.h>
  #include <winsock.h>
  #include <time.h>
  void errexit(const char *, ...);
  SOCKET passiveUDP(const char *);
  #define WSVERS MAKEWORD(2, 0)
  /*------------------------------------------------------------------------
  * main - Iterative UDP server for DAYTIME service
  *------------------------------------------------------------------------
  */
  void main(int argc, char *argv[])
  {
    struct sockaddr_in fsin; /* the from address of a client */
    char *service = "daytime"; /* service name or port number */
    SOCKET sock; /* socket */
    int alen; /* from-address length */
    char * pts; /* pointer to time string */
    time_t now; /* current time */
    WSADATA wsadata;

    switch (argc)
    {
      case 1:
        break;
      case 2:
        service = argv[1];
        break;
      default:
        errexit("usage: UDPdaytimed [port]\n");
    }

    if (WSAStartup(WSVERS, &wsadata) != 0)
      errexit("WSAStartup failed\n");
    sock = passiveUDP(service);
    while (1)
    {
      alen = sizeof(struct sockaddr);
      if (recvfrom(sock,buf,sizeof(buf),0,(struct sockaddr *)&fsin,&alen) == SOCKET_ERROR)
        errexit("recvfrom: error %d\n", GetLastError());
      (void) time(&now);
      pts = ctime(&now);
      (void) sendto(sock,pts,strlen(pts),0,(struct sockaddr *)&fsin,sizeof(fsin));
    }
    return 1; /* not reached */
  }
  ```
  + 程序结构图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210713233543.png)
+ 例2：面向连接并发DAYTIME服务器
  ```java 
  /* TCPdtd.cpp - main, TCPdaytimed */
  #include <stdlib.h>
  #include <winsock.h>
  #include <process.h>
  #include <time.h>
  void errexit(const char *, ...);
  void TCPdaytimed(SOCKET);
  SOCKET passiveTCP(const char *, int);
  #define QLEN 5
  #define WSVERS MAKEWORD(2, 0)
  /*------------------------------------------------------------------------
  * main - Concurrent TCP server for DAYTIME service
  *------------------------------------------------------------------------
  */
  void main(int argc, char *argv[])
  {
    struct sockaddr_in fsin; /* the from address of a client */
    char *service = "daytime"; /* service name or port number*/
    SOCKET msock, ssock; /* master & slave sockets */
    int alen; /* from-address length */
    WSADATA wsadata;

    switch (argc) {
      case1:
      break;
      case2:
      service = argv[1];
      break;
      default:
      errexit("usage: TCPdaytimed [port]\n");
    }

    if (WSAStartup(WSVERS, &wsadata) != 0)
      errexit("WSAStartup failed\n");
      msock = passiveTCP(service, QLEN);
    while (1) {
      alen = sizeof(struct sockaddr);
      ssock = accept(msock, (struct sockaddr *)&fsin, &alen);
      if (ssock == INVALID_SOCKET)
        errexit("accept failed: error number %d\n",GetLastError());
      if (_beginthread((void (*)(void *)) TCPdaytimed, 0,(void *)ssock) < 0) {
        errexit("_beginthread: %s\n", strerror(errno));
      }
    }
    return 1; /* not reached */
  }

  /*----------------------------------------------------------------------
  * TCPdaytimed - do TCP DAYTIME protocol
  *-----------------------------------------------------------------------
  */
  void TCPdaytimed(SOCKET fd)
  {
    char * pts; /* pointer to time string */
    time_t now; /* current time */
    (void) time(&now);
    pts = ctime(&now);
    (void) send(fd, pts, strlen(pts), 0);
    (void) closesocket(fd);
  }
  ```
  + 程序结构图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210713233927.png)}}

## 传输层

### 传输层概述
+ 传输层作用：{{c1::传输层协议为运行在不同Host上的进程提供了一种**逻辑通信机制**![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210713235404.png)}}
+ 端系统运行传输层协议
  + 发送方：{{c1::将应用递交的消息分成一个或多个的Segment，并向下传给网络层。}}
  + 接收方：{{c1::将接收到的segment组装成消息，并向上交给应用层。}}
+ 基本机制：
  1. {{c1::复用/分用}}
  2. {{c1::可靠数据传输机制}}
  3. {{c1::流量控制机制}}
  4. {{c1::拥塞控制机制}}
+ 传输层vs.网络层: {{c1:: 网络层提供主机之间的逻辑通信机制, 传输层提供应用进程之间的逻辑通信机制 }}

### Internet传输层协议特点
+ TCP特点：{{c1::可靠、按序的交付服务，拥塞控制，流量控制，连接建立}}
+ UDP特点：{{c1::基于“**尽力而为(Best-effort)**”的网络层，没有做（可靠性方面的）扩展}}
+ 两种服务均不保证：{{c1::延迟，带宽}}

