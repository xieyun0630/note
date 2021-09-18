
## 环境配置 [ ](javaCore_20210818044143811)

### Java相关术语 [ ](javaCore_20210818044143813)
+ `JDK`：{{c1::Java Development Kit(Java开发工具包）}}
+ `JRE`：{{c1::Java Runtime Environment (Java 运行时环境）}}
+ `Server JRE`：{{c1::(服务器JRE)，在服务器上运行Java程序的软件}}
+ `SE`：{{c1::Standard Edition（标准版），用于桌面或简单服务器应用的Java平台}}
+ `EE`：{{c1::Enterprise Edition，用于复杂服务器应用的Java平台}}
+ `ME`：{{c1::Micro Edition（微型版），用于小型设备的Java平台}}
+ `Java FX`：{{c1::用于图形化用户界面的一个备选工具包，在Java11之前的某些Java SE发布版本中提供}}
+ `OpenJDK`:{{c1::Java SE的一个免费开源实现}}
+ `SDK`: {{c1::Software Development Kit(软件开发工具包）,一个过时的术语，用于描述1998~2006年之间的JDK}}

### JShell [ ](javaCore_20210818044143815)
+ 作用：{{c1::Shell s会让Java语言和类库的学习变得轻松而有趣，它不要求你启动一个庞大的开发环境，不会让你再为 public static void main而困扰。}}
+ 使用方法：{{c1::直接在终端中输入jshell命令}}
+ 使用示例：
  + `$n`：{{c1::记录上一个命令结果}}
  + `tab`: {{c1::自动搜索补全}}
  + 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714192112.png)}}

## java基本程序设计结构 [ ](javaCore_20210818044143817)

### 文件的输入与输出 [ ](javaCore_20210818044143819)
+ Scanner用法：{{c1::`Scanner in = new Scanner(Path.of(myfile.txt"),Standardcharsets.UTF_8);`}}
+ PrintWriter用法：{{c1::`Printwriter out = new Printwriter("myfile.txt",Standardcharsets.UTF_8);`}}
+ 常见API描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714193619.png)}}

### 数组相关操作 [ ](javaCore_20210818044143821)
+ 拷贝数组：{{c1::`Luckynumbers Arrays copyof(Luckynumbers, 2 *Luckynumbers. Length)`}}
  + 注意：{{c1::第二个参数为新数组的大小，常用于拓展新数组。}}
+ 数组排序：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714195535.png)}}
+ 不规则数组初始化：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714195829.png)}}


## 面向对象相关概念 [ ](javaCore_20210818044143823)

### 类路径 [ ](javaCore_20210818044143825)
+ 作用：{{c1::当使用`java`命令运行一个java类或类中`import 包`时，需要到指定的路径下寻找相应的类,类路径指定该路径。}}
+ 类路径指定方式：
  + 设置环境变量：
    + linux下设置：{{c1::`export CLASSPATH = /classes`}}
    + windows:{{c1:: `set CLASSPATH = c:\classes` }}
  + `java -classpath`:{{c1::java命令中的-classpath参数}}
+ spring配置中`classpath`2种用法解释：
  + `classpath:entry/dev/spring-mvc.xml`:{{c1::使用classpath:这种前缀，就只能代表一个文件。}}
  + `classpath*:**/mapper/mapping/*Mapper.xml`:{{c1::使用classpath*:这种前缀，则可以代表多个匹配的文件}}

### JAR文件 [ ](javaCore_20210818044143827)
+ 创建JAR文件：
  + 语法：{{c1::`jar cvf jarFileName file1 file2 ...`}}
  + 例：{{c1::`jar cvf CalculatorClasses.jar *.class icon.gif`}}
+ 清单文件：
  + 作用：{{c1::每个JAR文件都包含一个清单文件( manifest),用于描述归档文件的特殊特性。}}
  + 默认名称：{{c1::`MANIFEST.MF`}}
  + 创建包含清单文件语法：{{c1::`jar cfm MyArchive.jar MANIFEST.MF com/mycompany/nypkg/*,class`}}
  + 内容示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714220824.png)}}
+ 可执行JAR文件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210714221207.png)}}

### java中hashCode()方法 [ ](javaCore_20210818044143829)
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

### java中可变参数的本质 [ ](javaCore_20210818044143831)
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

### 接口 [ ](javaCore_20210818044143833)
+ **接口VS抽象类**：{{c1::抽象类只能**单一继承**，接口可以保留多继承的优点，避免了多继承带来的复杂性。}}
+ **接口的属性**：{{c1::接口中的字段总是 `public static final`}}
+ **接口中静态/私有方法**：{{c1:: 可以作为工具方法存在。例如`Path/Paths`, Path接口中静态方法可以代替Paths伴随类。}}
+ **默认方法**：{{c1:: 主要为了向后兼容而设计的特性。可以调用接口中的**抽象**方法**提前**实现功能。}}
+ 解决默认方法冲突：
  + 接口冲突：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210715225648.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210715231430.png)}}
  + 类优先：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210715231502.png)}}


### 内部类 [ ](javaCore_20210818044143835)
+ 引出原因：{{c1::内部类可以对同一个包中的其他类**隐藏**。内部类方法可以**访问**定义这个类的**作用域**中的数据，包括**原本私有的数据**。}}
+ 内部类对象有一个外围类对象的引用：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210728083341.png)}}
+ 编译器会修改所有的内部类构造器，添加一个对应外围类引用的参数:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210728083524.png)}}
+ 内部类本质：{{c1::本质上是**编译器现象**，JVM只识别**常规类**，编译器会将内部类转换为常规类，并提供**数据访问**的方法。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210728085041.png)}}


### 内部类的特殊语法 [ ](javaCore_20210818044143837)
  + 使用外部类引用正规语法：{{c1::`OuterClass.this`}}
  + 更加明确地编写内部类对象的构造器：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210728084037.png)}}
  + 显式地命名将外围类引用设置为其他的对象：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210728084233.png)}}
  + 在外部类作用域之外，引用内部类：{{c1::`OuterClass.InnerClass`}}


### 内部类：各种类型 [ ](javaCore_20210818044143839)
+ 局部内部类作用：{{c1::局部类有一个很大的优势，即对外部世界完全隐藏，局部类的作用域被限定在声明这个局部类的块中。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210728085553.png)}}
+ 匿名内部类：
  + 作用：{{c1::使用局部内部类时，通常还可以再进一步。假如只想创建这个类的一个对象，甚至不需要为类指定名字。这样一个类被称为匿名内部类( anonymous inner class)}}
  + 示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210728102227.png)}}
  + 注意：{{c1::与lambda表达式的关联}}
+ 静态内部类：
  + 作用：{{c1::有时候，使用内部类只是为了把一个类隐藏在另外一个类的内部，并不需要内部类有外围类对象的一个引用。为此，可以将内部类声明为 static,这样就不会生成那个引用。注释：只要内部类不需要访问外国类对象，就应该使用静态内部类。有些程序员用嵌套类(nested class)表示静态内部类}}

## 异常 [ ](java_se_20210107100220073)
### java的异常类体系 [ ](java_se_20210107100220075)
+ 图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210107155809.png) }}

### java常见异常类 [ ](java_se_20210107100220077)

+ `Error`：{{c1:: `Error`是无需捕获的严重错误 }}
  + `OutOfMemoryError`：{{c1:: 内存耗尽 }}
  + `NoClassDefFoundError`：{{c1:: 无法加载某个Class }}
  + `StackOverflowError`：{{c1:: 栈溢出 }}
+ `Exception`：{{c1:: 运行时的错误，它可以被捕获并处理理。 }}
  + `NumberFormatException`：{{c1:: 数值类型的格式错误 }}
  + `FileNotFoundException`：{{c1:: 未找到文件 }}
  + `SocketException`：{{c1:: 读取网络失败 }}
  + `NullPointerException`：{{c1:: 对某个null的对象调用方法或字段 }}
  + `IndexOutOfBoundsException`：{{c1:: 数组索引越界 }}

### try-catch-resources结构 [ ](javaCore_20210818044143841)
+ `AutoCloseable`作用：{{c1::对于实现AutoCloseable接口的类的实例，将其放到try后面（我们称之为：带资源的try语句），在try结束的时候，会自动将这些资源关闭（调用close方法）。}}
+ 代码演示：
  ```java
  //{{c1::
    public class AutoCloseableDemo {
      public static void main(String[] args) {
          try (AutoCloseableObjecct app = new AutoCloseableObjecct()) {
              System.out.println("--执行main方法--");
          } catch (Exception e) {
              System.out.println("--exception--");
          } finally {
              System.out.println("--finally--");
          }
      }
      //自己定义类 并实现AutoCloseable
      public static class AutoCloseableObjecct implements AutoCloseable {
          @Override
          public void close() throws Exception {
              System.out.println("--close--");
          }
      }
  }
  //}}
  ```

### 堆栈轨迹(stack trace) [ ](javaCore_20210818044143843)
+ 定义：{{c1:: 堆栈轨迹( stack trace)是**程序执行过程**中**某个特定点**上所有挂起的**方法调用**的一个**列表** }}
+ 访问堆栈轨迹
  + 使用Throwable:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731104144.png)}}
  + java9.0后使用StackWalker:
    ```java
    //{{c1::
    /**
    * A program that displays a trace feature of a recursive method call.
    * @version 1.10 2017-12-14
    * @author Cay Horstmann
    */
    public class StackTraceTest
    {
      public static int factorial(int n)
      {
          System.out.println("factorial(" + n + "):");
          var walker = StackWalker.getInstance();
          walker.forEach(System.out::println);      
          int r;
          if (n <= 1) r = 1;
          else r = n * factorial(n - 1);
          System.out.println("return " + r);
          return r;
      }
      public static void main(String[] args)
      {
          try (var in = new Scanner(System.in))
          {
            System.out.print("Enter n: ");
            int n = in.nextInt();
            factorial(n);
          }
      }
    }

    //}}
    ```
  + 输出：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731104302.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731104310.png)}}

### 必须捕获的异常与不需要捕获的异常 [ ](java_se_20210107100220079)
+ 必须捕获的异常：{{c1:: 包括`Exception`及其子类，但不包括`RuntimeException`及其子类，这种类型的异常称为`Checked Exception`。 }}
+ 不需要捕获的异常：{{c1:: 包括`Error`及其子类，`RuntimeException`及其子类 }}
+ 注意：{{c1:: 编译器对RuntimeException及其子类不做强制捕获要求，不是指应用程序本身不应该捕获并处理RuntimeException。是否需要捕获，具体问题具体分析。 }}

### 使用`try ... catch ... finally`时： [ ](java_se_20210113065733182)
- 匹配顺序：{{c1:: 多个`catch`语句的匹配顺序非常重要，子类必须放在前面；}}
- `finally`语句：{{c1:: 保证了有无异常都会执行，它是可选的；}}
- 一个`catch`语句也可以匹配多个：{{c1:: 非继承关系的异常。`catch (IOException | NumberFormatException e)`}}
- `Throwable.getSuppressed()`：{{c1:: 通过`Throwable.getSuppressed()`可以获取所有的`Suppressed Exception`。}}

### 自定义异常 [ ](java_se_20210113065733185)
+ 抛出异常时，{{c1:: 尽量复用JDK已定义的异常类型； }}
+ 根异常: {{c1:: 自定义异常体系时，推荐从`RuntimeException`派生“根异常”，再派生出业务异常； }}
+ 构造方法: {{c1:: 自定义异常时，应该提供多种构造方法。 }}

### 异常使用技巧 [ ](javaCore_20210818044143845)
1. **异常处理不能代替简单的测试**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731105049.png)}}
2. **不要过分地细化异常**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731105255.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731105314.png)}}
3. **充分利用异常层次结构**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731105440.png)}}
4. **不要压制异常**：{{c1::调用某个方法时，不想添加Throws声明到方法定义，这时使用try....catch忽略异常时要谨慎。是否需要做足够的异常处理。}}
5. **在检測错误时，“苛刻”要比放任更好**：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731105912.png)
6. **不要羞于传递异常**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731105955.png)}}

## java9的日志使用 [ ](javaCore_20210818044143847)
+ **基本日志**的使用:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731111324.png)}}
+ **高级日志**:
  + **引出原因**:{{c1:: 在一个专业的应用程序中，你肯定不想将所有的日志都记录到一个**全局日志记录器**中。你可以定义**自己的日志记录器**。 }}
  + **获取日志记录器：**{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731112813.png) }}
  + **日志记录器名也具有层次结构：**{{c1::例如，如果对日志记录器“com. mycompany”设置了日志级别，它的子日志记录器也会继承这个级别。}}
  + **日志级别**：{{c1:: `SEVERE WARNING INFO CONFIG FINE FINER FINEST` }}
  + **设置日志级别**：{{c1:: `logger.setLevel(Level.FINE);` }}
  + **级别日志方法**：{{c1:: `Logger.warning(message);` `Logger.fine(message);` 或 `logger,Log(Level.FINE,message);` }}
  + **记录异常日志**：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731125342.png)

### java9修改日志管理器配置 [ ](javaCore_20210818044143849)
+ 配置文件默认位置：
  + java9以后：{{c1::`conf/logging.properties`}}
  + java9之前：{{c1::`java -Djava.util.logging.config.file=configfile Mainclass`}}
+ 修改日志级别的配置
  + 修改默认级别：{{c1::`conf/logging.properties`中添加`.level=INFO`}}
  + 修改指定日志记录器级别：{{c1::`conf/logging.properties`中添加`com.mycompany.myapp.level=FINE`}}

### java9日志处理器 [ ](javaCore_20210818044143851)
+ 作用：{{c1::接受日志记录器的日志数据，然后以指定的方式输出/持久化。}}
+ 配置处理器的日志级别：{{c1::`conf/logging.properties`中添加`java util.logging.ConsoleHandler.level=INFO`}}
+ 绕过配置文件，安装自己的处理器:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731150653.png)}}
+ 常用处理器：
  1. {{c1::`ConsoleHandler`}}
  2. {{c1::`FileHandler`}}
  3. {{c1::`SocketHandler`}}
  4. {{c1::还可以通过扩展`Handler`类或`Streamhandler`类自定义处理器。}}
+ 过滤器：
  + 过滤器定义：{{c1::需要**实现Filter接口**并定义方法，`boolean isloggable( Logrecord record`}}
  + 使用: {{c1::将一个过滤器安装到一个**日志记录器**或**处理器**中，只需要调用`setFilter`方法就可以}}
+ 格式化器：
  + 格式化器定义：{{c1::需要实现`Formatter`接口并定义方法，`String format(Logrecord record)`}}
  + 使用: {{c1::将一个过滤器安装到一个**处理器**中，只需要调用`setFormatter`方法就可以}}

### 使用java9日志技巧 [ ](javaCore_20210818044143853)
+ 日志记录器的命名：{{c1::可以把日志记录器命名为与主应用包一样,![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731153208.png)}}
+ 覆盖日志默认配置：
  ```java
  //{{c1::
    if (System.getProperty("java.util.logging.config.class") == null
          && System.getProperty("java.util.logging.config.file") == null)
    {
        try
        {
          Logger.getLogger("com.horstmann.corejava").setLevel(Level.ALL);
          final int LOG_ROTATION_COUNT = 10;
          var handler = new FileHandler("%h/LoggingImageViewer.log", 0, LOG_ROTATION_COUNT);
          Logger.getLogger("com.horstmann.corejava").addHandler(handler);
        }
        catch (IOException e)
        {
          Logger.getLogger("com.horstmann.corejava").log(Level.SEVERE,
              "Can't create log file handler", e);
        }
    }
  //}}
  ```

### commons-logging [ ](java_se_20210113065733195)

+ 作用：{{c1:: Commons Logging，可以作为“日志接口”来使用。默认使用jdk内置日志实现 }}
+ 与log4j的关系：
  + {{c1:: 一个负责充当日志API，一个负责实现日志底层 }}
  + {{c1:: 使用Log4j只需要把log4j2.xml和相关jar放入classpath； }}
  + {{c1:: 只有扩展Log4j时，才需要引用Log4j的接口（例如，将日志加密写入数据库的功能，需要自己开发）。 }}
+ 简单使用：
  ```java
  //{{c1::
  Log log = LogFactory.getLog(Main.class);
  log.info("start...");
  log.warn("end.");
  try {
      ...
  } catch (Exception e) {
      log.error("got exception!", e);
  }
  //}}
  ```

### Commons Logging定义了6个日志级别： [ ](java_se_20210113065733197)

1. {{c1:: `FATAL` }}
2. {{c1:: `ERROR` }}
3. {{c1:: `WARNING` }}
4. {{c1:: `INFO` }}
5. {{c1:: `DEBUG` }}
6. {{c1:: `TRACE` }}

### SLF4J和Logback [ ](java_se_20210113065733200)

+ 作用：{{c1:: 其实SLF4J类似于Commons Logging，也是一个日志接口，而Logback类似于Log4j，是一个日志的实现。 }}
+ `Commons Logging`和`SLF4J`的接口使用区别：{{c1:: 不同之处就是Log变成了Logger，LogFactory变成了LoggerFactory。 }}
+ 配置文件：{{c1:: `logback.xml`放到`classpath`下 }}
+ 趋势：{{c1:: 越来越多的开源项目从Commons Logging加Log4j转向了SLF4J加Logback。  }}

## 泛型 [ ](javaCore_20210818044143855)
+ 泛型作用：{{c1::泛型程序设计( generic programming)意味着编写的代码可以对多种不同类型的对象重用。}}
+ 在Java中增加泛型类之前，泛型程序设计是用继承实现的，存在的问题：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210731161922.png)}}
+ 注意泛型的继承关系：{{c1:: 可以把`ArrayList<Integer>`向上转型为`List<Integer>`（`T`不能变！ ），但不能把`ArrayList<Integer>`向上转型为`ArrayList<Number>`（`T`不能变成父类）。}}
- 泛型可以同时定义多种类型，{{c1:: 例如`Map<K, V>`。 }}

### “泛型”方法 [ ](java_se_20210113065733236)
+ 语法: {{c1:: `修饰符 <T，E, ...> 返回值类型 方法名(形参列表) { 方法体... }` }}
```java
public class Pair<T> {
    private T first;
    private T last;
    public Pair(T first, T last) {
        this.first = first;
        this.last = last;
    }
    public T getFirst() { ... }
    public T getLast() { ... }
//{{c1::
    // 静态泛型方法应该使用其他类型区分:
    public static <K> Pair<K> create(K first, K last) {
        return new Pair<K>(first, last);
    }
//}}
}
```

### 从泛型类派生子类的两种情况 [ ](java_se_20210113065733234)

- 子类也是泛型类：{{c1:: 子类和父类的泛型类型要一致：`class ChildGeneric<T> extends Generic<T>` }}
- 子类不是泛型类：{{c1:: 父类要明确泛型的数据类型：`class ChildGeneric extends Generic<String>` }}

### 泛型擦拭法 [ ](java_se_20210113065733239)

- 擦拭法：{{c1:: Java的泛型是采用擦拭法实现的； }}
- 擦拭法决定了泛型`<T>`：
  - 不能是基本类型，例如：{{c1:: `int`； }}
  - 不能获取带泛型类型的`Class`，例如：{{c1:: `Pair<String>.class`； }}
  - 不能判断带泛型类型的类型，例如：{{c1:: `x instanceof Pair<String>`； }}
  - 不能实例化`T`类型，例如：{{c1:: `new T()`。 }}
- 泛型方法要防止重复定义方法，例如：{{c1:: `public boolean equals(T obj)`； }}
- 子类可以获取父类的泛型类型`<T>`。

### 类型擦除 [ ](java_se_20210113065733248)

+ 无限制**类型**擦除：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20200702221003157.png) }}
+ 有限制**类型**擦除：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20200702221003157.png) }}
+ 有限制**方法**擦除：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20200702221026746.png) }}
+ 无限制**方法擦除**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20200702221100946.png) }}


### extends通配符 [ ](java_se_20210113065733245)
使用类似`<? extends Number>`通配符作为**方法参数**时表示：
- 方法内部可以调用获取`Number`引用的方法，例如：{{c1:: `Number n = obj.getFirst();`；}}
- 方法内部无法调用传入`Number`引用的方法（`null`除外），例如：{{c1:: `obj.setFirst(Number n);`。}}
  + 即一句话总结：{{c1:: 使用`extends`通配符表示可以读，不能写。}}

### extends和super通配符区别 [ ](java_se_20210113065733250)

- `<? extends T>`允许：{{c1:: 调用读方法`T get()`获取`T`的引用，但不允许调用写方法`set(T)`传入`T`的引用（传入`null`除外）}}
- `<? super T>`允许：{{c1:: 调用写方法`set(T)`传入`T`的引用，但不允许调用读方法`T get()`获取`T`的引用（获取`Object`除外}}
+ 总结：{{c1:: 一个是允许读不允许写，另一个是允许写不允许读。 }}
+ 标准库例Collections.copy使用示例 :
  ```java
  //{{c1::
  public class Collections {
      // 把src的每个元素复制到dest中:
      public static <T> void copy(List<? super T> dest, List<? extends T> src) {
          for (int i=0; i<src.size(); i++) {
              T t = src.get(i);
              dest.add(t);
          }
      }
  }
  //}}
  ```
+ PECS原则: {{c1:: `Producer Extends Consumer Super` }}

## 集合 [ ](javaCore_20210818044143857)

### 常用具体集合的核心特点 [ ](javaCore_20210818044143859)
+ `Arraylist`: {{c1:: 可以**动态增长和缩减**的一个索引序列 }}
- `Vector`：{{c1:: 和 ArrayList 类似，但它是线程安全的。 }}
+ `LinkedList`: {{c1:: 可以在任何位置**高效插入和删除**的一个有序序列}}

+ `ArrayDeque`: {{c1:: 实现为**循环数组**的一个**双端**队列 }}

+ `HashSet`: {{c1:: **没有重复**元素的一个**无序**集合 }}

+ `TreeSet`: {{c1:: 一个**有序**集，底层实现为红黑树 }}

+ `EnumSet`: {{c1:: 一个包含**枚举类型值**的集 }}

+ `LinkedHashSet`: {{c1:: 一个可以**记住元素插入次序**的集 }}

+ `PriorityQueue`: {{c1:: 允许**高效删除最小元素**的一个集合 }}

+ `HashMap`: {{c1:: 存储**键/值关联**的一个数据结构 }}
  
- `HashTable`：{{c1:: 和 `HashMap` 类似，但它是线程安全的，这意味着同一时刻多个线程同时写入 `HashTable` 不会导致数据不一致。它是遗留类，不应该去使用它，而是使用 `ConcurrentHashMap` 来支持线程安全，`ConcurrentHashMap` 的效率会更高，因为 `ConcurrentHashMap` 引入了分段锁。 }}

+ `TreeMap`: {{c1:: **键有序**的一个映射 }}

+ `EnumMap`: {{c1:: **键属于枚举类型**的一个映射 }}

+ `LinkedHashMap`: {{c1:: 可以**记住键/值项添加次序**的一个映射 }}

+ `WeakHashMap`: {{c1:: **值不会在别处使用时就可以被垃圾回收**的一个映射 }}

+ `IdentityHashMap`: {{c1:: 用`=`而不是用`equals`比较键的一个映射 }}

### 集合接口继承关系 [ ](java_se_20210113065733255)
+ Collection体系类图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191208220948084.png)}}
+ Map体系类图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201101234335837.png) }}

### 容器中迭代器模式  [ ](java_se_20210113065733273)
+ 结构图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191208225301973.png) }}

### `Iterator`遍历`List`  [ ](java_se_20210113065733273)

+ 实际调用：
  ```java
  //{{c1::
  List<String> list = List.of("apple", "pear", "banana");
  for (Iterator<String> it = list.iterator(); it.hasNext(); ) {
    String s = it.next();
    System.out.println(s);
  }
  //}}
  ```
+ 简写版
  ```java
  //{{c1::
  List<String> list = List.of("apple", "pear", "banana");
  for (String s : list) {
    System.out.println(s);
  }
  //}}
  ```
+ `for each`与`Iterable`：{{c1:: 只要实现了`Iterable`接口的集合类都可以直接用`for each`循环来遍历 }}

### List和Array转换  [ ](java_se_20210113065733275)
+ List转换为Array：{{c1:: `Integer[] array = list.toArray(new Integer[3]);` }}
+ Array转换为List：{{c1:: `List.of(T...)`方法，注意，返回的是一个只读`List`： }}

### map视图 [ ](javaCore_20210818044143861)
+ 3种map视图：
	+ 含义：{{c1::键集、值集合（**不是一个Set**）以及键/值对集。}}
	+ 获取方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210801101659.png)	}}
		+ 注意：
			+ {{c1::`keyset`不是 `HashSet`或 `TreeSet`,而是实现了`Set`接口的另外某个类的对象。}}
			+ {{c1::如果在键集视图上调用迭代器的`remove方法`，实际上会从映射中删除这个键和与它关联的值。不过，不能向键集视图中添加元素。}}
			+ 视图有一些限制: {{c1:: 可能只读，可能无法改変大小，或者可能只支持删除而不支持插入（如映射的键视图）。如果试图执行不恰当的操作，受限制的视图就会抛出一个nsupportedoperationexception}}

# TreeSet类概念 [ ](javaCore_20210818044143863)
+ 作用：{{c1:: Treeset类与散列集十分类似，不过，它比散列集有所改进。树集是一个有序集合（ sorted collection)。可以以任意顺序将元素插入到集合中。在对集合进行遍历时，值将自动地按照排序后的顺序呈现。底层数据结构为红黑数}}
+ 与散列集的核心区别：{{c1:: 如果不需要数据是有序的，就没有必要付出排序的开销。树集通常比散列慢，对于某些数据来说，**对其进行排序要比给出一个散列函数更加困难**。例如一个矩形集，是按照面积还是坐标？}}
+ 使用TreeSet必要条件：{{c1::树的排序顺序必须是全序。也就是说，任意两个元素都必须是可比的，并且只有在两个元素相等时结果才为0。}}

### TreeSet的使用实例:创建了Item对象的两个树集。 [ ](javaCore_20210818044143865)
+ 实例目标：{{c1::创建Item对象的两个树集。第一个按照部件编号排序，这是Item对象的默认排序顺序。第二个通过使用一个定制的比较器按照描述信息排序。}}
  ```java
  //{{c1::
  package treeSet;
  import java.util.*;
  public class TreeSetTest
  {
    public static void main(String[] args)
    {
        var parts = new TreeSet<Item>();
        parts.add(new Item("Toaster", 1234));
        parts.add(new Item("Widget", 4562));
        parts.add(new Item("Modem", 9912));
        System.out.println(parts);

        var sortByDescription = new TreeSet<Item>(Comparator.comparing(Item::getDescription));

        sortByDescription.addAll(parts);
        System.out.println(sortByDescription);
    }
  }
  //}}
  ```
+ Item类
  ```java
  //{{c1::
  package treeSet;
  import java.util.*;
  public class Item implements Comparable<Item>
  {
      private String description;
      private int partNumber;

      /**
      * Constructs an item.
      * @param aDescription the item's description
      * @param aPartNumber the item's part number
      */
      public Item(String aDescription, int aPartNumber)
      {
        description = aDescription;
        partNumber = aPartNumber;
      }

      /**
      * Gets the description of this item.
      * @return the description
      */
      public String getDescription()
      {
        return description;
      }

      public String toString()
      {
        return "[description=" + description + ", partNumber=" + partNumber + "]";
      }

      public boolean equals(Object otherObject)
      {
        if (this == otherObject) return true;
        if (otherObject == null) return false;
        if (getClass() != otherObject.getClass()) return false;
        var other = (Item) otherObject;
        return Objects.equals(description, other.description) && partNumber == other.partNumber;
      }

      public int hashCode()
      {
        return Objects.hash(description, partNumber);
      }

      public int compareTo(Item other)
      {
        int diff = Integer.compare(partNumber, other.partNumber);
        return diff != 0 ? diff : description.compareTo(other.description);
      }
  }
  //}}
  ```

# 并发 [ ](javaCore_20210818044143867)

## 线程定义 [ ](javaCore_20210818044143869)

### 线程与进程概念 [ ](java_se_20200604111131319)

+ 进程的特征：{{c1:: 独立性，动态性，并发性。}}
+ 并发性：{{c1:: 同一时刻，有多条指令在多个处理器上同时执行。}}
+ 并行性：{{c1:: 同一时刻只有一条指令执行，多个进程快速轮流执行}}
+ 多线程的优点：{{c1:: 共享内存。创建线程代价小，java内置。}}

### 3种定义线程的方式 [	](java_se_20200604111131320)
+ {{c1::实现 Runnable 接口 }}
+ {{c1::实现 Callable 接口}}
+ {{c1::继承 Thread 类}}


### 实现 Callable 接口 [	](java_se_20200604111131323)

+ 与 Runnable 相比，Callable 可以有返回值，返回值通过 `FutureTask` 进行封装。
  ```java
  //{{c1::
  public class MyCallable implements Callable<Integer> {
      public Integer call() {
          return 123;
      }
  }
  //}}
  ```

+ 调用

  ```java
  //{{c1::
  public static void main(String[] args) throws ExecutionException, InterruptedException {
      MyCallable mc = new MyCallable();
      FutureTask<Integer> ft = new FutureTask<>(mc);
      Thread thread = new Thread(ft);
      thread.start();
      System.out.println(ft.get());
  //}}
  }
  ```

### 多线程：`Callable`接口与`Runnable`接口区别 [	](java_se_20200604111131325)
1. 返回值:{{c1:: `call()`方法可以有返回值。}}
2. 异常:{{c1:: `call()`方法可以声明抛出异常。}}


### 获取线程名字的2个方法 [	](java_se_20200604111131324)
1. `Thread.currentThread()`:{{c1:: 总是返回当前正在执行的线程。 }}
2. `getName()`:{{c1:: Thread类的实例方法，常用于继承 Thread 类的线程。 }}

### Future接口 [	](java_se_20200604111131326)

+ `boolean cancel(boolean mayInterruptIfRunning)`：{{c1:: 试图取消关联的callable任务 }}
+ `boolean isCancelled()`：{{c1:: 判断Callable任务是否取消 }}
+ `boolean isDone()`：{{c1:: 判断Callable任务是否结束 }}
+ `V get()`：{{c1:: 返回Callable任务中的返回值 }}
+ `V get(long timeout, TimeUnit unit)`：{{c1:: 指定时间内，返回Callable任务中的返回值 }}

## 线程通信 [ ](javaCore_20210818044143871)

### 线程状态 [	](java_se_20200604111131327)

+ `isAlive()`：{{c1:: 当线程处于新建与死亡状态时，返回false }}
+ 对死亡的线程调用`start()`方法,会引发{{c1:: `IllegalThreadStateException` }}异常
+ 五种线程状态转换图
  {{c1:: ![image-20200603230326712](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200603230326712.png) }}



### 线程之间的协助 [	](java_se_20200604111131328)

+ `join()`：{{c1:: Thread实例方法，在线程中调用另一个线程的 join() 方法，会将当前线程挂起，而不是忙等待，直到目标线程结束。 }}
+ `wait() notify() notifyAll()`：
  1. {{c1:: Object的实例方法}}
  2. {{c1:: 只能用在同步方法或者同步控制块中使用}}
  3. {{c1:: 使用 wait() 挂起期间，线程会释放锁。这是因为，如果没有释放锁，那么其它线程就无法进入对象的同步方法或者同步控制块中，那么就无法执行 notify() 或者 notifyAll() 来唤醒挂起的线程，造成死锁。}}

### `wait() notify() notifyAll()`使用例子`before after` [	](java_se_20200604111131329)

```java
public class WaitNotifyExample {
//{{c1:: 
    public synchronized void before() {
      System.out.println("before");
        notifyAll();
    }

    public synchronized void after() {
      try {
        wait();
        } catch (InterruptedException e) {
          e.printStackTrace();
        }
        System.out.println("after");
    }
//}}
}
public static void main(String[] args) {
    ExecutorService executorService = Executors.newCachedThreadPool();
    WaitNotifyExample example = new WaitNotifyExample();
    executorService.execute(() -> example.after());
    executorService.execute(() -> example.before());
}
```

### wait() 和 sleep() 的区别 [	](java_se_20200604111131330)

1. {{c1:: wait() 是 Object 的方法，而 sleep() 是 Thread 的静态方法。}}
2. {{c1:: wait() 会释放锁，sleep() 不会。}}

### 后台线程 [	](java_se_20200604111131331)

+ 特征：{{c1:: 如何前台线程都死亡，后台线程自动死亡 }}
+ 设置指定线程成后台线程：{{c1:: Thread对象的`setDaemon(true)`方法 }}

### sleep()方法与yield()方法的区别 [	](java_se_20200604111131333)

1. 优先级：{{c1:: sleep()不理会线程的优先级 }}
2. 状态转换：{{c1:: sleep()会进入阻塞状态，yield直接进入就绪状态 }}
3. 异常：{{c1:: sleep会抛出`InterruptedException`异常，yield没有抛出异常。 }}
4. 可移植性：{{c1:: sleep()比yield()要好。 }}

### 线程的优先级设置 [	](java_se_20200604111131334)
+ Thread类提供了{{c1:: `SetPriority(int newPriority)`}}方法设置优先级。
+ Thread包含3个优先级静态常量：
    1. {{c1:: MAX_PRIORITY:值为10}}
    2. {{c1:: MIN_PRIORITY:值为1}}
    3. {{c1:: NORM_PRIORITY:值为5}}

## 锁机制 [ ](javaCore_20210818044143873)

### Java 提供了两种锁机制来控制多个线程对共享资源的互斥访问 [	](java_se_20200604111131335)

1. {{c1:: JVM 实现的 ` synchronized`。 }}
2. {{c1:: JDK 实现的 `ReentrantLock`。 }}
3. **临界区**定义：{{c1:: **临界区**指的是一个访问共用资源（例如：共用设备或是共用存储器）的程序片段，而这些共用资源又无法同时被多个[线程](https://baike.baidu.com/item/线程/103101)访问的特性。}}
4. **临界资源**：{{c1::**一次仅允许一个进程使用的资源**。}}

- 非同步线程与同步线程的比较：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210807092347.png)}}

### 锁与条件的要点总结 [ ](javaCore_20210818044143875)
+ **锁**作用：
  + {{c1::锁用来保护代码片段，一次只能有一个线程执行被保护的代码。}}
  + {{c1::锁可以管理试图进人被保护代码段的线程。}}
+ **条件对象**作用：
  + {{c1::一个锁可以有一个或多个相关联的条件对象。}}
  + {{c1::每个条件对象管理那些已经进入被保护代码段但还不能运行的线程}}

### volatile [ ](javaCore_20210818044143877)
+ JMM 的抽象示意图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210807111945.png)}}
+ **内存可见性**:{{c1:: 内存可见性是指当一个线程修改了某个变量的值，其它线程总是能知道这个变量变化。也就是说，如果线程 A 修改了共享变量 V 的值，那么线程 B 在使用 V 的值时，能立即读到 V 的最新值。 }}
+ volatile主要作用:{{c1::使用 volatile 修饰共享变量后，每个线程要操作变量时会从主内存中将变量拷贝到本地内存作为副本，当线程操作变量副本并写回主内存后，会通过 **CPU 总线嗅探机制**告知其他线程该变量副本已经失效，需要重新从主内存中读取。}}




### synchronized同步方式 [	](java_se_20200604111131337)
+ `synchronized`本质：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210807104111.png)}}
1. 同步一个代码块：
    {{c1::
  ```java
  public void func() {
    synchronized (this) {
      // ...
      }
  }
  ```
  }}
2. 同步一个方法：
    {{c1::
  ```java
  public synchronized void func () {
    // ...
  }
  ```
  }}
3. 同步一个类：
    {{c1::
  ```java
  public void func() {
    synchronized (SynchronizedExample.class) {
      // ...
      }
  }
  ```
  }}
4. 同步一个静态方法：
    {{c1::
```java
  public synchronized static void fun() {
    // ...
  }
```
  }}
### `ReentrantLock`同步方式 [	](java_se_20200604111131338)

+ 重入锁定的特性：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210807100357.png)}}
```java
//{{c1::
public class LockExample {
  private Lock lock = new ReentrantLock();
    int count;
    public void func() {
      lock.lock();
        try {
          for (int i = 0; i < 10; i++) {
            System.out.println(Thread.currentThread().getName()+":"+(++count));
          }
        } finally {
          lock.unlock(); // 确保释放锁，从而避免发生死锁。
        }
    }
}
//}}
```



### 使用`Conditon`控制线程通信 [	](java_se_20200604111131340)

+ **条件对象**作用：{{c1::线程进入临界区后却发现只有满足了某个条件之后它オ能执行。可以使用一个条件对象来管理那些已经获得了一个锁却不能做有用工作的线程。}}
+ **等待获得锁的线程**和**已经调用了 await方法的线程**存在本质上的不同：{{c1:: 一旦一个线程调用了`await`方法，它就进入这个条件的等待集(wait set)。当锁可用时，该线程并不会变为可运行状态。实际上，它仍保持非活动状态，直到另一个线程在同一条件上调用` signalAll` }}
+ 实例创建：{{c1:: `Conditoin`实例被绑定在一个Lock对象上，调用Lock对象的`newCondition()`方法即可。 }}
+ Condition类提供了3个线程通信方法
  1. {{c1:: `await()`:类似于同步监视器上的`wait()`方法，只是监视器对象变成了Lock对象。 }}
  2. {{c1:: `signal()`:类似与`notify()` }}
  3. {{c1:: `signalAll()`:类似于`notifyAll()` }}

### 线程不会释放同步监视器的情况 [	](java_se_20200604111131339)

1. {{c1:: 程序调用`Thread.sleep()`方法时 }}
2. {{c1:: 程序调用`Thread.yield()`方法时   }}
3. {{c1:: 调用了线程的`suspend()`方法 }}

### 使用`ReentrantLock`与`Conditon`的生产者消费者模式(实践) [	](java_se_20200604111131342)

```java
public class Account {
	// 显示定义Lock对象
	private final Lock lock = new ReentrantLock();
	// 获得指定Lock对象对应的条件变量
	private final Condition cond = lock.newCondition();
	// 账户编号
	private String accountNo;
	// 余额
	private double balance;

	// 标识账户中是否已经存款的旗标
	private boolean flag = false;

	public void draw(double drawAmount) {
    // {{c1::
		// 加锁
		lock.lock();
		try {
			// 如果账户中还没有存入存款，该线程等待
			if (!flag) {
				cond.await();
			} else {
				// 执行取钱操作
				System.out.println(Thread.currentThread().getName() + " 取钱:" + drawAmount);
				balance -= drawAmount;
				System.out.println("账户余额为：" + balance);
				// 将标识是否成功存入存款的旗标设为false
				flag = false;
				// 唤醒该Lock对象对应的其他线程
				cond.signalAll();
			}
		} catch (InterruptedException ex) {
			ex.printStackTrace();
		}
		// 使用finally块来确保释放锁
		finally {
			lock.unlock();
    }
    // }}
	}

	public void deposit(double depositAmount) {
    // {{c1::
		lock.lock();
		try {
			// 如果账户中已经存入了存款，该线程等待
			if (flag) {
				cond.await();
			} else {
				// 执行存款操作
				System.out.println(Thread.currentThread().getName() + " 存款:" + depositAmount);
				balance += depositAmount;
				System.out.println("账户余额为：" + balance);
				// 将标识是否成功存入存款的旗标设为true
				flag = true;
				// 唤醒该Lock对象对应的其他线程
				cond.signalAll();
			}
		} catch (InterruptedException ex) {
			ex.printStackTrace();
		}
		// 使用finally块来确保释放锁
		finally {
			lock.unlock();
    }
    //}}
	}
}
```

### `BlockingQueue`接口包含的方法之间的对应关系 [	](java_se_20200604111131343)

| 失败时，         | 抛出异常           | 返回false         | 阻塞线程        | 指定超时时长            |
| ---------------- | ------------------ | ----------------- | --------------- | ----------------------- |
| 队尾插入元素     | {{c1:: add(e) }}   | {{c1:: offer(e)}} | {{c1:: put(e)}} | offer(e,time,unit)}}    |
| 队头删除元素     | {{c1:: remove()}}  | {{c1:: poll()}}   | {{c1:: take()}} | {{c1::poll(time,unit)}} |
| 获取、不删除元素 | {{c1:: element()}} | {{c1:: peek()}}   | {{c1:: 无}}     | {{c1:: 无}}             |

### `BlockingQueue`接口具有的实现类 [	](java_se_20200604111131344)
+ {{c1:: `ArrayBlockingQueue` }}
+ {{c1:: `LinkedBlockingQueue`  }}
+ {{c1:: `PriorityBlockingQueue`  }}
+ {{c1:: `DelayQueue` }}
+ {{c1:: `SynchronousQueue` }}

{{c1:: ![image-20200604222338200](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200604222338200.png) }}

## 线程组  [ ](javaCore_20210818044143879)

### 线程组 [	](java_se_20200615060135980)

+ 作用：{{c1:: **可以批量管理线程或线程组对象，有效地对线程或线程组对象进行组织**。}}
+ 概念图:
	{{c1:: ![img](https://images2015.cnblogs.com/blog/801753/201510/801753-20151005180622909-789401754.png) }}

### 线程组的相关API [	](java_se_20200615060135982)

+ `Tread`类提供的构造器，设置新创建的线程属于哪个线程组
  + `Thread(ThreadGroup group, Runnable target)`
  + `Thread(ThreadGroup group, Runnable target, String name)`
  + `Thread(ThreadGroup group, String name)`
  + 参数：
    + `ThreadGroup group`:{{c1:: 指定线程组}}
    + `Runnable target`:{{c1:: 线程类}}
    + `String name`:{{c1:: 线程名称}}
  + 注意：{{c1:: 线程一旦加入指定线程组后，中途不能改变该线程所属组。  }}
+ `ThreadGroup`类
  + 构造器
    + `ThreadGroup(String name) `
    + `ThreadGroup(ThreadGroup parent, String name) `
    + 参数：
      + `ThreadGroup parent`：{{c1:: 父线程组 }}
      + `String name`：{{c1:: 线程组名称 }}
  + 方法：
    + `int activeCount()`：{{c1:: 活动线程的数目 }}
    + `void interrupt()`：{{c1:: 中断线程组中所有线程 }}
    + `boolean isDaemon()`：{{c1:: 是否后台线程组 }}
    + `void setDaemon(boolean daemon)`：{{c1:: 设置为后台线程组 }}
    + `void setMaxPriority(int pri)`：{{c1:: 设置线程组的最高优先级 }}

### Thread提供了两个方法来自定义（未处理的）异常处理： [	](java_se_20200615060135983)

+ `static setDefaultUncaughtExceptionHandler(UncaughtExceptionHandler eh)`:{{c1::  为线程类的所有实例设置默认的异常处理器}}
+ `setUncaughtExceptionHandler(UncaughtExceptionHandler eh)`:{{c1:: 为指定线程实例设置异常处理器}}
+ 自定义异常处理器
  ```java
    public class ExHandler
    {
      public static void main(String[] args) 
      {
        //{{c1::
        Thread.currentThread().setUncaughtExceptionHandler(
            (t,e)->{
                System.out.println(t + " 线程出现了异常：" + e);
            });
        int a = 5 / 0;
        //}}
      }
    }
  ```

## 任务和线程池 [ ](javaCore_20210818044143881)

### Executors类 [ ](javaCore_20210818044143883)
+ 作用：{{c1::执行器( Executors)类有许多静态工厂方法，用来**构造线程池**}}
+ 常用工厂方法：
  + `newCachedThreadPool`：{{c1:: 必要时创建新线程；空闲线程会保留60秒 }}
  + `newFixedThreadPool`：{{c1:: 池中包含固定数目的线程；空闲线程会一直保留 }}
  + `newWorkStealingPool`：{{c1::创建时如果不设置任何参数，则以当前机器处理器个数作为线程个数，此线程池会并行处理任务，不能保证执行顺序。}}
  + `newSingleThreadExecutor`：{{c1:: 创建一个单线程线程池。}}
  + `newScheduledThreadPool`：{{c1:: 用于调度执行的固定线程池 }}
  + `newSingleThreadScheduledExecutor`：{{c1:: 用于调度执行的单线程“池” }}
+ 提交线程到线程池：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210811082101.png)}}
+ 关闭线程池：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210811082226.png)}}
+ 线程池使用流程：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210811082330.png)}}
+ `ScheduleExecutorService`: {{c1:: 可以调度`Runnable`或`Callable`在一个初始延迟之后运行一次。也可以调度 Runnable定期运行。 }}
+ 控制任务工具方法:
  + `invokeAny`: {{c1::类似js的`promise.race()`方法}}
  + `invokeAll`：{{c1::类似js的`promise.all()`方法，返回一个`List<Future>`}}
    + `ExecutorCompletionService`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210811084904.png)}}

### fork-join框架 [ ](javaCore_20210818044143885)
+ 作用：{{c1:: 可以将一个大任务，分解为不同子任务交给多个线程处理 }}
+ `RecursiveTask` `RecursiveAction`区别：{{c1::RecursiveTask会生成类型为T的结果，RecursiveAction不生成任何结果}}
+ 示例：假设想统计一个数组中有多少个元素满足某个特定的属性。可以将这个数组一分为二，分别对这两部分进行统计，再将结果相加。
  ```java
  //{{c1::
  class Counter extends RecursiveTask<Integer>
  {
    //...
    protected Integer compute()
    {
        if (to - from < THRESHOLD)
        {
          int count = 0;
          for (int i = from; i < to; i++)
          {
              if (filter.test(values[i])) count++;
          }
          return count;
        }
        else
        {
          int mid = (from + to) / 2;
          var first = new Counter(values, from, mid, filter);
          var second = new Counter(values, mid, to, filter);
          invokeAll(first, second);
          return first.join() + second.join();
        }
    }
  }
  //}}
  ```

### 异步计算:CompletableFuture [ ](javaCore_20210818044143887)
+ CompletableFuture核心作用：
  1. {{c1::异步任务结束时，会自动回调某个对象的方法。}}
  2. {{c1::异步任务出错时，会自动回调某个对象的方法。}}
  3. {{c1::主线程设置好回调后，不再关心异步任务的执行。}}
+ CompletableFuture的命名规则：
  + `xxx()`：{{c1::表示该方法将继续在已有的线程中执行；}}
  + `xxxAsync()`：{{c1::表示将异步在线程池中执行。}}
+ CompletableFuture可以指定异步处理流程：
  + `thenAccept()`: {{c1::处理正常结果。}}
  + `exceptional()`: {{c1::处理异常结果。}}
  + `thenApplyAsync()`: {{c1::用于串行化另一个CompletableFuture。}}
  + `anyOf()和allOf()`: {{c1::用于并行化多个CompletableFuture。}}
+ **supplyAsync**任务分配：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210812083515.png)}}
+ **whenComplete**异常处理: {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210812084114.png)}}
+ **手动设置完成值/异常**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210812084326.png)}}
  + 注意：{{c1::如果这个future已经完成，这些调用没有任何作用。}}
+ `supplyAsync`与`runAsync`区别: {{c1:: `supplyAsync`表示创建带返回值的异步任务的，相当于`ExecutorService submit(Callable<T> task)` 方法，`runAsync`表示创建无返回值的异步任务，相当于`ExecutorService submit(Runnable task)`方法,这两方法各有一个重载版本，可以指定执行异步任务的`Executor`实现，如果不指定`executor`，默认使用`ForkJoinPool.commonPool()`: }}

### 异步计算:CompletableFuture的使用 [ ](javaCore_20210818044143889)
+ thenApply()和thenCompose()的区别(例):
  + thenApply()：{{c1::
      ```java
      CompletableFuture<Integer> future = CompletableFuture.supplyAsync(() -> {
            return 100;
      });
      CompletableFuture<String> f = future.thenApplyAsync(i -> i * 10).thenApply(i -> i.toString());
      System.out.println(f.get()); //"1000"
      ```
      }}
  + thenCompose()：{{c1::
      ```java
      CompletableFuture<Integer> future = CompletableFuture.supplyAsync(() -> {
          return 100;
      });
      CompletableFuture<String> f = future.thenCompose( i -> {
          return CompletableFuture.supplyAsync(() -> {
              return (i * 10) + "";
          });
      });
      System.out.println(f.get()); //1000
      ```
  }}
+ 使用例:同时从新浪和网易查询证券代码，只要任意一个返回结果，就进行下一步查询价格，查询价格也同时从新浪和网易查询，只要任意一个返回结果，就完成操作
  ```java
  //{{c1::
      public static void main(String[] args) throws Exception {
        // 两个CompletableFuture执行异步查询:
        CompletableFuture<String> cfQueryFromSina = CompletableFuture.supplyAsync(() -> {
            return queryCode("中国石油", "https://finance.sina.com.cn/code/");
        });
        CompletableFuture<String> cfQueryFrom163 = CompletableFuture.supplyAsync(() -> {
            return queryCode("中国石油", "https://money.163.com/code/");
        });
        // 用anyOf合并为一个新的CompletableFuture:
        CompletableFuture<Object> cfQuery = CompletableFuture.anyOf(cfQueryFromSina, cfQueryFrom163);
        // 两个CompletableFuture执行异步查询:
        CompletableFuture<Double> cfFetchFromSina = cfQuery.thenApplyAsync((code) -> {
            return fetchPrice((String) code, "https://finance.sina.com.cn/price/");
        });
        CompletableFuture<Double> cfFetchFrom163 = cfQuery.thenApplyAsync((code) -> {
            return fetchPrice((String) code, "https://money.163.com/price/");
        });
        // 用anyOf合并为一个新的CompletableFuture:
        CompletableFuture<Object> cfFetch = CompletableFuture.anyOf(cfFetchFromSina, cfFetchFrom163);
        // 最终结果:
        cfFetch.thenAccept((result) -> {
            System.out.println("price: " + result);
        });
        // 主线程不要立刻结束，否则CompletableFuture默认使用的线程池会立刻关闭:
        Thread.sleep(200);
    }
  //}}
  ```

### java进程相关类 [ ](javaCore_20210818044143890)
+ `java.lang.ProcessBuilder`：{{c1::通过配置相关信息，建立一个进程。}}
  + 执行命令配置：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210812142018.png)}}
+ `java.lang.Process`：{{c1::JVM启动的运行中的进程，可以控制进程的生命周期}}
+ `java.lang.ProcessHandle`：{{c1::进程句柄，可以访问当前操作系统中可见进程。}}
+ `java.lang.ProcessHandle.Info`：{{c1::可以访问当前操作系统中可见进程相关信息}}

## 流 [ ](javaCore_20210818044143892)

### 流与集合的区别 [ ](javaCore_20210818044143894)
1. 流并**不存储其元素**: {{c1::这些元素可能存储在底层的集合中，或者是按需生成的。}}
2. 流的操作**不会修改其数据源**: {{c1::例如，filter方法不会从新的流中移除元素，而是会生成一个新的流，其中不包含被过滤掉的元素。}}
3. 流的操作是**尽可能惰性执行**的: {{c1::这意味着直至需要其结果时，操作オ会执行。例如，如果我们只想查找前5个长单词而不是所有长单词，那么filter方法就会在匹配到第5个单词后停止过滤。因此，我们甚至可以操作无限流。}}

### Steam常用API [ ](javaCore_20210818044143896)
+ `java.util.Collection`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210812215248.png)}}
+ `java.util.stream.Stream`:{{c1::![image-20210812215901466](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812215901466.png)}}
+ `java.util.Arrays`:{{c1::![image-20210812220003672](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812220003672.png)}}
+ `java.util.regex.Pattern`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210812220027.png)}}
+ `java.nio.file.Files`:{{c1::![image-20210812220107402](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812220107402.png)}}
+ `java.util.function.Supplier`:{{c1::![image-20210812220133224](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812220133224.png)}}
+ `java.util.Optional`:{{c1::![image-20210812234505312](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812234505312.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813083316.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813083551.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813111450.png)}}


### Stream常用方法 [ ](javaCore_20210818044143898)
+ `filter` `map` `flatMap`:{{c1::![image-20210812220441663](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812220441663.png)}}
+ `limit` `skip` `concat`:{{c1::![image-20210812222549134](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812222549134.png)}}
+ `distinct` `sorted` `peek`: {{c1::![image-20210812223541147](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812223541147.png)}}
+ `max`` min`` findFirst`` findAny`` anyMatch`` allMatch`` noneMatch`:{{c1::![image-20210812231101581](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812231101581.png)}}
+ `reduce`用法:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813211538.png)}}

### Stream收集器常用方法 [ ](javaCore_20210818044143900)
+ `stream.forEach` `stream.toArray` `stream.collect`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813113921.png)}}
+ `Collector.toList/toSet/toCollection/joining/summarizingXXX/`:{{c1::![image-20210813115029910](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210813115029910.png)![image-20210813115102212](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210813115102212.png)}}
+ `xxxDoublesummarystatistics.getCount/getSum/getMax/getMin`:{{c1::![image-20210813115110819](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210813115110819.png)}}
+ `Collector.toMap`使用例:
  + 2个参数示例：{{c1::![image-20210813133821000](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210813133821000.png)}}
  + 3个参数示例：{{c1::![image-20210813133847730](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210813133847730.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813133933.png)}}
  + 4个参数示例：{{c1::![image-20210813134409949](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210813134409949.png)}}


### Steam常用函数应用 [ ](javaCore_20210818044143902)
+ 裁剪随机数的无限流：{{c1:: ![image-20210812222406292](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812222406292.png) }}
+ 去重：{{c1:: ![image-20210812222905217](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812222905217.png) }}
+ 排序：{{c1:: ![image-20210812222943338](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812222943338.png) }}
+ 进行流调试：{{c1:: ![image-20210812223358040](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812223358040.png) }}

### 如何使用Optional [ ](javaCore_20210818044143903)
+ 如何有效使用`Optional`方式：
  1. 不存在任何值的情况下产生相应的替代物:{{c1::![image-20210812232241605](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812232241605.png)}}
  2. 只有在其存在的情况下才消费该值:{{c1::![image-20210812234355845](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210812234355845.png)}}
+ 无效使用`Optional`值的方式：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813083240.png)}}
+ 创建`Optional`值：{{c1::![image-20210813083707513](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210813083707513.png)}}
  + 关键点：{{c1::当自定义方法可能返回null时，可返回`Optional`对象代替}}
+ 用`flatMap`来构建`Optional`值的函数：{{c1::![image-20210813111342662](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210813111342662.png)}}

### Stream分组 [ ](javaCore_20210818044143905)
+ `Collector.groupingBy/groupingByConcurrent/partitioningBy`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813135315.png)}}
  + 使用例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813135341.png)}}
+ 下游收集器使用例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813140025.png)}}
+ `counting` `summing` `maxBy` `minBy`:{{c1::![image-20210813195439483](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210813195439483.png)}}
+ `mapping`方法：{{c1::![image-20210813203115407](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210813203115407.png)}}
+ 分组中使用`summaryStatistics`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813203250.png)}}

### 基本类型的流 [ ](javaCore_20210818044143907)
+ 作用：{{c1::基本类型的流执行效率比引用类型高的多。}}
+ `IntStream` `LongStream` `DoubleStream`分别对应的基本类型:{{c1::如果想要存储 short、char、byte和boo1ean,可以使用 Instream,而对于f1oat,可以使用 Doublestream。}}
+ 创建IntStream:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813211855.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813211947.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813212045.png)}}
+ `mapToInt/Long/Double` `boxed`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210813212310.png)}}

### 并行流处理示例 [ ](javaCore_20210818044143909)
```java
   //{{c1::
   public static void main(String[] args) throws IOException
   {
      var contents = new String(Files.readAllBytes(
         Paths.get("../gutenberg/alice30.txt")), StandardCharsets.UTF_8);
      List<String> wordList = List.of(contents.split("\\PL+"));

      // Very bad code ahead
      var shortWords = new int[10];
      wordList.parallelStream().forEach(s -> 
         {
            if (s.length() < 10) shortWords[s.length()]++;
         });
      System.out.println(Arrays.toString(shortWords));

      // Try again--the result will likely be different (and also wrong)
      Arrays.fill(shortWords, 0);
      wordList.parallelStream().forEach(s -> 
         {
            if (s.length() < 10) shortWords[s.length()]++;
         });
      System.out.println(Arrays.toString(shortWords));

      // Remedy: Group and count
      Map<Integer, Long> shortWordCounts = wordList.parallelStream()
         .filter(s -> s.length() < 10)
         .collect(groupingBy(String::length, counting()));

      System.out.println(shortWordCounts);

      // Downstream order not deterministic
      Map<Integer, List<String>> result = wordList.parallelStream().collect(Collectors.groupingByConcurrent(String::length));

      System.out.println(result.get(14));

      result = wordList.parallelStream().collect(Collectors.groupingByConcurrent(String::length));

      System.out.println(result.get(14));

      Map<Integer, Long> wordCounts = wordList.parallelStream().collect(groupingByConcurrent(String::length, counting()));
      System.out.println(wordCounts);
   //}}
   }
```

## 输入/输出 [ ](javaCore_20210818044143911)
### Java 的 I/O 大概可以分成以下几类： [ ](java_se_20210107100220084)

- 磁盘操作：{{c1:: `File` }}
- 字节操作：{{c1:: `InputStream` 和 `OutputStream` }}
- 字符操作：{{c1:: `Reader` 和 `Writer` }}
- 对象操作：{{c1:: `Serializable` }}
- 网络操作：{{c1:: `Socket` }}
- 新的输入/输出：{{c1:: `NIO` }}

### 磁盘操作：File类 [ ](java_se_20210107100220087)

+ 作用：{{c1:: File 类可以用于表示文件和目录的信息，但是它不表示文件的内容。 }}

+ 代替方案：{{c1:: 从 Java7 开始，可以使用 Paths 和 Files 代替 File。 }}

+ 使用例：递归地列出一个目录下所有文件

  ```java
  //{{c1::
  public static void listAllFiles(File dir) {
      if (dir == null || !dir.exists()) {
          return;
      }
      if (dir.isFile()) {
          System.out.println(dir.getName());
          return;
      }
      for (File file : dir.listFiles()) {
          listAllFiles(file);
      }
  }
  //}}
  ```



### InputStream/OutputStream常用方法API [ ](javaCore_20210818044143913)
+ `inputStream.read/skip/available/close/mark/reset/markSupported`:{{c1::![image-20210814081542587](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814081542587.png)![image-20210814081559353](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814081559353.png)}}
+ `outputStream.write/close/flush`:{{c1::![image-20210814081741033](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814081741033.png)}}




### 字节操作： 使用`InputStream` 和 `OutputStream`实现文件复制 [ ](java_se_20210107100220090)

```java
//{{c1::
public static void copyFile(String src, String dist) throws IOException {
    FileInputStream in = new FileInputStream(src);
    FileOutputStream out = new FileOutputStream(dist);
    byte[] buffer = new byte[20 * 1024];
    int cnt;

    // read() 最多读取 buffer.length 个字节
    // 返回的是实际读取的个数
    // 返回 -1 的时候表示读到 eof，即文件尾
    while ((cnt = in.read(buffer, 0, buffer.length)) != -1) {
        out.write(buffer, 0, cnt);
    }

    in.close();
    out.close();
  //}}
}
```

### Reader 与 Writer [ ](java_se_20210107100220101)

+ 作用：{{c1:: 不管是磁盘还是网络传输，最小的存储单元都是字节，而不是字符。但是在程序中操作的通常是字符形式的数据，因此需要提供对字符进行操作的方法。 }}

- `InputStreamReader` ：{{c1:: 实现从字节流解码成字符流； }}

- `OutputStreamWriter` ：{{c1:: 实现字符流编码成为字节流。 }}

- 例:实现逐行输出文本文件的内容

  ```java
  public static void readFileContent(String filePath) throws IOException {
  //{{c1::
      FileReader fileReader = new FileReader(filePath);
      BufferedReader bufferedReader = new BufferedReader(fileReader);
  
      String line;
      while ((line = bufferedReader.readLine()) != null) {
          System.out.println(line);
      }
  
      // 装饰者模式使得 BufferedReader 组合了一个 Reader 对象
      // 在调用 BufferedReader 的 close() 方法时会去调用 Reader 的 close() 方法因此只要一个 close() 调用即可
      bufferedReader.close();
  //}}
  }
  ```

### 常用IO实现类 [ ](javaCore_20210818044143915)
+ `FileInputStream`:{{c1::![image-20210814093820064](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814093820064.png)}}
+ `FileOutputStream`:{{c1::![image-20210814093826081](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814093826081.png)}}
+ `BufferedInputStream`:{{c1::![image-20210814093833112](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814093833112.png)}}
+ `BufferedOutputStream`:{{c1::![image-20210814093839171](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814093839171.png)}}
+ `PushbackInputStream`:{{c1::![image-20210814093846451](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814093846451.png)}}
+ `PrintWriter/printWriter.print/println/printf/checkError`:{{c1::![image-20210814094505913](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814094505913.png)![image-20210814094525153](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814094525153.png)}}
+ `DataInput`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210814102026.png)}}
+ `DataOutput`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210814102059.png)}}
+ `RandomAccessFile`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210814103904.png)}}


### Java I/O中的装饰者模式 [ ](java_se_20210107100220092)

- Java I/O 使用了装饰者模式来实现。以 InputStream 为例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/9709694b-db05-4cce-8d2f-1c8b09f4d921.png) }}
- `DataInputStream` ：{{c1:: 提供了对更多数据类型进行输入的操作 }}
- `BufferedInputStream` ：{{c1:: 为 FileInputStream 提供缓存的功能。 }}

### 编码与解码 [ ](java_se_20210107100220098)

+ 各编码方式的中英文占比：
  + GBK 编码中:{{c1:: 中文字符占 2 个字节，英文字符占 1 个字节； }}
  + UTF-8 编码中:{{c1:: 中文字符占 3 个字节，英文字符占 1 个字节； }}
  + UTF-16be 编码中:{{c1:: 中文字符和英文字符都占 2 个字节。 }}
+ Java 的内存编码使用：{{c1:: 双字节编码UTF-16be，双字节编码的好处是可以使用一个 char 存储中文和英文}}
- String类的编码与解码：{{c1::
  ```java
  String str1 = "中文";
  //注意：getBytes() 的默认编码方式与平台有关，一般为 UTF-8。
  byte[] bytes = str1.getBytes("UTF-8");
  String str2 = new String(bytes, "UTF-8");
  System.out.println(str2);
  ```
  }}



### java ZIP文档 [ ](javaCore_20210818044143917)
+ 通读ZIP文件代码序列示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210814104704.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210814104718.png)}}
+ 写入ZIP代码示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210814105041.png)}}
+ 相关API
  + `ZipInputStream`: {{c1::![image-20210814110616643](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814110616643.png)}}
  + `ZipOutputStream`: {{c1::![image-20210814110628570](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814110628570.png)![image-20210814110644476](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814110644476.png)}}
  + `ZipEntry`: {{c1::![image-20210814110701878](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814110701878.png)}}
  + `ZipFile`: {{c1::![image-20210814110716866](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814110716866.png)}}


### 对象序列化 [ ](javaCore_20210818044143918)
+ 对象序列化原因图示：{{c1::![image-20210814132415847](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814132415847.png)}}
+ 作用：{{c1:: 序列化就是将一个对象转换成字节序列，方便存储和传输。 }}
+ 实现：
  - 序列化**核心方法**：{{c1:: `ObjectOutputStream.writeObject()` }}
  - 反序列化**核心方法**：{{c1:: `ObjectInputStream.readObject()` }}
    ```java
    //{{c1::
    public static void main(String[] args) throws IOException, ClassNotFoundException {
    
        A a1 = new A(123, "abc");
        String objectFile = "file/a1";
    
        ObjectOutputStream objectOutputStream = new ObjectOutputStream(new FileOutputStream(objectFile));
        objectOutputStream.writeObject(a1);
        objectOutputStream.close();
    
        ObjectInputStream objectInputStream = new ObjectInputStream(new FileInputStream(objectFile));
        A a2 = (A) objectInputStream.readObject();
        objectInputStream.close();
        System.out.println(a2);
    }
    //}}
    ```
+ 自定义序列化方式
  + `transient`关键字：{{c1::序列化时，被标记的成员变量会被跳过。}}
  + 实现特殊方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210814160106.png)}}
+ 不会对静态变量进行序列化：{{c1:: 因为序列化只是保存对象的状态，静态变量属于类的状态。 }}
  
  + `Serializable`接口：{{c1:: 序列化的类需要实现 Serializable接口，它只是一个标准，没有任何方法需要实现，但是如果不去实现它的话而进行序列化，会抛出异常。 }}

### Path类 [ ](javaCore_20210818044143920)
+ 作用：{{c1::Path表示的是一个**目录**名**序列**，其后还可以跟着一个文件名。}}
+ 常用方法
  + `static get`: {{c1::![image-20210814165055714](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814165055714.png)}}
  + `resolve` `resolveSibling` `relativize` `normalize`:{{c1::![image-20210814165355690](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814165355690.png)}}
  + `toAbolutePath` `getParent` `getFileName` `getRoot` `toFile`:{{c1::![image-20210814170018097](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210814170018097.png)}}
  + `java.io.File Path toPath()`:{{c1::![image-20210815103018629](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815103018629.png)}}

### Files类 [ ](javaCore_20210818044143922)
+ 作用：{{c1:: 提供操作中小型大小文件的一系列简便方法,以及作为常规输入输出流工厂}}
+ 常用方法：
  + `readAllBytes` `readAllLines` `write`:{{c1::![image-20210815105218189](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815105218189.png)}}
  + `newInputStream` `newOutputStream` `newBufferedReader` `newBufferedWriter`:{{c1::![image-20210815105341663](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815105341663.png)}}
  + `createFile` `createDirectory` `createDirectories` `createTempFile` `createTempDirectory`:{{c1::![image-20210815114533336](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815114533336.png)}}
  + `copy` `move` `delete` `deleteIfExists`:{{c1::![image-20210815145424687](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815145424687.png)}}
  + `exists` `isHidden` `isReadable` `isWritable` `isExecutable` `isRegularFile` `isDirectory` `isSymbolicLink` `size` `readAttributes`:{{c1::![image-20210815150034528](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815150034528.png)}}
  + `list` `walk`:{{c1::![image-20210815153635631](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815153635631.png)}}
  + `newDirectoryStream walkFileTree`:{{c1::![image-20210815154047240](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815154047240.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210815163012.png)}}
  + glob模式，`*` `**` `?` `[...]` `{...}` `\`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210815154153.png)}}
  + `SimpleFileVisitor`:{{c1::![image-20210815162918728](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815162918728.png)}}
    + 删除目录树使用示例：{{c1::![image-20210815163236227](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815163236227.png)}}

### BasicFileAttributes类 [ ](javaCore_20210818044143924)
+ 作用：{{c1::所有的文件系统都会报告一个基本属性集，它们被封装在Basi cFileAttributes接口。}}
+ 获取对象方式：{{c1::![image-20210815150411123](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815150411123.png)}}
+ 相关方法：
  + `creationTime`` lastAccessTime`` lastModifiedTime`` isRegularFile`` isDirectory`` isSymbolicLink`` size`` fileKey`:{{c1::![image-20210815150556587](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815150556587.png)![image-20210815150612507](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210815150612507.png)}}


### ZIP文件系统 [ ](javaCore_20210818044143926)
+ 遍历文件树示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210817020326.png)}}
+ `FileSystems/FileSystem`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210817020419.png)}}

### 内存映射文件 [ ](javaCore_20210826082439278)
+ 作用：{{c1::大多数操作系统都可以利用虚拟内存实现来将一个文件或者文件的一部分“映射”到内存中。然后，这个文件就可以当作是内存数组一样地访问，这比传统的文件操作要快得多。}}
+ java.nio内存映射
  + 创建通道：{{c1::`FileChannel channel =FileChannel.open(path, options);`}}
  + 支持的模式：
    + `READ_ONLY`:{{c1::![image-20210820172736554](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820172736554.png)}}
    + `READ_WRITE`{{c1:::![image-20210820173052575](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820173052575.png)}}
    + `PRIVATE`: {{c1::![image-20210820172750881](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820172750881.png)}}
+ 内存映射文件相关API
  + `FileInputStream`:{{c1::![image-20210820173849561](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820173849561.png)}}
  + `FileOutputStream`:{{c1::![image-20210820173853947](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820173853947.png)}}
  + `RandomAccessFile`:{{c1::![image-20210820173900425](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820173900425.png)}}
  + `FileChannel`:{{c1::![image-20210820173909835](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820173909835.png)![image-20210820173918639](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820173918639.png)}}
  + `Buffer`:{{c1::![image-20210820174015306](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820174015306.png)}}
  + `ByteBuffer`:{{c1::![image-20210820174031180](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820174031180.png)![image-20210820174103489](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820174103489.png)}}
  + `charBuffer`:{{c1::![image-20210820174121889](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820174121889.png)![image-20210820174134605](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820174134605.png)}}

### java.nio缓冲区数据结构 [ ](javaCore_20210826082439281)
+ 什么是缓冲区：{{c1::缓冲区是由具有相同类型的数值构成的数组}}
+ 缓冲区构成：
  + **容量**：{{c1::它永远不能改变。}}
  + **读写位置**：{{c1::下一个值将在此进行读写。}}
  + **界限**：{{c1::超过它进行读写是没有意义的。}}
  + **标记**：{{c1::用于重复一个读入或写出操作。}}
  + 构成图：{{c1::![image-20210820174856919](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820174856919.png)}}
+ 常用Buffer类方法
  + `clear` `flip` `rewind` `mark` `reset` `remaining` `position capacity`:{{c1::![image-20210820175254590](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210820175254590.png)}}

### java.nio文件加锁机制 [ ](javaCore_20210826082439282)
+ 获得锁:
  ```java
  //{{c1::
    FileChannel channel = FileChannel.open(path);
    FileLock lock = channel.lock();
    File lock = channel.tryLock();
  //}}
  ```
+ 相关API
  + `fileChannel.lock/trylock`:{{c1::![image-20210821095240408](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821095240408.png)}}
  + `FileLock`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821095308.png)}}

## XML [ ](javaCore_20210826082439284)

### JAVA中提供的两种XML解析器 [ ](javaCore_20210826082439286)
+ **DOM**:{{c1:: 像文档对象模型(Document Object Model,DOM)解析器这样的树型解析器（tree parser),它们将读入的XML文档转换成树结构。 }}
+ **SAX**:{{c1:: 像XML简单API(Simple API for XML,SAX)解析器这样的流机制解析器(streaming parser),它们在读入XML文档时生成相应的事件。 }}
+ 使用区别：{{c1::如果你要处理很长的文档，用它生成树结构将会消耗大量内存，或者如果你只是对于某些元素感兴趣，而不关心它们的上下文，那么在这些情况下你应该考虑使用流机制解析器。}}

### java XML处理API [ ](javaCore_20210826082439288)
+ Document对象构成：{{c1::Document对象是XML文档的树型结构在内存中的表示方式，它由实现了**Node接口及其各种子接口**的类的对象构成。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821134119.png)}}
+ 获取Document对象：{{c1::![image-20210821133821876](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821133821876.png)}}
+ 启动对文档内容的分析：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821144746.png)}}
+ 相关API：
  + `DocumentBuilderFactory`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821145243.png)}}
  + `DocumentBuilder`:{{c1::![image-20210821150202852](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821150202852.png)}}
  + `Document`:{{c1::![image-20210821150220189](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821150220189.png)}}
  + `Element`:{{c1::![image-20210821150228930](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821150228930.png)}}
  + `Node`:{{c1::![image-20210821150241780](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821150241780.png)![image-20210821150253223](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821150253223.png)}}
  + `CharacterData`：{{c1::![image-20210821150312780](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821150312780.png)}}
  + `NodeList`：{{c1::![image-20210821150321240](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821150321240.png)}}
  + `NamedNodeMap`：{{c1::![image-20210821150330410](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821150330410.png)}}

### 验证XML文件：DTD定义 [ ](javaCore_20210826082439290)
+ 目的:自动校验某个文档是否具有正确的结构。
+ 嵌入式定义方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821153335.png)}}
+ SYSTEM声明：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821153414.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821153422.png)}}
+ PUBLIC声明：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821153507.png)}}
+ ELEMENT通用语法：{{c1::`<!ELEMENT elementName RegExp>`}}
  + 常用内容定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821155323.png)}}
+ ATTLIST通用语法：{{c1::`<!ATTLIST element attribute type default>`}}
  + 常用属性类型定义：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821155612.png) }}
  + 常用属性默认值定义：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821155629.png) }}
  + 示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821155654.png) }}
+ 启用验证特性：{{c1:: `factory.setValidating(true);` }}
+ 提供错误处理器：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821160506.png)}}
+ 安装错误处理器：{{c1::`builder.setErrorHandler(handler)`}}
+ 相关API：
  + `documentBuilder.setEntityResolver/setErrorHandler`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821160954.png)}}
  + `EntityResolver`：{{c1::![image-20210821162715889](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821162715889.png)}}
  + `InputSource`：{{c1::![image-20210821162700480](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821162700480.png)![image-20210821162706319](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821162706319.png)}}
  + `ErrorHandler `：{{c1::![image-20210821162649338](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821162649338.png)}}
  + `SAXParseException`：{{c1::![image-20210821162643710](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821162643710.png)}}
  + `documentBuilderFactory.isValidating/setValidating/isIgnoringElementContentWithspcase/setIgnoringElementContentWithspcase`:{{c1::![image-20210821162635202](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821162635202.png)}}

### 验证XML文件：XMLSchema定义 [ ](javaCore_20210826082439292)
+ 引用Schema文件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821163211.png)}}
+ 简单示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821163237.png)}}

### XPath表达式 [ ](javaCore_20210826082439294)
+ 作用: {{c1::如果要定位某个XML文档中的一段特定信息，那么，通过遍历DOM树的众多节点来进行查找会显得有些麻烦。Xpath语言使得访问树节点变得很容易。}}
+ 表达式示例:
  + 选择节点集：{{c1::`/gridbag/row`}}
  + `[]`操作符：{{c1::`/gridbag/row[1]/cell[1]/@anchor`}}
  + 获取属性：{{c1::`/gridbag/row/cell/@anchor`}}
  + 函数使用：{{c1::`count(/gridbag/row)`}}
+ java计算XPath表达式调用:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210821205945.png)}}
+ 相关API
  + `XPathFactory`:{{c1::![image-20210821210308719](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821210308719.png)}}
  + `xPath.evaluate`:{{c1::![image-20210821210316250](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210821210316250.png)}}

### XML中命名空间概念 [ ](javaCore_20210826082439296)

+ 定义：{{c1::XML中的命令空间通常是一串URL地址。}}
+ 子元素可以提供自己的命名空间：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823193607.png)}}
+ 短标识符：
  + 作用：{{c1::可以通过简短的字符串表示子孙元素的命名空间。}}
  + 典型例子：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823193947.png)
  + 注意：{{c1::只有子元素继承了它们父元素的命名空间，而**不带显式前缀的属性**并不是命名空间的一部分。}}
+ 相关API
  + `getLocalName/getNamespaceURI`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823194214.png)}}
  + `isNamespaceAware/setNamespaceAware`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823194247.png)}}

### java SAX解析器 [ ](javaCore_20210826082439298)
+ 作用: {{c1::SAX解析器在解析XML输入数据的各个组成部分时会报告事件，但不会以任何方式存储文档}}
+ ContentHandler接口的回调方法
+ `startElement` `endEtement` : {{c1::在每当遇到起始或终止标签时调用。}}
+ `characters` : {{c1::在每当遇到字符数据时调用。}}
+ `startDocument` `endDocument` : {{c1::分别在文档开始和结束时各调用一次。}}
  
  + 例如：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823200831.png)}}
+ 获得SAX解析器代码示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823201226.png)}}
+ 使用SAX解析器网络爬虫程序示例：
  ```java
  //{{c1::
  public static void main(String[] args) throws Exception
   {
      String url;
      if (args.length == 0)
      {
         url = "http://www.w3c.org";
         System.out.println("Using " + url);
      }
      else url = args[0];

      var handler = new DefaultHandler()
         {
            public void startElement(String namespaceURI, String lname, 
                  String qname, Attributes attrs)
            {
               if (lname.equals("a") && attrs != null)
               {
                  for (int i = 0; i < attrs.getLength(); i++)
                  {
                     String aname = attrs.getLocalName(i);
                     if (aname.equals("href")) 
                        System.out.println(attrs.getValue(i));
                  }
               }
            }
         };

      SAXParserFactory factory = SAXParserFactory.newInstance();
      factory.setNamespaceAware(true);
      factory.setFeature(
         "http://apache.org/xml/features/nonvalidating/load-external-dtd", 
         false);
      SAXParser saxParser = factory.newSAXParser();
      InputStream in = new URL(url).openStream();
      saxParser.parse(in, handler);
   }
  //}}
  ```

### java SAX解析器相关API [ ](javaCore_20210826082439300)
+ `SAXParserFactory`类`static newInstance` `newSAXParser` `isNamespaceAware` `setNamespaceAware` `isValidating` `setValidating`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823205437.png)}}
+ `SAXParser`类 `parse`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823205557.png)}}
+ `ContentHandler`类 `startDocument` `endDocument` `startElement` `endElement` `characters`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823205721.png)}}
+ `Attributes`类 `getLength` `getLocalName` `getURI` `getQName` `getValue`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823205824.png)}}

### java StAX解析器 [ ](javaCore_20210826082439302)
+ 特点：{{c1::是一种**拉解析器（pull parser)**}}
+ 简单网络爬虫示例：
  ```java
  //{{c1::
   public static void main(String[] args) throws Exception
   {
      String urlString;
      if (args.length == 0)
      {
         urlString = "http://www.w3c.org";
         System.out.println("Using " + urlString);
      }
      else urlString = args[0];
      var url = new URL(urlString);
      InputStream in = url.openStream();
      XMLInputFactory factory = XMLInputFactory.newInstance();
      XMLStreamReader parser = factory.createXMLStreamReader(in);
      while (parser.hasNext())
      {
         int event = parser.next();
         if (event == XMLStreamConstants.START_ELEMENT)
         {
            if (parser.getLocalName().equals("a")) 
            {
               String href = parser.getAttributeValue(null, "href");
               if (href != null)
                  System.out.println(href);               
            }
         }
      }
   }
  //}}
  ```
+ 相关API
  + `XMLInputFactory`类 `newInstance` `getProperty` `createXMLStreamReader`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823212401.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823212413.png)}}
  + `XMLStreamReader`类 `hasNext` `next` `isStartElement` `isEndElement` `isCharacters` `isWhiteSpace` `getName` `getLocalName` `getText` `getAtrributeCount/Name/LocalName/Vlue`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823212704.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823212718.png)}}

### java生成XML文档:通过DOM写出XML文件 [ ](javaCore_20210826082439304)
+ 建立一颗不带命名空间的DOM树：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823214800.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823214829.png)}}
+ 建立一颗命名空间的DOM树：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210823215727.png)}}
+ 通过DOM写出XML文件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825213953.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825214018.png)}}
+ 使用StAX写出XML文档:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825222508.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825222621.png) }}
+ 相关API
  + `DocumentBuilder`类 `newDocument`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825214336.png)}}
  + `Document`类 `createElement` `createElementNS` `createTextNode`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825214350.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825214407.png)}}
  + `Node`类 `appendChild`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825214514.png)}}
  + `Element`类 `setAttribute` `setAttributeNS`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825214534.png)}}
  + `TransformerFactory`类 `newInstance` `newTransformer`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825214723.png)}}
  + `Transformer`类 `setOutputProperty` `transform`：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825214905.png)}}
  + `DOMSource`类: {{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825215029.png)}}
  + `StreamResult`类：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825215118.png)}}

## java网络编程 [ ](javaCore_20210826082439306)

### java Socket连接服务器 [ ](javaCore_20210826082439308)
+ `telnet`命令测试端口连通性示例：
  + 访问UDP：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825231544.png)}}
  + 访问HTTP：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825231530.png)}}
+ java Socket测试端口连通性:
  ```java
  //{{c1::
  public static void main(String[] args) throws IOException
   {
      try (var s = new Socket("time-a.nist.gov", 13);
            var in = new Scanner(s.getInputStream(), StandardCharsets.UTF_8))
      {
         while (in.hasNextLine())
         {
            String line = in.nextLine();
            System.out.println(line);
         }
      }
   }
  //}}
  ```
+ Socket超时问题：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825234633.png) }}
+ 相关API：
  
  + `Socket`类 `getInputStream` `getOutputStream` `Socket` `connect` `setSoTimeout` `isConnected` `isClosed`:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210825234817.png) }}

### InetAddress [ ](javaCore_20210826082439310)
+ 作用：{{c1::如果需要在主机名和因特网地址之间进行转换，那么就可以使用InetAddress类。}}
+ 简单使用示例:
  ```java
  //{{c1::
  public class InetAddressTest
  {
    public static void main(String[] args) throws IOException
    {
        if (args.length > 0)
        {
          String host = args[0];
          InetAddress[] addresses = InetAddress.getAllByName(host);
          for (InetAddress a : addresses)
              System.out.println(a);
        }
        else
        {
          InetAddress localHostAddress = InetAddress.getLocalHost();
          System.out.println(localHostAddress);
        }
    }
  }
  //}}
  ```
+ 相关API：
  
  + `InetAddress`类 `getByName` `getALLByName` `getLocalHost` `getAddress` `getHostAddress`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826000113.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826000147.png)}}

### ServerSocket [ ](javaCore_20210911041056116)
+ 使用流程：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826222322.png)}}
+ 单线程服务示例：
  ```java
  public class EchoServer
  {
    public static void main(String[] args) throws IOException
    {
      //{{c1::
        // establish server socket
        try (var s = new ServerSocket(8189))
        {
          // wait for client connection
          try (Socket incoming = s.accept())
          {
              InputStream inStream = incoming.getInputStream();
              OutputStream outStream = incoming.getOutputStream();
    
              try (var in = new Scanner(inStream, StandardCharsets.UTF_8))
              {
                var out = new PrintWriter(
                    new OutputStreamWriter(outStream, StandardCharsets.UTF_8),
                    true /* autoFlush */);
        
                out.println("Hello! Enter BYE to exit.");
        
                // echo client input
                var done = false;
                while (!done && in.hasNextLine())
                {
                    String line = in.nextLine();
                    out.println("Echo: " + line);
                    if (line.trim().equals("BYE")) done = true;
                }
              }
          }
        }
      //}}
    }
  }
  ```
+ 多线程服务：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826225105.png)}}
+ 半关闭示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826230324.png)}}
+ 可中断套接字：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826232622.png)}}
+ 相关API
  + `ServerSocket`类 `ServerSocket(int port)` `accept` `close`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826223348.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826223403.png)}}
  + `Socket`类 `shutdownOutput` `shutdownInput` `isOutputShutdown` `isInputShutown`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826230503.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826230515.png)}}
  + `InetSocketAddress`类 `InetSocketAddress(hostname,port)` `isUnresolved`:![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826231936.png)
  + `SocketChannel`类 `open`:![image-20210826232041566](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210826232041566.png)![image-20210826232105730](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210826232105730.png)
  + `Channels`类`newInputStream` `newOutputStream`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826232217.png)}}

### java的URI与URL [ ](javaCore_20210911041056118)
+ 主要区别：{{c1::URI不提供**访问资源**的方法，URI类的作用是**解析标识符**并将它分解成各种不同的组成部分，以及处理**绝对**URI与**相对**URI。}}
+ **绝对**URI与**相对**URI：
  + 绝对化：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826234729.png)}}
  + 相对化：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210826234805.png)}}

### URLConnection [ ](javaCore_20210911041056120)
+ 作用：{{c1::如果想从某个Web资源获取更多信息，那么应该使用 Urlconnection类，通过它能够得到比基本的URL类更多的控制功能。}}
+ 基本使用示例：
  ```java
  //{{c1::
  public static void main(String[] args)
   {
      try
      {
         String urlName;
         if (args.length > 0) urlName = args[0];
         else urlName = "http://horstmann.com";

         var url = new URL(urlName);
         URLConnection connection = url.openConnection();

         // set username, password if specified on command line

         if (args.length > 2)
         {
            String username = args[1];
            String password = args[2];
            String input = username + ":" + password;
            Base64.Encoder encoder = Base64.getEncoder();
            String encoding = encoder.encodeToString(input.getBytes(StandardCharsets.UTF_8));
            connection.setRequestProperty("Authorization", "Basic " + encoding);
         }

         connection.connect();

         // print header fields

         Map<String, List<String>> headers = connection.getHeaderFields();
         for (Map.Entry<String, List<String>> entry : headers.entrySet())
         {
            String key = entry.getKey();
            for (String value : entry.getValue())
               System.out.println(key + ": " + value);
         }

         // print convenience functions

         System.out.println("----------");
         System.out.println("getContentType: " + connection.getContentType());
         System.out.println("getContentLength: " + connection.getContentLength());
         System.out.println("getContentEncoding: " + connection.getContentEncoding());
         System.out.println("getDate: " + connection.getDate());
         System.out.println("getExpiration: " + connection.getExpiration());
         System.out.println("getLastModifed: " + connection.getLastModified());
         System.out.println("----------");

         String encoding = connection.getContentEncoding();
         if (encoding == null) encoding = "UTF-8";
         try (var in = new Scanner(connection.getInputStream(), encoding))
         {   
            // print first ten lines of contents
   
            for (int n = 1; in.hasNextLine() && n <= 10; n++)
               System.out.println(in.nextLine());
            if (in.hasNextLine()) System.out.println(". . .");
         }
      }
      catch (IOException e)
      {
         e.printStackTrace();
      }
   }
  //}}
  ```
+ 发送Post请求流程：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210907235541.png)}}
+ 相关API:
  + `URL`类 `openStream` `openConnection`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210907232728.png)}}
  + `URLConnection`: `set/getDoInput` `set/getDoOutput` `set/getIfModifiedSince` `set/getUseCaches` `set/getAllowUserInteraction` `set/getConnectTimeout` `set/getReadTimeout` `set/getRequestProperty` `connect` `getHeaderFields`:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210907233255.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210907233338.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210907233450.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210907233508.png)}}

### java发送EMail简介 [ ](javaCore_20210911041056121)
+ 简单使用套接字发送：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210908000125.png)}}
  + 注意:{{c1::该方式并没有实现认证功能。}}
+ JavaMail方式：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210908000324.png)}}


### 第八章 [ ](javaCore_20210917101115656)
+ DOTO