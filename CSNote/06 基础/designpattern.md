### 设计模式的目的 [	](designpattern_20200629095419184)

- 代码重用性:{{c1::  (即：相同功能的代码，不用多次编写)  }}
- 可读性 :{{c1:: (即：编程规范性, 便于其他程序员的阅读和理解) }}
- 可扩展性:{{c1::  (即：当需要增加新的功能时，非常的方便，称为可维护) }}
- 可靠性 :{{c1:: (即：当我们增加新的功能后，对原来的功能没有影响) }}
- 使程序呈现{{c1:: 高内聚，低耦合 }}的特性 

### 单一职责原则 [	](designpattern_20200629095419186)

**SRP**：{{c1:: Single Responsibility Principle }}

注意：我们应当遵守单一职责原则，只有逻辑足够简单，才可以在代码级违反单一职责原则；只有类中方法数量足够少，可以在方法级别保持单一职责原则

### 接口隔离原则 [	](designpattern_20200629095419187)

**ISP**：**Interface  Segregation Principle**

反例图：{{c1:: ![image-20200629211404990](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629211404990.png) }}

改进后接口隔离原则例图：{{c1::![image-20200629210906436](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629210906436.png)}}

### 依赖倒转原则 [	](designpattern_20200629095419189)

+ 定义：
    1. {{c1:: 上层模块不应该依赖底层模块，它们都应该依赖于抽象。}}
    2. {{c1:: 抽象不应该依赖于细节，细节应该依赖于抽象。}}
+ 披萨店例子：
    + 反例图：{{c1:: ![image-20200629212530571](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629212530571.png)}}
    + 改进后依赖倒转原则图：{{c1:: ![image-20200629212538616](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629212538616.png)}}



# FirstHead设计模式 [	](designpattern_20201202040742352)

### 设计原则 [	](designpattern_20201202040742355)

+ 变化：{{c1:: 找出应用中可能需要变化之处，把它们独立出来，不要和那些不需要变化的代码混在一起。}}
+ 面向接口：{{c1:: 针对接口编程，而不是针对实现编程。}}
+ 组合：{{c1:: 多用组合，少用继承。}}

## 策略模式 [	](designpattern_20201202040742359)

### 策略设计模式的定义与结构 [	](designpattern_20201202040742361)
+ 策略模式的定义：{{c1:: 定义一系列的算法,把它们一个个封装起来, 并且使它们可相互替换。 }}
+ 结构图：{{c1:: ![策略设计模式的结构](https://gitee.com/xieyun714/nodeimage/raw/master/img/structure.png) }}
+ Duck实例设计:{{c1::  ![M9qmQrgLOV](https://gitee.com/xieyun714/nodeimage/raw/master/img/M9qmQrgLOV.jpg)}}


### 策略模式练习题 [	](designpattern_20201202040742364)
+ 要求：将下面动作冒险游戏中的类，根据策略模式组织起来，游戏角色的类和角色可以使用的武器行为的类。毎个角色一次只能使用一种武器
但是可以在游戏的过程中换武器。
+ 习题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201128235318.png)
+ 答案：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201128235348.png) }}

## 观察者模式 [	](designpattern_20201202040742366)

### 观察者模式的定义与结构 [	](designpattern_20201202040742369)
+ 定义:{{c1:: 观察者模式定义了对象之间的一对多依赖，这样一来，当一个对象改变状态时，它的所有依赖者都会收到通知并自动更新。 }}
+ 结构图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201129003828.png) }}
+ 气象站实例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201129003910.png)}}

### java.util.Observable的setChanged()方法作用？  [	](designpattern_20201202040742371)

+ 解释: {{c1:: 如果没有setChanged()方法，我们的气象站测量是如此敏锐， 以致于温度计读数每十分之一度就 会更新，这会造成WeatherData对象持续不断地通知观察者，我们并不希望看到这样的事情发生。 }}
+ `clearChanged()`方法:{{c1:: 将changed状态设置回false。 }}
+ `hasChanged()`方法:{{c1:: 告诉你changed标志的当前状态。 }}

### java.util.Observable的缺陷 [	](designpattern_20201202040742375)

- 是一个类:{{c1:: Observable是一个类:不是接口, 违反了面向接口编程原则,且java也没有多继承. }}
- 具有`protected`方法:{{c1:: Observable将关键的方法保护`protected`起来:会导致只有子类能使用 }}


### test [	](designpattern_20201202040742377)