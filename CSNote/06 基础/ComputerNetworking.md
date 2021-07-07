## 计算机网络基本概念

### 计算机网络概念
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

### 多路复用概念
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

### 数据交换的类型
+ {{c1::电路交换}}
+ {{c1::报文交换}}
+ {{c1::分组交换}}

### 电路交换
  + 最典型电路交换网络：{{c1::电话网络}}
  + 电路交换的三个阶段：
    1. {{c1::建立连接（呼叫/电路建立）}}
    2. {{c1::通信}}
    3. {{c1::释放连接（拆除电路）}}
  + 独占资源
  + 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707150756.png)}}

### 报文交换与分组交换
+ **报文**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707155527.png)}}
+ **分组**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707155626.png)}}
+ **分组交换:统计多路复用**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707161918.png)}}
+ **store-and-forward**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162002.png)}}
+ **分组传输延迟（时延）计算**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162235.png)}}

### 报文交换 vs 分组交换
+ 问：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162320.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162410.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162524.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162548.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707162608.png)}}


### 计算机网络性能相关名词:延迟/时延
+ **延迟/时延**: {{c1::(delay或latency)}}
  + 四种分组延迟:
    + **结点处理延迟**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707163830.png)}}
    + **排队延迟**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707163844.png)}}
    + **传输延迟**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707163910.png)}}
    + **传播延迟**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707163919.png)}}
  + 四种分组延迟的关系:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707164006.png)}}
  + **流量强度**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707164221.png)}}


### 计算机网络性能相关名词
+ **速率**：{{c1::速率即数据率(data rate)或称数据传输速率或比特率(bit rate)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707163201.png)}}
+ **带宽**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707163557.png)}}
+ **时延带宽积**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707164756.png)}}
+ **丢包率**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707164858.png)}}
+ **Throughput**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707165046.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707165103.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707165112.png)}}

### 计算机网络体系结构:OSI参考模型
+ 名词：
  + **PDU**：{{c1::一般指协议数据单元。协议数据单元，是指在分层网络结构，例如在开放式系统互联（OSI）模型中，在传输系统的每一层都将建立协议数据单元（PDU）。}}
+ OSI参考模型解释**通信过程**示意图:![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707165615.png)
+ OSI参考模型**数据封装与通信过程**示意图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210707165723.png)

### OSI参考模型：物理层功能