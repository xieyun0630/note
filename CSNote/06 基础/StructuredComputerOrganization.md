## 计算机系统概述 [ ](StructuredComputerOrganization_20210208114913980)

### 计算机组成基本概念 [ ](StructuredComputerOrganization_20210208114913983)
+ 冯·诺依曼计算机的特点：
  1. {{c1::计算机由五大部件组成}}
  2. {{c1::指令和数据以同等地位存于存储器，可按地址寻访}}
  3. {{c1::指令和数据用二进制表示}}
  4. {{c1::指令由操作码和地址码组成}}
  5. {{c1::存储程序:将指令以二进制代码的形式事先输入计算机的主存储器}}
  6. {{c1::以运算器为中心（现在一般以存储器为中心）}}
+ **低电平与高电平**：{{c1::低电平(表示二进制0) 高电平(表示二进制1)}}

### 现代计算机的结构 [ ](StructuredComputerOrganization_20210208114913986)
+ 2种结构图：{{c1::![image-20210206155702525](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210206155702525.png)![image-20210206155724613](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210206155724613.png)}}

### 计算机各硬件部件 [ ](StructuredComputerOrganization_20210208114913990)

### 主存各部件作用 [ ](StructuredComputerOrganization_20210208114913992)
  + **存储体**：
    + **存储单元**：{{c1::每个存储单元存放一串二进制代码}}
    + **存储字(word)**：{{c1::存储单元中二进制代码的组合}}
    + **存储字长**：{{c1::存储单元中二进制代码的位数}}
    + **存储元**：{{c1::即存储二进制的电子元件，每个存储元可存`1bit`}}
  + **MAR**：{{c1::`Memory Address Register`（存储地址寄存器），MAR位数反映存储单元的个数}}
  + **MDR**：{{c1::`Memory Data Register`（存储地址寄存器），MDR位数=存储字长}}
    + 图示：{{c1::![image-20210206160348355](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210206160348355.png)}}

### 运算器与控制器各部件作用 [ ](StructuredComputerOrganization_20210208114913995)
+ 运算器各部件：
  + **ACC**： {{c1::Accumulator,累加器，用于存放操作数，或运算结果。}}
  + **MQ**： {{c1::Multiple-Quotient Register,乘商寄存器，在乘、除运算时，用于存放操作数或运算结果。}}
  + **X**： {{c1::通用的操作数寄存器，用于存放操作数}}
  + **ALU**： {{c1::Arithmetic and Logic Unit,算术逻辑单元，通过内部复杂的电路实现算数运算、逻辑运算}}
+ 控制器各部件作用：
  + **CU**：{{c1::Control Unit,控制单元，分析指令，给出控制信号}}
  + **IR**：{{c1::Instruction Register,指令寄存器，存放当前执行的指令}}
  + **PC**：{{c1::Program Counter,程序计数器，存放下一条指令地址，有自动加1功能}}

### 计算机的工作过程：编译装入主存 [ ](StructuredComputerOrganization_20210208114913998)
+ 图示：{{c1::![image-20210206163749195](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210206163749195.png)}}

### 计算机的工作过程：执行取数指令 [ ](StructuredComputerOrganization_20210208114914001)

+ 注意理解图中各步骤操作：![image-20210206164029398](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210206164029398.png)
+ 各步骤解释：
  + 初：{{c1::(PC)=0，指向第一条指令的存储地址}}
  + #1：{{c1::(PC)->MAR，导致(MAR)=0}}
  + #3：{{c1::M(MAR)->MDR，导致(MDR)=`000001 0000000101`}}
  + #4：{{c1::(MDR)->IR，导致(IR)=`000001 0000000101`}}
  + #5：{{c1::OP(IR)->CU，指令的**操作码**送到CU，CU分析后得知，这是“**取数**”指令}}
  + #6：{{c1::Ad(IR)->MAR，指令的地址码送到MAR，导致(MAR)=5}}
  + #8：{{c1::M(MAR)->MDR，导致(MDR)=**0000000000000010=2**}}
  + #9：{{c1::(MDR)->ACC，导致(ACC)=**0000000000000010=2**}}
+ 伪代码解释：![image-20210206165727087](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210206165727087.png)

### 计算机的工作过程：执行乘法指令 [ ](StructuredComputerOrganization_20210208114914004)
+ 注意理解图中各步骤操作：![image-20210206164515578](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210206164515578.png)
+ 各步骤解释：
    #1：{{c1::(PC)->MAR，导致(MAR)=1}} [ ](StructuredComputerOrganization_20210208114914006)
    #3：{{c1::M(MAR)->MDR，导致(MDR)=000100 0000000110}} [ ](StructuredComputerOrganization_20210208114914008)
    #4：{{c1::(MDR)->IR，导致(IR)= 000100 0000000110}} [ ](StructuredComputerOrganization_20210208114914010)
    #5：{{c1::OP(IR)->CU，指令的操作码送到CU， CU分析后得知，这是“乘法”指令}} [ ](StructuredComputerOrganization_20210208114914012)
    #6：{{c1::Ad(IR)->MAR，指令的地址码送到MAR，导致(MAR)=6}} [ ](StructuredComputerOrganization_20210208114914015)
    #8：{{c1::M(MAR)->MDR，导致(MDR)=0000000000000011=3}} [ ](StructuredComputerOrganization_20210208114914018)
    #9：{{c1::(MDR)->MQ，导致(MQ)=0000000000000011=3}} [ ](StructuredComputerOrganization_20210208114914022)
    #10：{{c1::(ACC)->X，导致(X)=2}} [ ](StructuredComputerOrganization_20210208114914024)
    #11：{{c1::(MQ)*(X)->ACC，由ALU实现乘法运算，导致(ACC)=6，如果乘积太大，则需要MQ辅助存储}} [ ](StructuredComputerOrganization_20210208114914029)

### 计算机的工作过程：执行加法指令 [ ](StructuredComputerOrganization_20210208114914031)

+ 注意图中各步骤操作：![image-20210206164814621](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210206164814621.png)
+ 各步骤解释：
  + #1：{{c1::(PC)->MAR，导致(MAR)=2}}
  + #3：{{c1::M(MAR)->MDR，导致(MDR)= 000011 0000000111}}
  + #4：{{c1::(MDR)->IR，导致(IR)= 000011 0000000111}}
  + #5：{{c1::OP(IR)->CU，指令的操作码送到CU， CU分析后得知，这是“加法”指令}}
  + #6：{{c1::Ad(IR)->MAR，指令的地址码送到MAR，导致(MAR)=7}}
  + #8：{{c1::M(MAR)->MDR，导致(MDR)=0000000000000001=1}}
  + #9：{{c1::(MDR)->X，导致(X)=0000000000000001=1}}
  + #10：{{c1::(ACC)+(X)->ACC，导致(ACC)=7，由ALU实现加法运算}}

### 计算机的工作过程：执行存数指令 [ ](StructuredComputerOrganization_20210208114914036)

+ 注意图中各步骤操作：![image-20210206165059253](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210206165059253.png)
+ 各步骤解释：
  + #1：{{c1::(PC)->MAR，导致(MAR)=3}}
  + #3：{{c1::M(MAR)->MDR，导致(MDR)=000010 0000001000}}
  + #4：{{c1::(MDR)->IR，导致(IR)= 000010 0000001000}}
  + #5：{{c1::OP(IR)->CU，指令的操作码送到CU，CU分析后得知，这是“存数”指令}}
  + #6：{{c1::Ad(IR)->MAR，指令的地址码送到MAR，导致(MAR)=8}}
  + #7：{{c1::(ACC)->MDR，导致(MDR)=7}}
  + #9：{{c1::(MDR)->地址为8的存储单元，导致y=7}}

### 计算机系统的层次结构 [ ](StructuredComputerOrganization_20210208114914038)

- 计算机硬件角度的5层结构：{{c1::![image-20210206175911557](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210206175911557.png)}}
+ 三种级别的语言之间的关系：{{c1::![image-20210206180007547](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210206180007547.png)}}
- 编译程序：{{c1::将高级语言编写的源程序全部 语句一次全部翻译成机器语言程序，而后 再执行机器语言程序（只需翻译一次） }}
- 解释程序：{{c1::将源程序的一条语句翻译成对 应于机器语言的语句，并立即执行。紧接 着再翻译下一句（每次执行都要翻译）}}

### CPU的性能指标 [ ](StructuredComputerOrganization_20210208114914040)
+ **CPU时钟周期** **CPU主频（时钟频率）** **CPI**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210206203948.png)}}
+ Eg：某CPU主频为 1000Hz，某程序包含100条指令，平均来看指令的CPI=3。该程序在该CPU上执行需要多久？
  + {{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210206204209.png)}}
+ **IPS** **FLOPS**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210206204635.png)}}

### 系统整体的性能指标 [ ](StructuredComputerOrganization_20210208114914043)
+ **数据通路带宽**：{{c1::数据总线一次所能并行传送信息的位数（各硬件部件通过数据总线传输数据）}}
+ **吞吐量**：{{c1::指系统在单位时间内处理请求的数量。}}
+ **响应时间**：{{c1::指从用户向计算机发送一个请求，到系统对该请求做出响应并获得它所需要的结果的等待时间。}}

## 数据的表示与运算 [ ](StructuredComputerOrganization_20210208114914045)

### 进位计数制及其相互转换 [ ](StructuredComputerOrganization_20210208114914048)
+ **任意进制->十进制**公式：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210206212426.png)}}
+  **二进制<-->八进制、十六进制**方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210206213450.png)注意：补位，整数补高位，小数补低位}}
+ **十进制->任意进制**
  + 整数部分：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210206214610.png)}}
  + 小数部分：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210206214619.png)}}
+ 真值与机器数：{{c1::**真值**表示符合人类习惯的数字，**机器数**表示数字实际存到机器里的形式，正负号需要被“数字化”}}

### BCD码 [ ](StructuredComputerOrganization_20210208114914050)
+ 含义：{{c1::`Binary-Coded Decimal`,用二进制编码的十进制，即使用4bit对应一个十进制数}}
+ 作用：{{c1::解决二进制转换到十进制麻烦的问题。}}
+ 8421码的加法（手算/机算）：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210206234913.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210206234934.png)}}
+ **余3码** **2421码**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210207000407.png)}}

### 字符与字符串在计算机内的表示与存储 [ ](StructuredComputerOrganization_20210208114914052)
+ 问：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210207002449.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210207002503.png)}}

### 数据校验原理 [ ](StructuredComputerOrganization_20210208114914053)
+ 作用：{{c1::解决计算机中数据传输出现错误的问题。}}
+ 码字：{{c1::由若干位代码组成的一个字叫码字}}
+ 两个码字间的距离：{{c1::将两个码字逐位进行对比，具有不同的位的个数称为两个码字间的距离。}}
+ 码距：{{c1::一种编码方案可能有若干个合法码字，各合法码字间的最小距离称为“码距”。若码距=2,有检错能力；若码距>=3,可能还会纠错能力}}


### 数据校验：奇偶校验码 [ ](StructuredComputerOrganization_20210208114914056)
+ 奇校验码：{{c1::整个校验码（有效信息位和校验位）中“1”的个数为奇数。}}
+ 偶校验码：{{c1::整个校验码（有效信息位和校验位）中“1”的个数为偶数。}}
+ 校验码结构：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210207011034.png)}}
+ 【例】 给出两个编码1001101和1010111的奇校验码和偶校验码：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210207010654.png)}}
+ 偶校验的硬件实现：{{c1::各信息进行异或（模2加）运算，得到的结果即为偶校验位}}
+ 注意：{{c1::奇偶校验码的码距d=2,仅能检测出**奇数位错误**，**无纠错**能力}}

### 数据校验：海明码* [ ](StructuredComputerOrganization_20210208114914060)
+ 海明码求解步骤，**信息位：1010**
  1. 确定海明码的位数：
      + {{c1::![image-20210207020946058](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210207020946058.png)}}
  2. 确定校验位的分布：
      + {{c1::![image-20210207020952688](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210207020952688.png)}}
  3. 求校验位的值：
      + {{c1::![image-20210207021000022](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210207021000022.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210207021231.png)}}
  4. 纠错：
      + {{c1::![image-20210207021018814](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210207021018814.png)}} 
 + 全体校验位：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210207022036.png)}}

### 定点数的表示 [ ](StructuredComputerOrganization_20210208114914067)