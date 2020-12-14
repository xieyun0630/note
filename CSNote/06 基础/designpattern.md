## UML [  ](designpattern_20201209125527586) 

### 类图的6大关系 [  ](designpattern_20201209125527589) 

1. 依赖关系:{{c1:: **类中用到了对方**，那么他们之间就存在依赖关系。 }}
2. 泛化关系:{{c1:: 实际上就是继承关系，他是**依赖关系的特例** }}
3. 实现关系:{{c1:: 实际上就是A类实现B接口，他是**依赖关系的特例** }}
4. 关联关系：{{c1:: (Association)类与类之间的联系，他是**依赖关系的特例** }}
  + 具有导航性:{{c1:: 即双向关系或单向关系 }}
  + 具有多重性:{{c1:: 如`n...m` }}
5. 组合关系：{{c1::`Composition`,整体"拥有"部分"的生命,是**关联关系的特例**}}
6. 聚合关系：{{c1::`Aggregation`,整体"有管理"部分"的特有的职责,是**关联关系的特例**}}
+ 总结：{{c1:: 6大关系实际上都是依赖，只是具体细分了另外5种 }}
## 设计原则 [  ](designpattern_20201203022249287) 

### 单一职责原则 [  ](designpattern_20200629095419186) 

**SRP**：{{c1:: Single Responsibility Principle }}

注意：我们应当遵守单一职责原则，只有逻辑足够简单，才可以在代码级违反单一职责原则；只有类中方法数量足够少，可以在方法级别保持单一职责原则

### 接口隔离原则 [  ](designpattern_20200629095419187) 

**ISP**：**Interface  Segregation Principle**

反例图：{{c1:: ![image-20200629211404990](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629211404990.png) }}

改进后接口隔离原则例图：{{c1::![image-20200629210906436](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629210906436.png)}}

### 依赖倒置原则 [  ](designpattern_20200629095419189) 

+ 定义：
    1. {{c1:: 上层模块不应该依赖底层模块，它们都应该依赖于抽象。}}
    2. {{c1:: 抽象不应该依赖于细节，细节应该依赖于抽象。}}
+ 披萨店例子：
    + 反例图：{{c1:: ![image-20200629212530571](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629212530571.png)}}
    + 改进后依赖倒转原则图：{{c1:: ![image-20200629212538616](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200629212538616.png)}}

### 避免在OO设计中违反依赖倒置原则建议： [  ](designpattern_20201203022249290) 

+ 变量不可以持有具体类的引用: {{c1:: 如果使用new，就会持有具体类的引用。你可以改用工厂来避开样的做法。 }}
+ 不要让类派生自具体类:{{c1:: 如果派生自具体类，你就会依赖具体类。请派生自一个抽象（接口或抽类）。 }}
+ 不要覆盖基类中已实现的方法:{{c1:: 如果覆盖基类已实现的方法。，那么你的类就不是一个真正道合被继承的抽象。基类中已实现的方法，应由所有的子类共享 }}
+ 注意:{{c1:: 应该尽量达到这些原则，也不是一定死守规矩 }}

### 设计原则：最少知识原则 
+ 定义：{{c1:: 每个单元对其他单元只拥有有限的知识，只了解与当前单元紧密联系的单元； }}
+ 在对象的方法内，只应该调用以下范围的方法
  + {{c1:: 该对象本身的方法 }}
  + {{c1:: 被当做方法的参数而传递进来的对象 }}
  + {{c1:: 此方法所创建或实例化的任何对象 }}
    + 注意：{{c1:: 以上建议代表不要调用从其他方法返回对象的方法 }}
  + {{c1:: 对象的任何组件（HAS-A） }}
+ 应用例子：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201210001408498.png) }}
+ 别称：{{c1:: 迪米特法则（Law of Demeter） }}

# FirstHead设计模式 [  ](designpattern_20201202040742352) 

### 设计模式的目的 [  ](designpattern_20200629095419184) 

- 代码重用性:{{c1::  (即：相同功能的代码，不用多次编写)  }}
- 可读性 :{{c1:: (即：编程规范性, 便于其他程序员的阅读和理解) }}
- 可扩展性:{{c1::  (即：当需要增加新的功能时，非常的方便，称为可维护) }}
- 可靠性 :{{c1:: (即：当我们增加新的功能后，对原来的功能没有影响) }}
- 使程序呈现{{c1:: 高内聚，低耦合 }}的特性 

## 策略模式 [  ](designpattern_20201202040742359) 

### 策略设计模式的定义与结构 [  ](designpattern_20201202040742361) 
+ 策略模式的定义：{{c1:: 定义一系列的算法,把它们一个个封装起来, 并且使它们可相互替换。 }}
+ 结构图：{{c1:: ![策略设计模式的结构](https://gitee.com/xieyun714/nodeimage/raw/master/img/structure.png) }}
+ Duck实例设计:{{c1::  ![M9qmQrgLOV](https://gitee.com/xieyun714/nodeimage/raw/master/img/M9qmQrgLOV.jpg)}}


### 策略模式练习题 [  ](designpattern_20201202040742364) 
+ 要求：将下面动作冒险游戏中的类，根据策略模式组织起来，游戏角色的类和角色可以使用的武器行为的类。毎个角色一次只能使用一种武器
但是可以在游戏的过程中换武器。
+ 习题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201128235318.png)
+ 答案：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201128235348.png) }}

## 观察者模式 [  ](designpattern_20201202040742366) 

### 观察者模式的定义与结构 [  ](designpattern_20201202040742369) 
+ 定义:{{c1:: 观察者模式定义了对象之间的一对多依赖，这样一来，当一个对象改变状态时，它的所有依赖者都会收到通知并自动更新。 }}
+ 结构图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201129003828.png) }}
+ 正式版:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203164626.png) }}
+ 气象站实例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201129003910.png)}}

### java.util.Observable的setChanged()方法作用？  [  ](designpattern_20201202040742371) 

+ 解释: {{c1:: 如果没有setChanged()方法，我们的气象站测量是如此敏锐，以致于温度计读数每十分之一度就会更新，这会造成WeatherData对象持续不断地通知观察者，我们并不希望看到这样的事情发生。 }}
+ `clearChanged()`方法:{{c1:: 将changed状态设置回false。 }}
+ `hasChanged()`方法:{{c1:: 告诉你changed标志的当前状态。 }}

### java.util.Observable的缺陷 [  ](designpattern_20201202040742375) 

- 是一个类:{{c1:: Observable是一个类:不是接口, 违反了面向接口编程原则,且java也没有多继承. }}
- 具有`protected`方法:{{c1:: Observable将关键的方法保护`protected`起来:会导致只有子类能使用 }}

## 装饰者模式 [  ](designpattern_20201203022249293) 
### 装饰模式:UML结构图 [  ](designpattern_20201203022249295) 
+ 严格版本:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201202215634.png) }}
+ first head版本：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201202215348.png) }}

### 装饰模式:加密和压缩装饰的示例 [  ](designpattern_20201203022249297) 
+ 程序使用一对装饰来封装数据源对象。 这两个封装器都改变了从磁盘读写数据的方式：
  + 当数据即将被**写入磁盘**前， 装饰对数据进行加密和压缩。 在原始类对改变毫无察觉的情况下， 将加密后的受保护数据写入文件。
  + 当数据刚从**磁盘读出**后， 同样通过装饰对数据进行解压和解密。 装饰和数据源类实现同一接口， 从而能在客户端代码中相互替换。
+ UML结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201202220046.png) }}

### java.io中的装饰者模式 [  ](designpattern_20201203022249299) 
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
### 装饰模式优缺点 [  ](designpattern_20201203022249302) 
+ 优点：
  + **无需新子类**：{{c1:: 无需创建新子类即可扩展对象的行为。 }}
  + **运行时增删**：{{c1:: 可以在运行时添加或删除对象的功能。 }}
  + **组合几种行为**：{{c1:: 多个装饰封装对象来组合几种行为。 }}
  + **单一职责原则**：{{c1:: 你可以将实现了许多不同行为的一个大类拆分为多个较小的类。 }}
+ 缺点：
  + **删除特定封装器**:{{c1:: 在封装器栈中删除特定封装器比较困难。 }}
  + **栈顺序影响**:{{c1:: 实现行为不受装饰栈顺序影响的装饰比较困难。 }}
  + **初始化配置**:{{c1:: 各层的初始化配置代码看上去可能会很糟糕。 }}

## 工厂模式 [  ](designpattern_20201209125527591) 

### 简单工厂模式 [  ](designpattern_20201209125527593) 

+ 结构：![image-20201208234527736](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201208234527736.png)
+ 示例：

```
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
```



### 工厂方法模式定义与结构： [  ](designpattern_20201203022249306) 
+ 定义：{{c1:: 工厂方法模式是一种创建型设计模式，其在父类中提供一个创建对象的方法，允许子类决定实例化对象的类型。 }}
+ 结构：
  + 正式版：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203010112.png) }}
  + 伪代码版：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203010542.png) }}
### 工厂方法模式：问题引出 [  ](designpattern_20201203022249308) 
+ 如何将父类中具体对象类型与父类解耦
+ 问题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203011641.png)
+ 工厂方法模式解决方法：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203011927.png) }}

### 工厂方法模式优缺点 [  ](designpattern_20201203022249311) 
+ 优点
  + **避免耦合**:{{c1:: 可以避免创建者和具体产品之间的紧密耦合。}}
  + **单一职责原则**:{{c1:: 可以将产品创建代码放在程序的单一位置， 从而使得代码更容易维护。}}
  + **开闭原则**:{{c1:: 无需更改现有客户端代码，你就可以在程序中引入新的产品类型。}}
+ 缺点：
  + **复杂性**:{{c1:: 应用工厂方法模式需要引入许多新的子类，代码可能会因此变得更复杂。最好的情况是将该模式引入创建者类的现有层次结构中。 }}

### 抽象工厂模式：问题引出 [  ](designpattern_20201203022249317) 
+ ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203013548.png)
+ 要求：你不希望在添加新产品或新风格时修改已有代码。
+ 解决方案：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203013645.png)}}
### 抽象工厂模式：定义与结构 [	](designpattern_20201203022249320)
+ 定义：{{c1:: 抽象工厂模式提供一个接口，用于创建相关或相互依赖对象的家族，而不需要明确指定具体类。 }}
+ 结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203013705.png) }}

### 抽象工厂模式：具体示例（理解） [  ](designpattern_20201203022249324) 
+ 披萨订购问题结构： ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203014323.png) 
+ 跨平台UI类示例： ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201203015039.png)
+ 理解：{{c1:: 标签 }}
### 抽象工厂模式优缺点 [  ](designpattern_20201203022249326) 
+ 优点：
  + **产品相互匹配**: {{c1:: 你可以确保同一工厂生成的产品相互匹配。 }}
  + **解耦合**: {{c1:: 你可以避免客户端和具体产品代码的耦合。 }}
  + **单一职责原则**: {{c1:: 你可以将产品生成代码抽取到同一位置， 使得代码易于维护。 }}
  + **开闭原则**: {{c1:: 向应用程序中引入新产品变体时， 你无需修改客户端代码。 }}
+ 缺点：
  + **复杂性增加**: {{c1::由于采用该模式需要向应用中引入众多接口和类， 代码可能会比之前更加复杂。 }}

## 单例模式 [  ](designpattern_20201209125527596) 

### 单例模式定义与结构 [  ](designpattern_20201209125527599) 

+ 单例模式定义：{{c1:: 单件模式确保一个类只有一个实例，并提供一个全局访问点。 }}
+ 结构：{{c1:: ![单例模式结构](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201208202027.png) }}
+ 2个必要注意点：
  1. {{c1:: 单例的**构造函数**必须对客户端（Client）代码隐藏。 }}
  2. {{c1:: 调用**获取实例方法**必须是获取单例对象的唯一方式。}}
+ JDK中`Runtime`例:{{c1:: JDK中，java.lang.Runtime就是经典的单例模式(饿汉式) }}

### java的8种单例模式实现方法 [  ](designpattern_20201209125527602) 

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

### 单例模式:饿汉式 [  ](designpattern_20201209125527604) 
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

### 单例模式:懒汉式（线程不安全） [  ](designpattern_20201209125527606) 

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
  + 缺点: {{c1:: **效率低**，每个线程在想获得类的实例时候，执行getInstance()方法都要进行同步。而其实这个方法只执行一次实例化代码就够了，后面的想获得该类实例，直接return就行了。方法进行同步效率太低 }}
  + 结论: {{c1:: 在实际开发中，不推荐这种方式. }}
+ 懒汉式(同步代码块)
  + 实现：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201208210823.png)
  + 注意：不能使用这种方式，这种同步并不能起到线程同步的作用，假如两个线程**同时**进入了`if (singleton == null)`判断语句块，这时便会产生多个实例

### 单例模式：双重检查（Double-Check) [  ](designpattern_20201209125527609) 

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
### 单例模式：静态内部类 [  ](designpattern_20201209125527611) 
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
### 单例模式：使用枚举实现 [  ](designpattern_20201209125527614) 
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

### 单例模式使用的场景举例 [  ](designpattern_20201209125527616) 
+ {{c1:: 需要频繁的进行创建和销毁的对象 }}
+ {{c1:: 创建对象时耗时过多或耗费资源过多(即：重量级对象)，但又经常用到的对象、工具类对象 }}
+ {{c1:: 频繁访问数据库或文件的对象(比如数据源、session工厂等) }}

## 命令模式 [  ](designpattern_20201209125527619) 

### 命令模式：问题引出 [  ](designpattern_20201209125527622) 

+ 需求:开发一款新的文字编辑器， 当前的任务是创建一个包含多个按钮的工具栏， 并让每个按钮对应编辑器的不同操作。
+ 示意图：![image-20201209003259063](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201209003259063.png)
+ 问题：如过需要快捷键替代按钮的功能，这时就不得不多复制一份按钮中对应功能的代码。
+ 解决：{{c1:: ![image-20201209003618359](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201209003618359.png) }}
  + {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201209003956.png) }}

### 命令模式定义与结构 [  ](designpattern_20201209125527624) 
+ 定义：{{c1:: 将一个请求封装成一个对象，从而使您可以用不同的请求对客户进行参数化。 }}
+ 主要目的：{{c1:: 使得请求发送者与请求接收者消除彼此之间的耦合 }}
+ 结构图：
  + 正式版:{{c1:: ![命令模式结构](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201209004327.png) }}
  + 详细版:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201209005335.png) }}
+ 抽象命令类（Command）角色： {{c1:: 明执行命令的接口，拥有执行命令的抽象方法 execute()。 }}
+ 具体命令类（Concrete Command）角色： {{c1:: 抽象命令类的具体实现类，它拥有接收者对象，并通过调用接收者的功能来完成命令要执行的操作。 }}
+ 实现者/接收者（Receiver）角色： {{c1:: 执行与请求相关的操作，**真正执行命令的对象** }}
+ 调用者/请求者（Invoker）角色： {{c1:: **请求的发送者**，它通常拥有很多的命令对象，并通过访问命令对象来执行相关请求，它不直接访问接收者。 }}

### 命令模式：智能生活案例 
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
### 命令模式：宏命令 
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

## 适配器模式 
### 适配器模式定义与结构 
+ 定义：{{c1:: 适配器模式将一个类的接口，转换成客户期望的另一个接口。主要目是兼容性 }}
+ 对象适配器结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201210003513.png) }}
+ 类适配器结构：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201210003608.png) }}

### 适配器模式:类适配器 
+ 结构：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201211063500.png)
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

### 适配器模式:对象适配器 
+ 结构：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201211080620.png)
+ 与类适配器的区别：将继承变成了组合
+ client端实现：
  ```java
  //{{c1::
    System.out.println(" === 对象适配器模式 ====");
    Phone phone = new Phone();
    phone.charging(new VoltageAdapter(new Voltage220V()));
  //}}
  ```
### 适配器模式:接口适配器模式 
+ 作用：当不需要全部实现接口提供的方法时，可先设计一个抽象类实现接口，并为该接口中每个方法提供一个默认实现（空方法），那么该抽象类的子类可有选择地覆盖父类的某些方法来实现需求
+ 例如：
  ```java
  new AnimatorListenerAdapter() {
      @Override
      public void onAnimationStart(Animator animation) {
      //xxxx具体实现
      }
  }
  ```

### 适配器模式在SpringMVC框架应用的源码剖析 

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
+ 标签：理解
+ 库索引：TODO


## 外观模式 
### 外观模式定义与结构 
+ 定义：{{c1:: 外观模式提供了一个统一的接口，用来访间子系统中的一群接口。外观定义了一个高层接口，让子系统更容易使用。 }}
+ 结构：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201210005149.png)
+ 亦称：{{c1:: 门面模式、Facade }}
### test [  ](designpattern_20201202040742377) 
