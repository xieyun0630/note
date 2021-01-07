## 面向对象三大特性 [ ](designpattern_20201227010951560)

### 封装 [ ](designpattern_20201227010951562)
+ 概念：{{c1:: 利用**抽象数据类型**将数据和基于数据的操作封装在一起，使其构成一个**不可分割的独立实体**。数据被保护在抽象数据类型的内部，尽可能地隐藏内部的细节，只保留一些对外的接口使其与外部发生联系。用户无需关心对象内部的细节，但可以通过对象对外提供的接口来访问该对象。 }}

### 继承 [ ](designpattern_20201227010951564)
+ `IS-A`:{{c1:: 继承实现了IS-A关系，例如Cat和Animal就是一种IS-A关系，因此Cat可以继承自Animal，从而获得Animal非private的属性和方法。 }}
+ 遵循原则:{{c1:: 继承应该遵循里氏替换原则，子类对象必须能够替换掉所有父类对象。 }}
+ **向上转型**:{{c1:: Cat可以当做Animal来使用，也就是说可以使用Animal引用Cat对象。父类引用指向子类对象称为向上转型。}}

### 多态 [ ](designpattern_20201227010951567)
+ 定义：{{c1:: 同一类族的对象，接受相同的消息可以展现不同的处理。 }}
+ 多态分为编译时多态和运行时多态：
  - **编译时多态**:{{c1:: 主要指方法的重载 }}
  - **运行时多态**:{{c1:: 指程序中定义的对象引用所指向的具体类型在运行期间才确定 }}
+ 运行时多态有三个条件：
  1. {{c1:: 继承 }}
  2. {{c1:: 覆盖（重写） }}
  3. {{c1:: 向上转型 }}


## UML [ ](designpattern_20201209125527586)

### 3种类之间的关系 [ ](designpattern_20201227010951570)

- `is-a`关系:{{c1:: 也叫继承或泛化 }}
- `has-a`关系:{{c1:: 通常称之为关联（组合，聚合） }}
- `use-a`关系:{{c1:: 通常称之为依赖 }}

### 类图的6大关系 [ ](designpattern_20201209125527589)
1. 依赖关系:{{c1::  (Dependency)**类中用到了对方**，那么他们之间就存在依赖关系。 }}
2. 泛化关系:{{c1:: (Generalization) 实际上就是继承关系，他是**依赖关系的特例** }}
3. 实现关系:{{c1:: (Realization)实际上就是A类实现B接口，他是**依赖关系的特例** }}
4. 关联关系：{{c1:: (Association)类与类之间的联系，他是**依赖关系的特例** }}
  + 具有导航性:{{c1:: 即双向关系或单向关系 }}
  + 具有多重性:{{c1:: 如`n...m` }}
5. 组合关系：{{c1::`Composition`,整体"拥有"部分"的生命,是**关联关系的特例**}}
6. 聚合关系：{{c1::`Aggregation`,整体"有管理"部分"的特有的职责,是**关联关系的特例**}}

+ 总结：{{c1:: 6大关系实际上都是依赖，只是具体细分了另外5种 }}

## 设计原则 [ ](designpattern_20201224091851209)

### 设计模式的作用 [ ](designpattern_20200629095419184)

- 代码重用性:{{c1::  (即：相同功能的代码，不用多次编写)  }}
- 可读性 :{{c1:: (即：编程规范性, 便于其他程序员的阅读和理解) }}
- 可扩展性:{{c1::  (即：当需要增加新的功能时，非常的方便，称为可维护) }}
- 可靠性 :{{c1:: (即：当我们增加新的功能后，对原来的功能没有影响) }}
- 使程序呈现{{c1:: 高内聚，低耦合 }}的特性 

### S.O.L.I.D原则 [ ](designpattern_20201224091851215)

| 简写 |                全拼                 |   中文翻译   |
| :--: | :---------------------------------: | :----------: |
| SRP  | {{c1:: `The Single Responsibility Principle`}} | {{c1:: `单一责任原则`}} |
| OCP  |      {{c1:: `The Open Closed Principle`}}      | {{c1:: `开放封闭原则`}} |
| LSP  |  {{c1:: `The Liskov Substitution Principle`}}  | {{c1:: `里氏替换原则`}} |
| ISP  | {{c1:: `The Interface Segregation Principle`}} | {{c1:: `接口分离原则`}} |
| DIP  | {{c1:: `The Dependency Inversion Principle`}}  | {{c1:: `依赖倒置原则`}} |

### 单一责任原则 [ ](designpattern_20201224091851219)

> **intent**: {{c1:: 修改一个类的原因应该只有一个。 换句话说就是让一个类只负责一件事，当这个类需要做过多事情的时候，就需要分解这个类。}}

### 开放封闭原则 [ ](designpattern_20201224091851222)

> **intent**: {{c1:: 类应该对扩展开放，对修改关闭。 }}

+ **扩展**:{{c1:: 就是添加新功能的意思，因此该原则要求在添加新功能时不需要修改代码。 }}

+ 相应模式：{{c1:: 符合开闭原则最典型的设计模式是装饰者模式，它可以动态地将责任附加到对象上，而不用去修改类的代码。 }}

### 里氏替换原则 [ ](designpattern_20201224091851225)

> **intent**: {{c1:: 子类对象必须能够替换掉所有父类对象。 }}

+ `IS-A`:{{c1:: 继承是一种 IS-A 关系，子类需要能够当成父类来使用，并且需要比父类更特殊。 }}


### 接口分离原则 [ ](designpattern_20201224091851229)

> **intent**: {{c1:: 不应该强迫客户依赖于它们不用的方法。因此使用多个专门的接口比使用单一的总接口要好。 }}

+ 反例图：{{c1:: ![image-20200629211404990](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629211404990.png) }}
+ 改进后接口隔离原则例图：{{c1::![image-20200629210906436](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629210906436.png)}}

### 依赖倒置原则 [ ](designpattern_20201224091851231)

> **intent**: {{c1:: 高层模块不应该依赖于低层模块，二者都应该依赖于抽象；抽象不应该依赖于细节，细节应该依赖于抽象。 }}
+ 避免在OO设计中违反依赖倒置原则建议：
  + 变量不可以持有具体类的引用: {{c1:: 如果使用new，就会持有具体类的引用。你可以改用工厂来避开样的做法。 }}
  + 不要让类派生自具体类:{{c1:: 如果派生自具体类，你就会依赖具体类。请派生自一个抽象（接口或抽类）。 }}
  + 不要覆盖基类中已实现的方法:{{c1:: 如果覆盖基类已实现的方法。，那么你的类就不是一个真正道合被继承的抽象。基类中已实现的方法，应由所有的子类共享 }}
  + 注意:{{c1:: 应该尽量达到这些原则，也不是一定死守规矩 }}
+ 披萨店例子：
  + 反例图：{{c1:: ![image-20200629212530571](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629212530571.png)}}
  + 改进后依赖倒转原则图：{{c1:: ![image-20200629212538616](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629212538616.png)}}

### S.O.L.I.D原则外，常见其他原则 [ ](designpattern_20201224091851234)

| 简写 |               全拼                | 中文翻译     |
| :--: | :-------------------------------: | :----------- |
| LOD  |        {{c1:: `The Law of Demeter`}}         | {{c1:: `迪米特法则` }} |
| CRP  |   {{c1:: `The Composite Reuse Principle`}}   | {{c1:: `合成复用原则` }} |
| CCP  |   {{c1:: `The Common Closure Principle`}}    | {{c1:: `共同封闭原则` }} |
| SAP  | {{c1:: `The Stable Abstractions Principle`}} | {{c1:: `稳定抽象原则` }} |
| SDP  | {{c1:: `The Stable Dependencies Principle`}} | {{c1:: `稳定依赖原则` }} |

###  迪米特法则 [ ](designpattern_20201224091851237)

+ **intent**:{{c1:: 迪米特法则又叫作最少知识原则（Least Knowledge Principle，简写 LKP），就是说一个对象应当对其他对象有尽可能少的了解，不和陌生人说话。 }}
+ 在对象的方法内，只应该调用以下范围的方法
  + {{c1:: 该对象本身的方法 }}
  + {{c1:: 被当做方法的参数而传递进来的对象 }}
  + {{c1:: 此方法所创建或实例化的任何对象 }}
    + 注意：{{c1:: 以上建议代表不要调用从其他方法返回对象的方法 }}
  + {{c1:: 对象的任何组件（HAS-A） }}
+ 应用例子：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201210001408498.png) }}
+ 别称：{{c1:: 迪米特法则（Law of Demeter） }}

### 合成复用原则 [ ](designpattern_20201224091851239)

- **intent**:{{c1:: 尽量使用对象组合，而不是通过继承来达到复用的目的。 }}


### 共同封闭原则 [ ](designpattern_20201224091851242)

- **intent**:{{c1:: 一起修改的类，应该组合在一起（同一个包里）。如果必须修改应用程序里的代码，我们希望所有的修改都发生在一个包里（修改关闭），而不是遍布在很多包里。}}

### 稳定抽象原则 [ ](designpattern_20201224091851244)

- **intent**:{{c1:: 最稳定的包应该是最抽象的包，不稳定的包应该是具体的包，即包的抽象程度跟它的稳定性成正比。}}

### 稳定依赖原则 [ ](designpattern_20201224091851247)

- **intent**:{{c1:: 包之间的依赖关系都应该是稳定方向依赖的，包要依赖的包要比自己更具有稳定性。 }}

# 模式 [ ](designpattern_20201224091851250)

## 策略模式 [ ](designpattern_20201202040742359)

### 策略设计模式的定义与结构 [ ](designpattern_20201202040742361)

+ 策略模式的定义：{{c1:: 定义一系列的算法,把它们一个个封装起来, 并且使它们可相互替换。 }}
+ 结构图：{{c1:: ![策略设计模式的结构](https://gitee.com/xieyun714/nodeimage/raw/master/img/structure.png) }}
+ Duck实例设计:{{c1::  ![M9qmQrgLOV](https://gitee.com/xieyun714/nodeimage/raw/master/img/M9qmQrgLOV.jpg)}}


### 策略模式练习题 [ ](designpattern_20201202040742364)

+ 要求：将下面动作冒险游戏中的类，根据策略模式组织起来，游戏角色的类和角色可以使用的武器行为的类。毎个角色一次只能使用一种武器
  但是可以在游戏的过程中换武器。
+ 习题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201128235318.png)
+ 答案：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201128235348.png) }}

## 观察者模式 [ ](designpattern_20201202040742366)

### 观察者模式的定义与结构 [ ](designpattern_20201202040742369)

+ 定义:{{c1:: 观察者模式定义了对象之间的一对多依赖，这样一来，当一个对象改变状态时，它的所有依赖者都会收到通知并自动更新。 }}
+ 结构图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201129003828.png) }}
+ 正式版:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203164626.png) }}
+ 气象站实例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201129003910.png)}}

### java.util.Observable的setChanged()方法作用？  [ ](designpattern_20201202040742371)

+ 解释: {{c1:: 如果没有setChanged()方法，我们的气象站测量是如此敏锐，以致于温度计读数每十分之一度就会更新，这会造成WeatherData对象持续不断地通知观察者，我们并不希望看到这样的事情发生。 }}
+ `clearChanged()`方法:{{c1:: 将changed状态设置回false。 }}
+ `hasChanged()`方法:{{c1:: 告诉你changed标志的当前状态。 }}

### java.util.Observable的缺陷 [ ](designpattern_20201202040742375)

- 是一个类:{{c1:: Observable是一个类:不是接口, 违反了面向接口编程原则,且java也没有多继承. }}
- 具有`protected`方法:{{c1:: Observable将关键的方法保护`protected`起来:会导致只有子类能使用 }}

## 装饰者模式 [ ](designpattern_20201203022249293)

### 装饰模式:UML结构图 [ ](designpattern_20201203022249295)
+ 定义：{{c1:: 通过将对象放入包含行为的特殊封装对象,动态地给一个对象添加一些额外的职责 }}
+ 严格版本:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201202215634.png) }}
+ first head版本：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201202215348.png) }}

### 装饰模式:加密和压缩装饰的示例 [ ](designpattern_20201203022249297)

+ 程序使用一对装饰来封装数据源对象。 这两个封装器都改变了从磁盘读写数据的方式：
  + 当数据即将被**写入磁盘**前， 装饰对数据进行加密和压缩。 在原始类对改变毫无察觉的情况下， 将加密后的受保护数据写入文件。
  + 当数据刚从**磁盘读出**后， 同样通过装饰对数据进行解压和解密。 装饰和数据源类实现同一接口， 从而能在客户端代码中相互替换。
+ UML结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201202220046.png) }}

### java.io中的装饰者模式 [ ](designpattern_20201203022249299)

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

### 装饰模式优缺点 [ ](designpattern_20201203022249302)

+ 优点：
  + **无需新子类**：{{c1:: 无需创建新子类即可扩展对象的行为。 }}
  + **运行时增删**：{{c1:: 可以在运行时添加或删除对象的功能。 }}
  + **组合几种行为**：{{c1:: 多个装饰封装对象来组合几种行为。 }}
  + **单一职责原则**：{{c1:: 你可以将实现了许多不同行为的一个大类拆分为多个较小的类。 }}
+ 缺点：
  + **删除特定封装器**:{{c1:: 在封装器栈中删除特定封装器比较困难。 }}
  + **栈顺序影响**:{{c1:: 实现行为不受装饰栈顺序影响的装饰比较困难。 }}
  + **初始化配置**:{{c1:: 各层的初始化配置代码看上去可能会很糟糕。 }}

## 工厂模式 [ ](designpattern_20201209125527591)

### 简单工厂模式 [ ](designpattern_20201209125527593)

+ 结构：![image-20201208234527736](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201208234527736.png)
+ 示例：

```java
//{{c1::
public class SimpleFactory {
  public Pizza createPizza(String orderType) {
    Pizza pizza = null;
    System.out.println("使用简单工厂模式");
    if (orderType.equals("greek")) {
      pizza = new GreekPizza();
      pizza.setName(" 希腊披萨 ");
    } else if (orderType.equals("cheese")) {
      pizza = new CheesePizza();
      pizza.setName(" 奶酪披萨 ");
    } else if (orderType.equals("pepper")) {
      pizza = new PepperPizza();
      pizza.setName("胡椒披萨");
    }
    return pizza;
  }
  
  public static Pizza createPizza2(String orderType) {
    //... 与前面相同
  }
}
//}}
```



### 工厂方法模式定义与结构： [ ](designpattern_20201203022249306)

+ 定义：{{c1:: 工厂方法模式是一种创建型设计模式，其在父类中提供一个创建对象的方法，允许子类决定实例化对象的类型。 }}
+ 结构：
  + 正式版：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203010112.png) }}
  + 伪代码版：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203010542.png) }}

### 工厂方法模式：问题引出 [ ](designpattern_20201203022249308)

+ 如何将父类中具体对象类型与父类解耦
+ 问题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203011641.png)
+ 工厂方法模式解决方法：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203011927.png) }}

### 工厂方法模式优缺点 [ ](designpattern_20201203022249311)

+ 优点
  + **避免耦合**:{{c1:: 可以避免创建者和具体产品之间的紧密耦合。}}
  + **单一职责原则**:{{c1:: 可以将产品创建代码放在程序的单一位置， 从而使得代码更容易维护。}}
  + **开闭原则**:{{c1:: 无需更改现有客户端代码，你就可以在程序中引入新的产品类型。}}
+ 缺点：
  + **复杂性**:{{c1:: 应用工厂方法模式需要引入许多新的子类，代码可能会因此变得更复杂。最好的情况是将该模式引入创建者类的现有层次结构中。 }}

### 抽象工厂模式：问题引出 [ ](designpattern_20201203022249317)

+ ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203013548.png)
+ 要求：你不希望在添加新产品或新风格时修改已有代码。
+ 解决方案：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203013645.png)}}

### 抽象工厂模式：定义与结构 [	](designpattern_20201203022249320)

+ 定义：{{c1:: 提供一个接口，用于创建相关或相互依赖对象的家族，而不需要明确指定具体类。 }}
+ 结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203013705.png) }}

### 抽象工厂模式：具体示例（理解） [ ](designpattern_20201203022249324)

+ 披萨订购问题结构： ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203014323.png) 
+ 跨平台UI类示例： ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203015039.png)
+ 理解：{{c1:: 标签 }}

### 抽象工厂模式优缺点 [ ](designpattern_20201203022249326)

+ 优点：
  + **产品相互匹配**: {{c1:: 你可以确保同一工厂生成的产品相互匹配。 }}
  + **解耦合**: {{c1:: 你可以避免客户端和具体产品代码的耦合。 }}
  + **单一职责原则**: {{c1:: 你可以将产品生成代码抽取到同一位置， 使得代码易于维护。 }}
  + **开闭原则**: {{c1:: 向应用程序中引入新产品变体时， 你无需修改客户端代码。 }}
+ 缺点：
  + **复杂性增加**: {{c1::由于采用该模式需要向应用中引入众多接口和类， 代码可能会比之前更加复杂。 }}

## 单例模式 [ ](designpattern_20201209125527596)

### 单例模式定义与结构 [ ](designpattern_20201209125527599)

+ 单例模式定义：{{c1:: 单件模式确保一个类只有一个实例，并提供一个全局访问点。 }}
+ 结构：{{c1:: ![单例模式结构](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201208202027.png) }}
+ 2个必要注意点：
  1. {{c1:: 单例的**构造函数**必须对客户端（Client）代码隐藏。 }}
  2. {{c1:: 调用**获取实例方法**必须是获取单例对象的唯一方式。}}
+ JDK中`Runtime`例:{{c1:: JDK中，java.lang.Runtime就是经典的单例模式(饿汉式) }}

### java的8种单例模式实现方法 [ ](designpattern_20201209125527602)

1. 饿汉
   1. {{c1:: **饿汉式（静态常量）** }}
   2. {{c1:: **饿汉式（静态代码块）** }}
2. 懒汉
   1. {{c1:: 懒汉式（线程不安全） }}
   2. {{c1:: 懒汉式（线程安全，同步方法） }}
   3. {{c1:: 懒汉式（线程安全，同步代码块） }}
3. {{c1:: **双重检查** }}
4. {{c1:: **静态内部类** }}
5. {{c1:: **枚举** }}

+ 注意：{{c1:: 推荐使用与不推荐使用 }}

### 单例模式:饿汉式实现 [ ](designpattern_20201209125527604)

+ 实现

  ```java
  //{{c1::
  class Singleton {
    //1. 构造器私有化, 外部能new
    private Singleton() {
      
    }
    //2.本类内部创建对象实例
    private final static Singleton instance = new Singleton();
    //3. 提供一个公有的静态方法，返回实例对象
    public static Singleton getInstance() {
      return instance;
    }
  }
  //}}
  ```

+ 优点：{{c1:: 简单，在类装载的时候就完成实例化。避免了线程同 }}
  步问题。

+ 缺点：{{c1:: 在类装载的时候就完成实例化，没有达到`Lazy Loading`的效果。 }}

+ 使用结论：{{c1:: 这种单例模式可用，可能造成内存浪费 }}

### 单例模式:懒汉式（线程不安全）实现 [ ](designpattern_20201209125527606)

+ 线程不安全懒汉式：

  + 实现：

    ```java
    //{{c1::
    class Singleton {
      private static Singleton instance;
      private Singleton() {}
      public static Singleton getInstance() {
        if(instance == null) {
          instance = new Singleton();
        }
        return instance;
      }
    }
    //}}
    ```

  + 优点: {{c1:: `Lazy Loading` }}

  + 缺点: {{c1:: **线程不安全**，如果2个线程同时进入了`if (singleton == null)`判断语句块,会导致**多实例** }}

  + 结论: {{c1:: 在实际开发中，不要使用这种方式. }}

+ 懒汉式(同步方法)

  + 实现：

  ```java
  //{{c1::
  class Singleton {
    private static Singleton instance;
    private Singleton() {}
    //提供一个静态的公有方法，加入同步处理的代码，解决线程安全问题
    //即懒汉式
    public static synchronized Singleton getInstance() {
      if(instance == null) {
        instance = new Singleton();
      }
      return instance;
    }
  }
  //}}
  ```

  + 优点: {{c1:: 解决了线程不安全问题 }}
  + 缺点: {{c1:: **效率低**，每个线程在想获得类的实例时候，执行`getInstance()`方法都要进行同步。而其实这个方法只执行一次实例化代码就够了，后面的想获得该类实例，直接`return`就行了。方法进行同步效率太低 }}
  + 结论: {{c1:: 在实际开发中，不推荐这种方式. }}

+ 懒汉式(同步代码块)

  + 实现：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201208210823.png)
  + 注意：不能使用这种方式，这种同步并不能起到线程同步的作用，假如两个线程**同时**进入了`if (singleton == null)`判断语句块，这时便会产生多个实例

### 单例模式：双重检查（Double-Check)实现 [ ](designpattern_20201209125527609)

```java
//{{c1::
class Singleton {
  private static volatile Singleton instance;
    private Singleton() {}
    public static synchronized Singleton getInstance() {
        if(instance == null) {
          synchronized (Singleton.class) {
            if(instance == null) {
              instance = new Singleton();
            }
          }
        }
      return instance;
    }
}
//}}
```

+ 特点：{{c1::线程安全,懒加载,保证了效率,推荐使用}}

### 单例模式：静态内部类实现 [ ](designpattern_20201209125527611)

```java
//{{c1::
class Singleton {
  private static volatile Singleton instance;
  private Singleton() {}
  private static class SingletonInstance {
    private static final Singleton INSTANCE = new Singleton(); 
  }
  public static synchronized Singleton getInstance() {
    return SingletonInstance.INSTANCE;
  }
}
//}}
```
+ 特点：{{c1:: 懒加载，线程安全，推荐使用 }}
+ 为什么线程安全？
  + {{c1:: 采用了类装载的机制来保证初始化实例时只有一个线程。 }}
  + {{c1:: 静态内部类方式在Singleton类被装载时并不会立即实例化，而是在需要实例化时，调用getInstance方法，才会装载SingletonInstance类，从而完成Singleton的实例化。 }}

### 单例模式：使用枚举实现 [ ](designpattern_20201209125527614)

```java
//{{c1::
  enum Singleton {
    INSTANCE; //属性
    public void sayOK() {
      System.out.println("ok~");
    }
  } 
//}}
``` 
+ 特点：{{c1:: 线程同步，防止反序列破环单例，推荐使用 }}
+ 反序列化的作用：{{c1:: 根据字节流中保存的对象状态及描述信息，通过反序列化重建对象。 }}

### 单例模式使用的场景举例 [ ](designpattern_20201209125527616)

+ {{c1:: 需要频繁的进行创建和销毁的对象 }}
+ {{c1:: 创建对象时耗时过多或耗费资源过多(即：重量级对象)，但又经常用到的对象、工具类对象 }}
+ {{c1:: 频繁访问数据库或文件的对象(比如数据源、session工厂等) }}

## 命令模式 [ ](designpattern_20201209125527619)

### 命令模式：问题引出 [ ](designpattern_20201209125527622)

+ 需求:开发一款新的文字编辑器， 当前的任务是创建一个包含多个按钮的工具栏， 并让每个按钮对应编辑器的不同操作。
+ 示意图：![image-20201209003259063](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201209003259063.png)
+ 问题：如过需要快捷键替代按钮的功能，这时就不得不多复制一份按钮中对应功能的代码。
+ 解决：{{c1:: ![image-20201209003618359](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201209003618359.png) }}
  + {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201209003956.png) }}

### 命令模式定义与结构 [ ](designpattern_20201209125527624)

+ 定义：{{c1:: 将一个请求封装成一个对象，从而使您可以用不同的请求对客户进行参数化。 }}
+ 主要目的：{{c1:: 使得请求发送者与请求接收者消除彼此之间的耦合 }}
+ 结构图：
  + 正式版:{{c1:: ![命令模式结构](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201209004327.png) }}
  + 详细版:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201209005335.png) }}
+ 抽象命令类（Command）角色： {{c1:: 明执行命令的接口，拥有执行命令的抽象方法 execute()。 }}
+ 具体命令类（Concrete Command）角色： {{c1:: 抽象命令类的具体实现类，它拥有接收者对象，并通过调用接收者的功能来完成命令要执行的操作。 }}
+ 实现者/接收者（Receiver）角色： {{c1:: 执行与请求相关的操作，**真正执行命令的对象** }}
+ 调用者/请求者（Invoker）角色： {{c1:: **请求的发送者**，它通常拥有很多的命令对象，并通过访问命令对象来执行相关请求，它不直接访问接收者。 }}

### 命令模式：智能生活案例  [	](designpattern_20201224024146375)

+ 需求：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201209214512.png)

+ 结构图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201209195911.png) }}

+ Client代码实现：

  ```java
  //{{c1::
      //使用命令设计模式，完成通过遥控器，对电灯的操作
      //创建电灯的对象(接受者)
      LightReceiver lightReceiver = new LightReceiver();
      //创建电灯相关的开关命令
      LightOnCommand lightOnCommand = new LightOnCommand(lightReceiver);
      LightOffCommand lightOffCommand = new LightOffCommand(lightReceiver);
      //需要一个遥控器
      RemoteController remoteController = new RemoteController();
      //给我们的遥控器设置命令, 比如 no = 0 是电灯的开和关的操作
      remoteController.setCommand(0, lightOnCommand, lightOffCommand);
      System.out.println("--------按下灯的开按钮-----------");
      remoteController.onButtonWasPushed(0);
      System.out.println("--------按下灯的关按钮-----------");
      remoteController.offButtonWasPushed(0);
      System.out.println("--------按下撤销按钮-----------");
      remoteController.undoButtonWasPushed();
  //}}
  ```

### 命令模式：宏命令  [	](designpattern_20201224024146377)

+ 定义：

  ```java
  //{{c1::
    public class MacroCommand implements Command {
      Command[] commands;
    
      public MacroCommand(Command[] commands) {
        this.commands = commands;
      }
      public void execute() {
        for (int i = 0; i < commands.length; i++) {
          commands[i].execute();
        }
      }
      public void undo() {
        for (int i = commands.length -1; i >= 0; i--) {
          commands[i].undo();
        }
      }
    }
  //}}
  ```

+ 简单使用

  ```java
  //{{c1::
      LightOnCommand lightOn = new LightOnCommand(light);
      StereoOnCommand stereoOn = new StereoOnCommand(stereo);
      TVOnCommand tvOn = new TVOnCommand(tv);
      HottubOnCommand hottubOn = new HottubOnCommand(hottub);
      LightOffCommand lightOff = new LightOffCommand(light);
      StereoOffCommand stereoOff = new StereoOffCommand(stereo);
      TVOffCommand tvOff = new TVOffCommand(tv);
      HottubOffCommand hottubOff = new HottubOffCommand(hottub);
  
      Command[] partyOn = { lightOn, stereoOn, tvOn, hottubOn};
      Command[] partyOff = { lightOff, stereoOff, tvOff, hottubOff};
    
      MacroCommand partyOnMacro = new MacroCommand(partyOn);
      MacroCommand partyOffMacro = new MacroCommand(partyOff);
  
      remoteControl.setCommand(0, partyOnMacro, partyOffMacro);
  //}}
  ```

## 适配器模式  [	](designpattern_20201224024146379)

### 适配器模式定义与结构  [	](designpattern_20201224024146382)

+ 定义：{{c1:: 适配器模式将一个类的接口，转换成客户期望的另一个接口。主要目是兼容性 }}
+ 对象适配器结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201210003513.png) }}
+ 类适配器结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201210003608.png) }}

### 适配器模式:类适配器  [	](designpattern_20201224024146385)

+ 结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201211063500.png) }}
+ client端实现：
  ```java
  //{{c1::
    System.out.println(" === 类适配器模式 ====");
    Phone phone = new Phone();
    phone.charging(new VoltageAdapter());
  //}}
  ```
+ 缺点： {{c1:: 使用继承，暴露了多余方法 }}

+ 优点: {{c1:: 可以根据需求重写source类的方法 }}

### 适配器模式:对象适配器  [	](designpattern_20201224024146387)

+ 结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201211080620.png) }}
+ 与类适配器的区别：{{c1:: 将继承变成了组合 }}
+ client端实现：
  ```java
  //{{c1::
    System.out.println(" === 对象适配器模式 ====");
    Phone phone = new Phone();
    phone.charging(new VoltageAdapter(new Voltage220V()));
  //}}
  ```

### 适配器模式:接口适配器模式  [	](designpattern_20201224024146389)

+ 作用：{{c1:: 当不需要全部实现接口提供的方法时，可先设计一个抽象类实现接口，并为该接口中每个方法提供一个默认实现（空方法），那么该抽象类的子类可有选择地覆盖父类的某些方法来实现需求 }}
+ 例如：
  ```java
  //{{c1::
  new AnimatorListenerAdapter() {
      @Override
      public void onAnimationStart(Animator animation) {
      //xxxx具体实现
      }
  }
  //}}
  ```

### 适配器模式在SpringMVC框架应用的源码剖析  [	](designpattern_20201224024146392)

+ 代码分析流程：![image-20201211084548546](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201211084548546.png)
+ 动手写SpringMVC通过适配器设计模式获取到对应的Controller的源码![image-20201211085454077](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201211085454077.png)
+ client端实现:
  ```java
    // 此处模拟SpringMVC从request取handler的对象，
    // 适配器可以获取到希望的Controller
     HttpController controller = new HttpController();
    // AnnotationController controller = new AnnotationController();
    //SimpleController controller = new SimpleController();
    // 得到对应适配器
    HandlerAdapter adapter = getHandler(controller);
    // 通过适配器执行对应的controller对应方法
    adapter.handle(controller);
  ```
+ 标签：{{c1:: 理解 }}
+ 库索引：TODO
****

## 外观模式  [	](designpattern_20201224024146395)

### 外观模式定义与结构  [	](designpattern_20201224024146399)

+ 定义：{{c1:: 外观模式提供了一个统一的接口，用来访间子系统中的一群接口。外观定义了一个高层接口，让子系统更容易使用。 }}
+ 结构：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201210005149.png)
+ 亦称：{{c1:: 门面模式、Facade }}

## 模板方法模式 [	](designpattern_20201224024146401)

### 模板方法模式问题引出 [	](designpattern_20201224024146405)

+ 该程序的首个版本仅支持 DOC 文件。 在接下来的一个版本中， 程序能够支持 CSV 文件。 一个月后， 你 “教会” 了程序从 PDF 文件中抽取数据。![image-20201216072408062](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201216072408062.png)

+ 解决：{{c1:: ![image-20201216072930073](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201216072930073.png) }}
+ 注意：
  1. *抽象步骤*必须由各个子类来实现
  2. 步骤已有一些默认实现，但仍可在需要时进行重写

### 模板方法模式定义与结构  [	](designpattern_20201224024146407)

+ 定义：{{c1:: 它在基类中定义了一个算法的框架， 允许子类在不修改结构的情况下重 写算法的特定步骤。 }}
+ 结构：{{c1:: ![image-20201216074321328](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201216074321328.png) }}
+ **钩子方法**：{{c1:: 钩子是一种方法，它在抽象类中不做事，或者只做默认的事情，子类可以选择要不要去覆盖它。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201216082837.png)}}
+ `final`的使用：{{c1:: 为了防止子类改变模板方法中的算法，可以将模板方法声明为 `final` }}

### 模板方法模式与其他模式的关系 [	](designpattern_20201224024146410)

- 与工厂方法模式的关系：{{c1:: 工厂方法模式是**模板方法模式的一种特殊形式**。 同 时， 工厂方法可以作为一个大型模板方法中的一个步骤。 }}
- 与策略模式的关系：
  - **继承与组合**：{{c1::  策略模式和模板方法模式都封装算法，一个用组合，一个用继承。  }}
  - **静态与动态**：{{c1::  模板方法在**类层次**上运作， 因此它是**静态的**。 策略在**对象层次**上运作， 因此允许在**运行时切换行为**。 }}

## 迭代器模式 [	](designpattern_20201224024146412)

### 迭代器模式：问题引出 [	](designpattern_20201224024146415)

+ 问题:如何遍历不同数据结构的集合（树，图，线性表,...)![image-20201217073948248](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201217073948248.png)
+ 解决方案：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201217074027.png) }}

### 迭代器模式定义与结构 [	](designpattern_20201224024146417)

+ 定义: {{c1:: **迭代器模式**是一种行为设计模式， 让你能在不暴露集合底层表现形（列表、 栈和树等） 的情况下遍历集合中所有的元素。}}
+ 结构：{{c1:: ![image-20201217074526389](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201217074526389.png) }}

### 迭代器模式优缺点 [	](designpattern_20201224024146419)

- 优点
  -  **单一职责原则**：{{c1:: 通过将体积庞大的遍历算法代码抽取为独立的类， 你可对客户端代码和集合进行整理。 }}
  -  **开闭原则**：{{c1::  你可实现新型的集合和迭代器并将其传递给现有代码， 无需修改现有代码。 }}
  -  **并行遍历**：{{c1:: 你可以并行遍历同一集合， 因为每个迭代器对象都包含其自身的遍历状态。 }}
  -  **暂停遍历**：{{c1:: 相似的， 你可以暂停遍历并在需要时继续。 }}
- 缺点
  -  **矫枉过正**:{{c1:: 如果你的程序只与简单的集合进行交互，应用该模式可能会矫枉过正。}}
  - **特殊集合效率**:{{c1:: 对于某些特殊集合，使用迭代器可能比直接遍历的效率低。}}

## 组合模式 [	](designpattern_20201224024146421)

### 组合模式的定义与结构 [	](designpattern_20201224024146423)

+ 定义：{{c1:: 可以使用它将对象组合成树状结构，并且能像使用独立对象一样使用它们。 }}
+ 结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201217081946.png) }}
+ 解释：
    1. **组件**：{{c1::（Component）接口描述了树中简单项目和复杂项目所共有的操作。}}
    2. **叶节点**：{{c1::（Leaf）是树的基本结构， 它不包含子项目。}}
    3. **容器**：{{c1::（Composite）是包含叶节点或其他容器等子项目的单位。}}
    4. **客户端**：{{c1::（Client）通过组件接口与所有项目交互。}}
## 状态模式 [	](designpattern_20201224024146425)

### 状态模式：问题引出 [	](designpattern_20201224024146427)

+ 文档对象的几种状态：![![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201222065901.png)](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201222065821.png)
+ 解决方案：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201222065901.png) }}

### 状态模式结构与定义 [	](designpattern_20201224024146429)

+ 定义：{{c1:: 在一个对象的内部状态变化时改变其行为，使其看上去就像改变了自身所属的类一样。 }}
+ 结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201222070539.png) }}
+ 与策略模式的区别在于: {{c1:: 在状态模式中，特定状态知道其他所有状态的存在，且能触发从一个状态到另一个状态的转换；策略则几乎完全不知道其他策略的存在。 }}
### 状态模式优缺点 [	](designpattern_20201224024146432) 
+ 优点：
  -  **单一职责原则**：{{c1:: 将与特定状态相关的代码放在单独的类中。 }}
  -  **开闭原则**：{{c1:: 无需修改已有状态类和上下文就能引入新状态。 }}
  -  **消除臃肿**：{{c1:: 通过消除臃肿的状态机条件语句简化上下文代码。 }}
+ 缺点:
  -  **小题大作**：{{c1:: 如果状态机只有很少的几个状态， 或者很少发生改变， 那么应用该模式可能会显得小题大作。 }}
  -  **会产生很多类**：{{c1:: 每个状态都要一个对应的类，当状态过多时会产生很多类，加大维护难度 }}

## 代理模式 [ ](designpattern_20201224091851336)

### 代理模式定义与结构 [ ](designpattern_20201224091851338)

+ 定义：{{c1:: 为一个对象提供一个替身，以控制对这个对象的访问。即通过代理 对象访问目标对象.这样做的好处是:可以在目标对象实现的基础上,增强额外的 功能操作,即扩展目标对象的功能。 }}
+ 结构：{{c1:: ![image-20201224112429647](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201224112429647.png) }}
- java代理模式的形式：
  1. {{c1:: 静态代理：代理对象与目标对象要实现相同的接口,然后通过调用相同的方法来 调用目标对象的方法。 }}
  2. {{c1:: 动态代理 (JDK代理、接口代理) }}
  3. {{c1:: Cglib代理 (可以在内存动态的创建对象，而不需要实现接口， 属于动态代理的范畴) 。 }}
- 在AOP编程中如何选择代理模式：{{c1:: 目标对象需要实现接口，用JDK代理，目标对象不需要实现接口，用Cglib代理 }}

### 代理模式实现：JDK动态代理  [ ](designpattern_20201224091851341)

+ 主要思路：{{c1:: 代理对象,不需要实现接口，但是**目标对象要实现接口**，否则不能用动态代理。JDK实现代理只需要使用newProxyInstance方法 }}
- 代理对象代码：
```java
//{{c1::
public class ProxyFactory {
  private Object target;
  public ProxyFactory(Object target) {
    this.target = target;
  } 
  //给目标对象生成代理对象
  public Object getProxyInstance() {
    return Proxy.newProxyInstance(target.getClass().getClassLoader(), 
        target.getClass().getInterfaces(), 
        new InvocationHandler() {
          @Override
          public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
            System.out.println("JDK代理开始~~");
            Object returnVal = method.invoke(target, args);
            System.out.println("JDK代理提交");
            return returnVal;
          }
        }); 
  }
}
//}}
```

### 代理模式实现：Cglib代理 [ ](designpattern_20201224091851344)

+ 特点：{{c1:: Cglib代理不要求目标对象实现接口，它是在内存中构建一个子类对象从而实现对目标对象功能扩展，属于动态代理。 }}
+ 代理对象代码：
  ```java
  //{{c1::
  public class ProxyFactory implements MethodInterceptor {
    private Object target;
    public ProxyFactory(Object target) {
      this.target = target;
    }
  
    //返回一个代理对象:是target对象的代理对象
    public Object getProxyInstance() {
      //1. 创建一个工具类
      Enhancer enhancer = new Enhancer();
      //2. 设置父类
      enhancer.setSuperclass(target.getClass());
      //3. 设置回调函数
      enhancer.setCallback(this);
      //4. 创建子类对象，即代理对象
      return enhancer.create();
    }
    
    //重写intercept方法，会调用目标对象的方法
    @Override
    public Object intercept(Object arg0, Method method, Object[] args, MethodProxy arg3) throws Throwable {
      // TODO Auto-generated method stub
      System.out.println("Cglib代理模式 ~~ 开始");
      Object returnVal = method.invoke(target, args);
      System.out.println("Cglib代理模式 ~~ 提交");
      return returnVal;
    }
  }
  //}}
  ```

## 原型模式 [ ](designpattern_20201224091851346)

### 原型模式定义与结构 [ ](designpattern_20201224091851348)

+ 定义：{{c1:: **原型模式**是一种创建型设计模式， 使你能够复制已有对象， 无需知道如何创建的细节。 }}
+ 基本结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201224125546.png) }}

### 原型模式实现：浅拷贝与深拷贝 [ ](designpattern_20201224091851351)
+ 浅拷贝:{{c1:: 拷贝对象和原始对象的引用类型引用同一个对象。 }}
+ 深拷贝:{{c1:: 拷贝对象和原始对象的引用类型引用不同对象。 }}
+ 浅拷贝默认实现：
  ```java
  //{{c1::
  public class Sheep implements Cloneable {
    //省略成员属性
    @Override
    protected Object clone()  {
      Sheep sheep = null;
      try {
        sheep = (Sheep)super.clone();
      } catch (Exception e) {
        System.out.println(e.getMessage());
      }
      return sheep;
    }
  }
  //}}
  ```
-  深拷贝实现方式1：重写clone方法来实现深拷贝 :
  ```java
  //{{c1::
    @Override
    protected Object clone() throws CloneNotSupportedException {
      
      Object deep = null;
      //这里完成对基本数据类型(属性)和String的克隆
      deep = super.clone(); 
      //对引用类型的属性，进行单独处理
      DeepProtoType deepProtoType = (DeepProtoType)deep;
      deepProtoType.deepCloneableTarget  = (DeepCloneableTarget)deepCloneableTarget.clone();
      return deepProtoType;
    }
  //}}
  ```
-  深拷贝实现方式2：通过对象序列化实现深拷贝(推荐):
  ```java
  //{{c1::
    public Object deepClone() {
        //...核心代码如下
        bos = new ByteArrayOutputStream();
        oos = new ObjectOutputStream(bos);
        oos.writeObject(this);

        //反序列化
        bis = new ByteArrayInputStream(bos.toByteArray());
        ois = new ObjectInputStream(bis);
        DeepProtoType copyObj = (DeepProtoType)ois.readObject();
        return copyObj;
    }
  //}}
  ```

## 建造者模式 [ ](designpattern_20201224091851353)

### 建造者模式：问题引出 [ ](designpattern_20201224091851357)

+ 问题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201224152005.png)
另一种方法则无需生成子类。 你可以在 `房屋`基类中创建一个包括所有可能参数的超级构造函数， 并用它来控制房屋对象。 这种方法确实可以避免生成子类， 但它却会造成另外一个问题。
![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201224152827.png)
+ 解决：{{c1:: ![image-20201224153542372](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201224153542372.png)}}

### 建造者模式定义与结构 [ ](designpattern_20201224091851359)

- **Intent**：{{c1::  封装一个对象的构造过程，并允许按步骤构造。 }}
- 结构：{{c1:: ![image-20201224153721243](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201224153721243.png) }}
+ 视频版结构：{{c1:: ![image-20201224181233171](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201224181233171.png) }}

### 建造者模式实现:简易版StringBuilder [ ](designpattern_20201224091851361)

```java
public class AbstractStringBuilder {
    protected char[] value;

    protected int count;

    public AbstractStringBuilder(int capacity) {
        count = 0;
        value = new char[capacity];
    }

    public AbstractStringBuilder append(char c) {
        ensureCapacityInternal(count + 1);
        value[count++] = c;
        return this;
    }

    private void ensureCapacityInternal(int minimumCapacity) {
        // overflow-conscious code
        if (minimumCapacity - value.length > 0)
            expandCapacity(minimumCapacity);
    }

    void expandCapacity(int minimumCapacity) {
        int newCapacity = value.length * 2 + 2;
        if (newCapacity - minimumCapacity < 0)
            newCapacity = minimumCapacity;
        if (newCapacity < 0) {
            if (minimumCapacity < 0) // overflow
                throw new OutOfMemoryError();
            newCapacity = Integer.MAX_VALUE;
        }
        value = Arrays.copyOf(value, newCapacity);
    }
}
```

```java
public class StringBuilder extends AbstractStringBuilder {
    public StringBuilder() {
        super(16);
    }

    @Override
    public String toString() {
        // Create a copy, don't share the array
        return new String(value, 0, count);
    }
}
```

+ 标签：{{c1:: 理解 }}

## 桥接模式 [ ](designpattern_20201227010951572)

### 桥接模式问题引出 [ ](designpattern_20201227010951574)
+ 问题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201225110108.png)
+ 解决：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201225110313.png) }}


### 桥接模式的定义与结构 [ ](designpattern_20201227010951577)
+ intent: {{c1::  可将一个大类或一系列紧密相关的类拆分为**抽象和实现**两个独立的层次结构， 从而能在开发时分别使用。 }}
+ 结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201225112217.png) }}
+ 实例：{{c1:: ![image-20201225140459028](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201225140459028.png) }}

### 桥接模式使用场景参考 [ ](designpattern_20201227010951580)
- **根据维度**： {{c1:: 当一个类存在两个独立变化的维度，且这两个维度都需要进行扩展时。 }}
- **类个数爆炸问题**： {{c1:: 当一个系统不希望使用继承或因为多层次继承导致系统类的个数急剧增加时。 }}
- **避免静态继承关系**： {{c1:: 当一个系统需要在构件的抽象化角色和具体化角色之间增加更多的灵活性时。避免在两个层次之间建立静态的继承联系，通过桥接模式可以使它们在抽象层建立一个关联关系。 }}

## 享元模式 [ ](designpattern_20201227010951582)

### 享元模式定义与实现 [ ](designpattern_20201227010951585)

- intent：运用共享技术来有效地支持大量细粒度对象的复用。它通过**共享已经存在的对象**来大幅度**减少需要创建的对象数量**、避免大量相似对象的开销，从而**提高系统资源的利用率**
- 享元（ Flyweight)模式中存在以下两种状态
  - 内部状态，即不会随着环境的改变而改变的可共享部分。
  - 外部状态，指随环境改变而改变的不可以共享的部分。享元模式的实现要领就是区分应用中的这两种状态，并将外部状态外部化。
- 俄罗斯方块设计结构：![image-20201225142143437](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201225142143437.png)