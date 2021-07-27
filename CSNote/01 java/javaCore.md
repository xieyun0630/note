## 环境配置

### Java相关术语
+ `JDK`：{{c1::Java Development Kit(Java开发工具包）}}
+ `JRE`：{{c1::Java Runtime Environment (Java 运行时环境）}}
+ `Server JRE`：{{c1::(服务器JRE)，在服务器上运行Java程序的软件}}
+ `SE`：{{c1::Standard Edition（标准版），用于桌面或简单服务器应用的Java平台}}
+ `EE`：{{c1::Enterprise Edition，用于复杂服务器应用的Java平台}}
+ `ME`：{{c1::Micro Edition（微型版），用于小型设备的Java平台}}
+ `Java FX`：{{c1::用于图形化用户界面的一个备选工具包，在Java11之前的某些Java SE发布版本中提供}}
+ `OpenJDK`:{{c1::Java SE的一个免费开源实现}}
+ `SDK`: {{c1::Software Development Kit(软件开发工具包）,一个过时的术语，用于描述1998~2006年之间的JDK}}

### JShell
+ 作用：{{c1::Shell s会让Java语言和类库的学习变得轻松而有趣，它不要求你启动一个庞大的开发环境，不会让你再为 public static void main而困扰。}}
+ 使用方法：{{c1::直接在终端中输入jshell命令}}
+ 使用示例：
  + `$n`：{{c1::记录上一个命令结果}}
  + `tab`: {{c1::自动搜索补全}}
  + 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714192112.png)}}

## java基本程序设计结构

### 文件的输入与输出
+ Scanner用法：{{c1::`Scanner in = new Scanner(Path.of(myfile.txt"),Standardcharsets.UTF_8);`}}
+ PrintWriter用法：{{c1::`Printwriter out = new Printwriter("myfile.txt",Standardcharsets.UTF_8);`}}
+ 常见API描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714193619.png)}}

### 数组相关操作
+ 拷贝数组：{{c1::`Luckynumbers Arrays copyof(Luckynumbers, 2 *Luckynumbers. Length)`}}
  + 注意：{{c1::第二个参数为新数组的大小，常用于拓展新数组。}}
+ 数组排序：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714195535.png)}}
+ 不规则数组初始化：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714195829.png)}}


## 面向对象相关概念

### 类路径
+ 作用：{{c1::当使用`java`命令运行一个java类或类中`import 包`时，需要到指定的路径下寻找相应的类,类路径指定该路径。}}
+ 类路径指定方式：
  + 设置环境变量：
    + linux下设置：{{c1::`export CLASSPATH = /classes`}}
    + windows:{{c1:: `set CLASSPATH = c:\classes` }}
  + `java -classpath`:{{c1::java命令中的-classpath参数}}
+ spring配置中`classpath`2种用法解释：
  + `classpath:entry/dev/spring-mvc.xml`:{{c1::使用classpath:这种前缀，就只能代表一个文件。}}
  + `classpath*:**/mapper/mapping/*Mapper.xml`:{{c1::使用classpath*:这种前缀，则可以代表多个匹配的文件}}

### JAR文件
+ 创建JAR文件：
  + 语法：{{c1::`jar cvf jarFileName file1 file2 ...`}}
  + 例：{{c1::`jar cvf CalculatorClasses.jar *.class icon.gif`}}
+ 清单文件：
  + 作用：{{c1::每个JAR文件都包含一个清单文件( manifest),用于描述归档文件的特殊特性。}}
  + 默认名称：{{c1::`MANIFEST.MF`}}
  + 创建包含清单文件语法：{{c1::`jar cfm MyArchive.jar MANIFEST.MF com/mycompany/nypkg/*,class`}}
  + 内容示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714220824.png)}}
+ 可执行JAR文件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714221207.png)}}

### java中hashCode()方法
+ 实现hashCode()的常用工具方法：
  + `Objects.hashCode(Object a)`
  + `Objects.hash(Object... objects)`: {{c1::返回一个散列码，由提供的所有对象的散列码组合而得到，相当于多次调用前一个方法。}}
  + `Arrays.hashCode(xxx[] a)`：{{c1::散列码由数组元素的散列码组成。}}
  + `包装类型.hashCode(xxx value)`
+ 实现hashCode一个重要注意点：{{c1::`equals`与`hashcode`的定义必须相容：如果`x.equals(y)`返回`true`,那么`x.hashcode()`就必须与`y.hashcode()`返回相同的值。}}
+ 实现例：
  + 简单写法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714224003.png)}}
  + null安全写法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714224027.png)}}
  + 最简且null安全写法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714224055.png)}}

### java中可变参数的本质
+ 带可变参数函数：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210715221216.png)
+ 本质上编译器会将：{{c1::编译器将 `new double[]{3.1,40.4,-5}`传递给max方法。}}

## 枚举类 [ ](java_se_20210107100220063)

### 和`int`定义的常量相比，使用`enum`定义枚举有如下好处： [ ](java_se_20210107100220066)

- 首先，`enum`常量本身带有类型信息，即`Weekday.SUN`类型是`Weekday`，编译器会自动检查出类型错误。

  ```
  int day = 1;
  if (day == Weekday.SUN) { // Compile error: bad operand types for binary operator '=='
  }
  ```

- 不同类型的枚举不能互相比较或者赋值，因为类型不符

+ 标签:{{c1:: 理解 }}

### enum实例直接使用`==`比较 [ ](java_se_20210107100220068)

+ 原因：{{c1::  这是因为`enum`类型的每个常量在 JVM中只有一个唯一实例，所以可以直接用`==`比较。`==`比较的是两个引用类型的变量是否是同一个对象。因此，引用类型比较，要始终使用`equals()`方法.}}

### 枚举类特点 [ ](java_se_20210107100220071)

+ 与普通类的关系：{{c1:: Java使用`enum`定义枚举类型，它被编译器编译为`final class Xxx extends Enum { … }`； }}
+ `name()`：{{c1::  通过`name()`获取常量定义的字符串，注意不要使用`toString()`； }}
+ `ordinal()`：{{c1::  通过`ordinal()`返回常量定义的顺序（无实质意义）； }}
+ 定义成员：{{c1:: 可以为`enum`编写构造方法、字段和方法 }}
+ 构造方法：{{c1:: `enum`的构造方法要声明为`private`，字段强烈建议声明为`final`； }}
+ `switch`：{{c1:: `enum`适合用在`switch`语句中。 }}

### 接口
+ **接口VS抽象类**：{{c1::抽象类只能**单一继承**，接口可以保留多继承的优点，避免了多继承带来的复杂性。}}
+ **接口的属性**：{{c1::接口中的字段总是 `public static final`}}
+ **接口中静态/私有方法**：{{c1:: 可以作为工具方法存在。例如`Path/Paths`, Path接口中静态方法可以代替Paths伴随类。}}
+ **默认方法**：{{c1:: 主要为了向后兼容而设计的特性。可以调用接口中的**抽象**方法**提前**实现功能。}}
+ 解决默认方法冲突：
  + 接口冲突：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210715225648.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210715231430.png)}}
  + 类优先：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210715231502.png)}}