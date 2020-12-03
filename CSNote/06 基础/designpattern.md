## 设计原则 [	](designpattern_20201203022249287)

### 单一职责原则 [	](designpattern_20200629095419186)

**SRP**：{{c1:: Single Responsibility Principle }}

注意：我们应当遵守单一职责原则，只有逻辑足够简单，才可以在代码级违反单一职责原则；只有类中方法数量足够少，可以在方法级别保持单一职责原则

### 接口隔离原则 [	](designpattern_20200629095419187)

**ISP**：**Interface  Segregation Principle**

反例图：{{c1:: ![image-20200629211404990](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629211404990.png) }}

改进后接口隔离原则例图：{{c1::![image-20200629210906436](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629210906436.png)}}

### 依赖倒置原则 [	](designpattern_20200629095419189)

+ 定义：
    1. {{c1:: 上层模块不应该依赖底层模块，它们都应该依赖于抽象。}}
    2. {{c1:: 抽象不应该依赖于细节，细节应该依赖于抽象。}}
+ 披萨店例子：
    + 反例图：{{c1:: ![image-20200629212530571](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629212530571.png)}}
    + 改进后依赖倒转原则图：{{c1:: ![image-20200629212538616](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629212538616.png)}}

### 避免在OO设计中违反依赖倒置原则建议： [	](designpattern_20201203022249290)

+ 变量不可以持有具体类的引用: {{c1:: 如果使用new，就会持有具体类的引用。你可以改用工厂来避开样的做法。 }}
+ 不要让类派生自具体类:{{c1:: 如果派生自具体类，你就会依赖具体类。请派生自一个抽象（接口或抽类）。 }}
+ 不要覆盖基类中已实现的方法:{{c1:: 如果覆盖基类已实现的方法。，那么你的类就不是一个真正道合被继承的抽象。基类中已实现的方法，应由所有的子类共享 }}
+ 注意:{{c1:: 应该尽量达到这些原则，也不是一定死守规矩 }}

# FirstHead设计模式 [	](designpattern_20201202040742352)

### 设计模式的目的 [	](designpattern_20200629095419184)

- 代码重用性:{{c1::  (即：相同功能的代码，不用多次编写)  }}
- 可读性 :{{c1:: (即：编程规范性, 便于其他程序员的阅读和理解) }}
- 可扩展性:{{c1::  (即：当需要增加新的功能时，非常的方便，称为可维护) }}
- 可靠性 :{{c1:: (即：当我们增加新的功能后，对原来的功能没有影响) }}
- 使程序呈现{{c1:: 高内聚，低耦合 }}的特性 

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

## 装饰者模式 [	](designpattern_20201203022249293)
### 装饰模式:UML结构图 [	](designpattern_20201203022249295)
+ 严格版本:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201202215634.png) }}
+ first head版本：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201202215348.png) }}

### 装饰模式:加密和压缩装饰的示例 [	](designpattern_20201203022249297)
+ 程序使用一对装饰来封装数据源对象。 这两个封装器都改变了从磁盘读写数据的方式：
  + 当数据即将被**写入磁盘**前， 装饰对数据进行加密和压缩。 在原始类对改变毫无察觉的情况下， 将加密后的受保护数据写入文件。
  + 当数据刚从**磁盘读出**后， 同样通过装饰对数据进行解压和解密。 装饰和数据源类实现同一接口， 从而能在客户端代码中相互替换。
+ UML结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201202220046.png) }}

### java.io中的装饰者模式 [	](designpattern_20201203022249299)
+ 图示：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203021457.png)
+ 自定义IO装饰器,把输入流内的所有大写字符转成小写：
  ```java
    //{{c1::
    public class LowerCaseInputStream extends FilterInputStream {
        public LowerCaseInputStream(InputStream in) {
            super(in);
        }
        public int read() throws IOException {
            int c = in.read();
            return (c == -1 ? c : Character.toLowerCase((char)c));
        }
        public int read(byte[] b, int offset, int len) throws IOException {
            int result = in.read(b, offset, len);
            for (int i = offset; i < offset+result; i++) {
                b[i] = (byte)Character.toLowerCase((char)b[i]);
            }
            return result;
        }
    }
   //}}
  ```
### 装饰模式优缺点 [	](designpattern_20201203022249302)
+ 优点：
  + **无需新子类**：{{c1:: 无需创建新子类即可扩展对象的行为。 }}
  + **运行时增删**：{{c1:: 可以在运行时添加或删除对象的功能。 }}
  + **组合几种行为**：{{c1:: 多个装饰封装对象来组合几种行为。 }}
  + **单一职责原则**：{{c1:: 你可以将实现了许多不同行为的一个大类拆分为多个较小的类。 }}
+ 缺点：
  + **删除特定封装器**:{{c1:: 在封装器栈中删除特定封装器比较困难。 }}
  + **栈顺序影响**:{{c1:: 实现行为不受装饰栈顺序影响的装饰比较困难。 }}
  + **初始化配置**:{{c1:: 各层的初始化配置代码看上去可能会很糟糕。 }}

## 工厂方法模式 [	](designpattern_20201203022249304)
### 工厂方法模式定义与结构： [	](designpattern_20201203022249306)
+ 定义：{{c1:: 工厂方法模式是一种创建型设计模式，其在父类中提供一个创建对象的方法，允许子类决定实例化对象的类型。 }}
+ 结构：
  + 正式版：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203010112.png) }}
  + 伪代码版：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203010542.png) }}
### 工厂方法模式：问题引出 [	](designpattern_20201203022249308)
+ 如何将父类中具体对象类型与父类解耦
+ 问题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203011641.png)
+ 工厂方法模式解决方法：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203011927.png) }}

### 工厂方法模式优缺点 [	](designpattern_20201203022249311)
+ 优点
  + **避免耦合**:{{c1:: 可以避免创建者和具体产品之间的紧密耦合。}}
  + **单一职责原则**:{{c1:: 可以将产品创建代码放在程序的单一位置， 从而使得代码更容易维护。}}
  + **开闭原则**:{{c1:: 无需更改现有客户端代码，你就可以在程序中引入新的产品类型。}}
+ 缺点：
  + **复杂性**:{{c1:: 应用工厂方法模式需要引入许多新的子类，代码可能会因此变得更复杂。最好的情况是将该模式引入创建者类的现有层次结构中。 }}

## 抽象工厂模式 [	](designpattern_20201203022249314)
### 抽象工厂模式：问题引出 [	](designpattern_20201203022249317)
+ ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203013548.png)
+ 要求：你不希望在添加新产品或新风格时修改已有代码。
+ 解决方案：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203013645.png)}}
### 抽象工厂模式：定义与结构： [	](designpattern_20201203022249320)
+ 定义：抽象工厂模式提供一个接口，用于创建相关或相互依赖对象的家族，而不需要明确指定具体类。
+ 结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203013705.png) }}

### 抽象工厂模式：具体示例（理解） [	](designpattern_20201203022249324)
+ 披萨订购问题结构： ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203014323.png) 
+ 跨平台UI类示例： ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203015039.png)
+ 理解：{{c1:: 标签 }}
### 抽象工厂模式优缺点 [	](designpattern_20201203022249326)
+ 优点：
  + **产品相互匹配**: {{c1:: 你可以确保同一工厂生成的产品相互匹配。 }}
  + **解耦合**: {{c1:: 你可以避免客户端和具体产品代码的耦合。 }}
  + **单一职责原则**: {{c1:: 你可以将产品生成代码抽取到同一位置， 使得代码易于维护。 }}
  + **开闭原则**: {{c1:: 向应用程序中引入新产品变体时， 你无需修改客户端代码。 }}
+ 缺点：
  + **复杂性增加**: {{c1::由于采用该模式需要向应用中引入众多接口和类， 代码可能会比之前更加复杂。 }}

### test [	](designpattern_20201202040742377)