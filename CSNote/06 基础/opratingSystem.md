
### printf函数操作系统底层调用过程 [ ](opratingSystem_20210714094413989)
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210713182148.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210713185742.png)}}


### 多进程图像
+ 多进程如何组织
  + PCB：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210727141252.png)
  + 进程状态图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210727141216.png)
+ 多进程如何交替：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210727141441.png)
+ 如何形成多进程图像:
  1. {{c1::读写`PCB`，OS中最重要的结构，贯穿始终}}
  2. {{c1::要操作寄存器完成**切换**（L10，L11，L12）}}
  3. {{c1::要写**调度**程序（L13，L14）}}
  4. {{c1::要有**进程同步**与合作（L16，L17）}}
  5. {{c1::要有**地址映射**（L20）}}


### 进程切换概念
+ 进程与线程的区分：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210727163622.png)}}
+ 用户级线程：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210727163811.png)}}
+ 核心级线程：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210727163839.png)}}
+ 用户级线程、核心级线程的对比：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210727164238.png)}}