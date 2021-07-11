## 计算机网络基本概念 [ ](ComputerNetworking_20210709091758151)

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