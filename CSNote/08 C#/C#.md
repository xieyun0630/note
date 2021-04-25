
## C#基础 [ ](C#_20210327100148441)

### .NET Core 编译命令 [ ](C#_20210327100148444)
+ 查看模板列表: {{c1::`dotnet new`}}
+ 创建命令行应用: {{c1::`dotnet new console --output HelloWorld`}}
+ 构建应用：{{c1:: `dotnet build` }}
+ 运行应用：{{c1::在应用根目录下运行 `dotnet run` }}
+ 发布应用程序：{{c1:: `dotnet publish -f netcoreapp2.0 -c Release` }}
  + 发布指定平台版本: `dotnet publish -f netcoreapp2.0 -c Release -r win10-x64`
  + 跨平台发布cspro对应配置:
    ```xml
    //{{c1::
    <PropertyGroup>
        <RuntimeIdentifiers>win10-x64;ubuntu-x64;osx.10.11-x64;</RuntimeIdentifiers>
    </PropertyGroup>
    //}}
    ```

### 变量 [ ](C#_20210327100148446)
+ 类型推断var关键字：{{c1::`var someNumbyer = 0;` 等价于 `int someNumber;`}}
+ 常量声明：{{c1::`const int a = 100;`}}
+ `sbyte` `short` `int` `long` `byte` `ushort` `uint` `ulong`对应的.NET数据类型：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322114223.png)}}

### 字符串字面量 [ ](C#_20210327100148448)
+ `@`前缀：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322115013.png)
+ `$`前缀：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322115024.png)

### using关键字 [ ](C#_20210327100148450)
+ 作用：{{c1::为类型建立层次结构}}
+ using定义层次结构图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322115245.png)}}
+ 名称空间别名图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322115340.png)}}

### C#的3种注释 [ ](C#_20210327100148453)
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322115436.png)}}

### C#预处理器指令 [ ](C#_20210327100148456)
+ `#define #undef` : {{c1::相当于boolean值}}
+ `#if #elif #else #endif` :{{c1::根据`#define`所定义的常量进行判断}}
+ `#warning #error` ::{{c1:: `#warning` 编译时发出警告信息，`#error`发送错误信息且停止编译。}}
+ `#region #endregion` : {{c1::为代码区域命名}}
+ `#pragma`: {{c1::抑制或还原指定的编译警告}}

## 第3章 对象和类型  [ ](C#_20210327100148459)

### C# 类与结构 [ ](C#_20210327100148461)
+ 声明类语法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322130633.png)}}
+ 声明结构语法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322130654.png)}}
+ 声明实例：{{c1::对于类和结构，都使用关键字new来声明实例![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322131019.png)}}
+ 类与结构重要区别：{{c1::类型的对象通过引用传递，结构类型的对象按值传递}}

### C# 字段 [ ](C#_20210327100148463)
+ 字段声明：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322131344.png)
+ 字段声明：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322131551.png)
  + 注意：{{c1::如果只读字段是一个实例字段，就要在实例构造函数中初始化它。}}

### C# 属性 [ ](C#_20210327100148465)
+ 常规语法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322132646.png)}}
+ 具有表达式体的属性访问器：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322132708.png)}}
+ 自动实现的属性：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322132744.png)}}
+ 属性的访问修饰符：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322133005.png)}}

### C# 只读属性 [ ](C#_20210327100148468)
+ 只读属性：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322133101.png) }}
+ 自动实现的只读属性：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322133444.png)}}
+ 表达式体属性：{{c1:: 是带有get访问器的属性，但不需要get关键字![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322133755.png) }}
  

### C# 匿名类型 [ ](C#_20210327100148472)
+ 注意点：
  + 匿名类型只是一个继承自{{c1::Object且没有名称的类。}}
  + 根据字段名来区分各个类，{{c1::具有完全相同字段的两个类，类型相同。}}
  + 如果所设置的值来自于另一个对象，{{c1::则可以推断匿名类型成员的名称}}
+ 语法:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322134326.png)}}

### C# 方法 [ ](C#_20210327100148474)
+ 表达式体方法声明：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322134906.png)}}
+ 命名的参数方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322142022.png)}}
+ 可选参数方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322142124.png)}}
+ 可变参数方法：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322142307.png) }}

### C# 构造函数 [ ](C#_20210327100148477)
+ 表达式体构造函数:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322142428.png)}}
+ 从构造函数中调用其他构造函数:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322142501.png)}}
+ 静态构造函数：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322142548.png)}}

### C# 结构 [ ](C#_20210327100148479)
+ 结构的继承体系:{{c1::每个结构派生自System.ValueType类，System.ValueType派生自System.Object类。}}
+ 结构是值类型，具体到代码上与类的区别：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322143050.png)}}
+ 只读结构的声明：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322143115.png)}}

### C# 按值和按引用传递参数 [ ](C#_20210327100148481)
+ ref参数：
  + 图示：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322145201.png)
  + 传递结构：{{c1::为A添加ref关键字可以使用**引用**传递结构}}
  + 传递类型：{{c1::把A作为类类型，使用ref修饰符，传递对**引用的引用**(在C+术语中，是一个**指向指针的指针**）}}
+ out参数：
  + 作用：{{c1::通过参数返回方法调用结果}}
  + TryParse图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322145509.png)}}
+ in参数：
  + 作用：{{c1:: 保证发送到方法中的数据不会更改(在传递值类型时) }}
  + 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322150647.png) }}

### C# 可空类型 [ ](C#_20210327100148483)
+ 声明语法：{{c1:: `int? x = null;` }}
+ 注意：可空类型转换为普通类型时，{{c1:: 需要类型强制转换，如果是null会抛出异常 }}
+ HasValue与Value属性：{{c1:: `int x5 = x3.HasValue ? x3.Value : -1;` }}
+ 合并运算符结合可空类型使用：{{c1:: `int x6 = x3 ?? -1; `}}

### C# 枚举类型 [ ](C#_20210327100148485)
+ 默认情况下enum类型是int，改变为其他类型语法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322153339.png)}}
+ 理解[flags]在枚举中的作用：使用位进行枚举判断。
  ```c#
    [Flags]
    public enum DaysOfWeek
    {
        Monday = 0x1,
        Tuesday = 0x2,
        Wednesday = 0x4,
        Thursday = 0x8,
        Friday = 0x10,
        Saturday = 0x20,
        Sunday = 0x40,
        Weekend = Saturday | Sunday,
        Workday = 0x1f,
        AllWeek = Workday | Weekend
    }
  ```
  + 例如给`Daysofweek`的一个变量设置值3,{{c1::结果是`Monday`,如果使用`[Flags]`属性，结果就是`Tuesday`代码}}

### C# Enum类常用工具方法 [ ](C#_20210327100148487)
+ Enum.TryParse:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322154805.png)}}
+ Enum.GetNames:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322154815.png)}}
+ Enum.GetValues:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322154824.png)}}

### C# 部分类 [ ](C#_20210327100148490)
+ 作用：{{c1:: `partial`关键字允许把类、结构、方法或接口放在多个文件中。}}
+ 用法：{{c1::把 `partial`放在 `class` `struct` 或 `interface`关键字的前面。}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322161219.png)}}
+ 部分方法的作用：{{c1:: 使用生成的代码调用了可能不存在的方法，可以使用部分方法避免编译错误。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322161448.png) }}

### C# 拓展方法 [ ](C#_20210327100148493)
+ 作用:{{c1::本质上是静态方法，并没有放在类的源代码中。}}
+ 注意点：
  + this关键字声明
  + 实例方法优先
  + 方法冲突时，优先最近的命名空间。同层冲突报错。
+ 示例：
  ```C#
  //{{c1::
  namespace ExtensionMethods
  {
      namespace Foo
      {
          public static class StringExtensions
          {
              public static int GetWordCount(this string s) =>
                  s.Split().Length;           
          }
      }

      namespace Bar
      {
          public static class StringExtensions2
          {
              public static int GetWordCount(this string s) =>
                  s.Split().Length + 10;           
          }
      }

      class Program
      {
          static void Main()
          {
              string fox = "the ss quick brown fox jumped over the lazy dogs down 9876543210 times";
              int wordCount = fox.GetWordCount();
              Console.WriteLine($"{wordCount} words");
              Console.ReadLine();
          }
      }
  }
  //}}
  ```

## 第4章 继承 [ ](C#_20210327100148497)

### 实现继承 [ ](C#_20210327100148500)
+ 类继承：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322164204.png)}}
+ 结构继承（只能继承接口)：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322164151.png)}}

### 虚方法 [ ](C#_20210327100148502)
+ 作用：{{c1::指明基类中的方法可以被子类重写。}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322164422.png)}}

### 隐藏方法 [ ](C#_20210327100148505)
+ 定义：{{c1:: 如果签名相同的方法在基类和派生类中都进行了声明，但该方法没有分别声明为 virtual和 override,派生类方法就会隐藏基类方法 }}
 + new关键字抑制编译警告：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322170107.png)

### 调用方法的基类版本 [ ](C#_20210327100148508)
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322171723.png)}}

### 抽象类 [ ](C#_20210327100148511)
+ 语法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322171903.png)}}
+ 处理待定实现的抽象方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322172005.png)}}

### sealed关键字 [ ](C#_20210327100148514)
+ 作用：{{c1::给类`sealed`，不允许创建该类的子类。给方法`sealed`，表示不能重写该类的方法。}}
+ 注意：{{c1::需要密封的方法，要声明为virtual。}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322172412.png)}}

### C#调用基类的构造函数 [ ](C#_20210327100148519)
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322174202.png)}}

### C# 访问修饰符 [ ](C#_20210327100148522)

+ `public`:{{c1::公有访问。不受任何限制。}}
+ `private`:{{c1::私有访问。只限于本类成员访问，子类，实例都不能访问。}}
+ `protected`:{{c1::保护访问。只限于本类和子类访问，实例不能访问。}}
+ `internal`:{{c1::内部访问。只限于本项目内访问，其他不能访问。}}
+ `protected internal`:{{c1::内部保护访问。只限于本项目或是子类访问，其他不能访问 `protected` 或 `internal`}}
+ `private protected`:  {{c1::`private` 且 `protected`}}

### is和as运算符 [ ](C#_20210327100148525)
+ is使用例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322175532.png)}}
+ as使用例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322175545.png)}}
+ 体会主要区别:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323083210.png)}}

## 第5章 泛型 [ ](C#_20210327100148527)

### 泛型对性能的提升 [ ](C#_20210327100148530)
+ 主要因素：{{c1::泛型可以减少装箱与拆箱带来的性能损失}}
+ 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322180038.png)}}

### C# 泛型中default关键字 [ ](C#_20210327100148532)
+ 作用：{{c1::将null赋予引用类型，将0赋予值类型。}}
+ 示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322180751.png)}}

### C#泛型约束 [ ](C#_20210327100148535)

+ `where T: struct` : {{c1:: 对于结构约束，类型T必须是值类型 }}
+ `where T: class` : {{c1:: 类约束指定类型T必须是引用类型 }}
+ `where T: Ifoo` : {{c1:: 指定类型T必须实现接口IFoo }}
+ `where T: Foo` : {{c1:: 指定类型T必须派生自基类Foo }}
+ `where T: new()` : {{c1:: 这是一个构造函数约東，指定类型T必须有一个默认构造函数 }}
+ `where TI: T2` : {{c1:: 这个约束也可以指定，类型T1派生自泛型类型T2 }}
+ 合并多个约束：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322181413.png)}}
+ 带约束泛型方法图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323080856.png)}}

### C# 泛型继承 [ ](C#_20210327100148538)
+ 前提条件：{{c1::必须重复接口的泛型类型，或者必须指定基类的类型}}
  + 必须重复接口的泛型类型: {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322183019.png) }}
  + 指定基类的类型: {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322183040.png) }}
+ 部分泛型继承：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322183235.png)}}

### 泛型类的静态成员 [ ](C#_20210327100148541)
+ 需注意的点:{{c1::泛型类的静态成员只能在类的一个实例中共享。}}
+ 图示:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322183449.png)}}

### 协变和抗变 [ ](C#_20210327100148543)
+ 定义：{{c1::.net中**参数类型**是**抗变的**,方法**返回类型**是**协变的**。}}
+ 如果泛型类型用`in`关键字标注，{{c1:: 泛型接口就是**抗变的**。这样，接口只能把泛型类型T用作其方法的**参数**输入 }}
+ 如果泛型类型用`out`关键字标注，{{c1:: 泛型接口就是**协变的**。这也意味着**返回类型**只能是T }}
## 第6章 运算符和类型强制转换 [ ](C#_20210327100148546)

### 带委托的泛型方法 [ ](C#_20210327100148548)
+ 调用图示：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323082215.png)
+ 实现图示:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323082140.png) }}

### 溢出检查 [ ](C#_20210327100148552)
+ checked关键字：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323082810.png) }}
+ 全局开启与unchecked：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323082836.png) }}

### 常用运算符 [ ](C#_20210327100148556)
+ `sizeof`：{{c1::运算符可以确定栈中值类型需要的长度（单位是字节）}}
+ `typeof`: {{c1::typeof运算符返回一个表示特定类型的 System.Type对象。}}
+ `nameof`: {{c1::该运算符接受一个符号、属性或方法，并返回其名称。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323083840.png)}}
+ `??`：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323084021.png) }}


### 空值条件运算符处理空值 [ ](C#_20210327100148558)
+ 空值条件运算符：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323131158.png)}}
+ 使用空值条件运算简化以下代码：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323133658.png)
  + 简化后：{{c1::`string city = p?.HomeAddress?.City;`}}
+ 判断数组是否为空：{{c1::`int x1 = arr?[0] ?? 0;`}}

### 比较对象的相等性 [ ](C#_20210327100148560)
1. `ReferenceEquals()`方法:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323164909.png)}}
2. `Equals()`虚方法
3. 静态`Equals()`方法
4. 比较运算符(`==`)

### 比较运算符的重载 [ ](C#_20210327100148564)
+ 语法：
  ```C#
  //{{c1::
        public static bool operator ==(Vector left, Vector right)
        {
            if (ReferenceEquals(left, right)) return true;

            return left.X == right.X && left.Y == right.Y && left.Z == right.Z;
        }

        public static bool operator !=(Vector lhs, Vector rhs) =>
           !(lhs == rhs);
  //}}
  ```
+ 注意：
  + {{c1:: 如果重载了`==`,也就必须重载`!=`，否则会产生编译器错误 }}
  + {{c1:: 重写`Equals`和`Gethashcode`方法。这些方法应该总是在重写`==`运算符时进行重写，否则编译器会报错}}


### 实现自定义的索引运算符 [ ](C#_20210327100148567)
+ 语法：
  ```C#
  //{{c1::
    public class PersonCollection
    {
        private Person[] _people;

        public PersonCollection(params Person[] people) =>
            _people = people.ToArray();

        public Person this[int index]
        {
            get => _people[index];
            set => _people[index] = value;
        }
  0
        public IEnumerable<Person> this[DateTime birthDay] => _people.Where(p => p.Birthday == birthDay);
    }
  //}}
  ```
### 用户定义的类型强制转换 [ ](C#_20210327100148570)
+ 定义不同结构或类的实例之间的类型强制转换是完全合法的，但有两点限制
  1. {{c1::如果某个类派生自另一个类，就不能定义这两个类之间的类型强制转换（这些类型的强制转换已经存在）。}}
  2. {{c1::类型强制转换必須在源数据类型或目标数据类型的内部定义。}}
+ **隐式**强制转换
  ```C#
  //{{c1::
  public static implicit operator float (Currency value) =>
    value.Dollars + (value.Cents / 100.0f);
  //}}
  ```
+ **显式**强制转换
  ```C#
  //{{c1::
  public static explicit operator Currency(float value)
  {
      checked
      {
          uint dollars = (uint)value;

          ushort cents = Convert.ToUInt16((value - dollars) * 100);
          return new Currency(dollars, cents);
      }
  }
  //}}
  ```


## 第7章 数组 [ ](C#_20210327100148573)

### `C#`数组声明与初始化 [ ](C#_20210327100148575)

+ 声明：{{c1::`int[] myArray;`}}
+ 几种初始化：
  1. {{c1::`int[] myArray = new int[4];`}}
  2. {{c1::`int[] myArray = new int[4]{1,2,3,4};`}}
  3. {{c1::`int[] myArray = new int[]{1,2,3,4};`}}
  4. {{c1::`int[] myArray = {1,2,3,4};`}}

### 创建数组：`CreateInstance()`,`SetValue()`,`GetValue()` [ ](C#_20210327100148577)

+ 使用示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323173155.png) }}
+ `setValue()`对应维数：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323173227.png) }}

### 复制数组 [ ](C#_20210327100148580)
+ 浅复制：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323214637.png)}}

### `IComparable<T>`与`IComparer<T>`区别： [ ](C#_20210327100148583)
+ 主要区别：{{c1::`IComparable<T>`比较方法为`CompareTo()`只有一个参数，`IComparer<T>`比较方法为`Compare`具有两个参数。类似java的`comparable`与`comparator`}}
+ `IComparer`数组排序：{{c1::`Array.Sort(persons,new PersonComparer(PersonCompareType.FirstName));`}}
+ `IComparable`数组排序：{{c1::`Array.Sort(persons);`}}

### foreach语句调用迭代器解析 [ ](C#_20210327100148586)
```C#
  foreach(var p in persons){
    Console.WriteLine(p);
  }
```
+ 以上foreach语句会解析为下面的代码段:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323215907.png)}}

### 迭代集合的不同方式 [ ](C#_20210327100148588)
+ 类得默认迭代：
  + 定义迭代器：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323221608.png) }}
  + 调用：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323221635.png) }}
+ 命名得迭代：
  + 定义迭代器：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323221741.png) }}
  + 调用：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323221814.png) }}

### 用 `yield return`返回枚举器 [ ](C#_20210327100148590)

+ 定义迭代器：
  ```C#
  //{{c1::
    public class GameMoves
    {
        private IEnumerator _cross;
        private IEnumerator _circle;

        public GameMoves()
        {
            _cross = Cross();
            _circle = Circle();
        }

        private int _move = 0;
        const int MaxMoves = 9;

        public IEnumerator Cross()
        {
            while (true)
            {
                Console.WriteLine($"Cross, move {_move}");
                if (++_move >= MaxMoves)
                    yield break;
                yield return _circle;
            }
        }

        public IEnumerator Circle()
        {
            while (true)
            {
                Console.WriteLine($"Circle, move {_move}");
                if (++_move >= MaxMoves)
                    yield break;
                yield return _cross;
            }
        }
    }
  //}}
  ```
+ 调用：
  ```C#
  //{{c1::
  var game = new GameMoves();
  IEnumerator enumerator = game.Cross();
  while (enumerator.MoveNext())
  {
      enumerator = enumerator.Current as IEnumerator;
  }
  //}}
  ```
### 结构比较 [ ](C#_20210327100148593)

+ `IStructuralequatable`接口:{{c1::用于比较两个元组或数组是否有相同的内容}}
+ `IStructuralComparable`接口:{{c1::用于给元组或数组排序}}

### 数组池 [ ](C#_20210327100148595)
+ 创建数组池:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210324100721.png)}}
+ 从池中租用内存:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210324100832.png)}}
+ 将内存返回给池:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210324100847.png)}}

## 第8章 委托、lambda 表达式和事件 [ ](C#_20210327100148598)

### 委托 [ ](C#_20210327100148600)
+ 作用: {{c1:: 当要把方法传送给其他方法时，就需要使用委托。}}
+ 声明委托:![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210324102639.png)
+ 使用委托:
  ```c#
  //{{c1::
    class Program
    {
        private delegate string GetAString();
        static void Main()
        {
            int x = 40;
            GetAString firstStringMethod = new GetAString(x.ToString);
            Console.WriteLine($"String is {firstStringMethod()}");

            var balance = new Currency(34, 50);
            firstStringMethod = balance.ToString;
            Console.WriteLine($"String is {firstStringMethod()}");

            firstStringMethod = new GetAString(Currency.GetCurrencyUnit);
            Console.WriteLine($"String is {firstStringMethod()}");
        }
    }
  //}}
  ```
  + 注意：{{c1::`C#`编译器会用`firstStringMethod.Invoke()`代替`firstStringMethod()`}}

### `Action<T>`和`Func<T>`委托 [ ](C#_20210327100148602)

+ `Action<T>`: {{c1:: 没有泛型参数的 `Action`类可调用没有参数的方法。 `Action<in T>`调用带一个参数的方法，`Action<in T1>`,inT2>调用带两个参数的方法， `Action<in T1,in T2,in T3,in T4,in TS,in T6,in T,in T8>`调用带8个参数的方法。 }}
+ `Func<T>`: {{c1:: `Func< out Tresult>`委托类型可以调用带返回类型且无参数的方法，`Func<in T, out Tresult>`调用带一个参数的方法， `Func<in TI,in T2,in T3,in T4,out Tresult>`调用带4个参数的方法。 }}

### 多播委托 [ ](C#_20210327100148605)

+ 多播委托调用：
  ```C#
  //{{c1::
    Action<double> operations = MathOperations.MultiplyByTwo;
    operations += MathOperations.Square;

    ProcessAndDisplayNumber(operations, 2.0);
    ProcessAndDisplayNumber(operations, 7.94);
    ProcessAndDisplayNumber(operations, 1.414);
    Console.WriteLine();
  //}}
  ```
+ 异常导致多播委托截止问题：
  ```C#
    //{{c1::
        static void One()
        {
            Console.WriteLine("One");
            throw new Exception("Error in one");
        }

        static void Two()
        {
            Console.WriteLine("Two");
        }

        static void Main(string[] args)
        {
            Action d1 = One;
            d1 += Two;
            Delegate[] delegates = d1.GetInvocationList();
            foreach (Action d in delegates)
            {
                try
                {
                    d();
                }
                catch (Exception)
                {
                    Console.WriteLine("Exception caught");
                }
            }
        }
  //}}
  ```

### C# 匿名方法与lambda表达式 [ ](C#_20210327100148609)
+ 语法：
  ```C#
  //{{c1::
          static void Main()
          {
              string mid = ", middle part,";

              Func<string, string> anonDel = delegate (string param)
              {
                  param += mid;
                  param += " and this was added to the string.";
                  return param;
              };
              Console.WriteLine(anonDel("Start of string"));
          }
  //}}
  ```

### C# 事件，发布/订阅机制（观察者模式） [ ](C#_20210327100148611)

+ 结合观察者模式，定义被观察者:
  ```C#
  //{{c1::
  public class CarDealer
  {
      public event EventHandler<CarInfoEventArgs> NewCarInfo;
  
      public void NewCar(string car)
      {
          Console.WriteLine($"CarDealer, new car {car}");
  
          NewCarInfo?.Invoke(this, new CarInfoEventArgs(car));
      }
  }
  //}}
  ```

  + 注意：invoke与被委托方法参数的对应。

+ 结合观察者模式，定义观察者：

  ```C#
  //{{c1::
  public class Consumer
  {
      private string _name;
  
      public Consumer(string name) => _name = name;
  
      public void NewCarIsHere(object sender, CarInfoEventArgs e) =>
          Console.WriteLine($"{_name}: car {e.Car} is new");
  }
  //}}
  ```


## 第9章 字符串和正则表达式  [ ](C#_20210327100148613)

### FormattableString [ ](C#_20210327100148615)
+ 作用:字符串中的插值管理
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210325115445.png)}}

### C# 正则表达式调用 [ ](C#_20210327100148619)
+ 主要名称空间:{{c1::`using System.Text.RegularExpressions;`}}
+ 例：
  ```C#
  //{{c1::
        public static void Find1(string text)
        {
            Console.WriteLine("Find1\n");
            const string pattern = "ion";
            MatchCollection matches = Regex.Matches(text, pattern,
                                                    RegexOptions.IgnoreCase |
                                                    RegexOptions.ExplicitCapture);
            Console.WriteLine($"Original text was: \n\n{text}\n");
            Console.WriteLine($"No. of matches: {matches.Count}");

            foreach (Match nextMatch in matches)
            {
                int index = nextMatch.Index;
                string result = nextMatch.ToString();
                int charsBefore = (index < 5) ? index : 5;
                int fromEnd = text.Length - index - result.Length;
                int charsAfter = (fromEnd < 5) ? fromEnd : 5;
                int charsToDisplay = charsBefore + charsAfter + result.Length;

                Console.WriteLine($"Index: {index}, \tString: {result}, \t" +
                  $"{text.Substring(index - charsBefore, charsToDisplay)}");
            }
        }
  //}}
  ```

## 第10章 集合 [ ](C#_20210327100148621)

### `List<T>` [ ](C#_20210327100148624)

+ 创建列表:
  ```C# 
  //{{c1::
  var intList = new List<int>();
  var racers = new List<Racer>();
  List<int> intList = new List<int>(10);
  //}}
  ```
+ 获取和设置集合的属性：{{c1::`intList.Capacity = 20;`}}
+ 获取集合元素个数：{{c1::`intList.Count`}}
+ 缩减集合空白空间：{{c1::`intList.Count`}}
+ 集合初始值设定：
  ```C# 
  //{{c1::
  var intlist = new List<int>()(1, 2);
  var stringlist = new List<string>()("one","two"):
  //}}
  ```
+ 添加元素：
  ```C# 
  //{{c1::
  var graham = new Racer(7, "Graham", "Hill", "UK", 14);
  var emerson = new Racer(13, "Emerson", "Fittipaldi", "Brazil", 14);
  var mario = new Racer(16, "Mario", "Andretti", "USA", 12);

  var racers = new List<Racer>(20) { graham, emerson, mario };
  racers.Add(new Racer(24, "Michael", "Schumacher", "Germany", 91));
  racers.Add(new Racer(27, "Mika", "Hakkinen", "Finland", 20));
  racers.AddRange(new Racer[] {
      new Racer(14, "Niki", "Lauda", "Austria", 25),
      new Racer(21, "Alain", "Prost", "France", 51)});

  // insert elements
  racers.Insert(3, new Racer(6, "Phil", "Hill", "USA", 3));

  // accessing elements
  for (int i = 0; i < racers.Count; i++)
  {
      Console.WriteLine(racers[i]);
  }

  foreach (var r in racers)
  {
      Console.WriteLine(r);
  }
  //}}
  ```
+ 查找元素:
  + `IndexOf`: {{c1::`int index1 = racers.IndexOf(mario);`}}
  + `FindIndex`: {{c1::`int index2 = racers.FindIndex(new FindCountry("Finland").FindCountryPredicate);`}}
  + `FindIndex`: {{c1::`int index3 = racers.FindIndex(r => r.Country == "Finland");`}}
  + `Find`: {{c1::`Racer racer = racers.Find(r => r.FirstName == "Niki");`}}
  + `FindAll`: {{c1::`List<Racer> bigWinners = racers.FindAll(r => r.Wins > 20);`}}
+ 删除元素:
  ```C#
  //{{c1::
  if (!racers.Remove(graham)){
      Console.WriteLine("object not found in collection");
  }
  //}}
  ```
+ 只读集合：{{c1::`List<T>`集合的`AsReadOnly()`方法返回`ReadonlyCollection<T>`类型的对象}}


### `Queue<T>`类的常用方法 [ ](C#_20210327100148626)
+ `Count`: {{c1:: Count属性返回队列中的元素个数 }}
+ `Enqueue`: {{c1:: Enqueue方法在队列一端添加一个元素 }}
+ `Dequeue`: {{c1:: Dequeue方法在队列的头部读取和删除元素。如果在调用 Dequeue方法时，队列中不再有元素，就抛出一个 Invalidoperationexception类型的异常 }}
+ `Peek`: {{c1:: Peck()方法从队列的头部读取一个元素，但不删除它 }}
+ `TrimExcess`: {{c1:: TrimExcess方法重新设置队列的容量。 Dequeue方法从队列中删除元素，但它不会重新设置队列的容量。要从队列的头部去除空元素，应使用 TrimExcess方法 }}

### `Stack<T>`类常用方法 [ ](C#_20210327100148628)
+ `Count` : {{c1::返回栈中的元素个数}}
+ `Push` : {{c1::在栈顶添加一个元素}}
+ `Pop` : {{c1::从栈顶删除一个元素，并返回该元素。如果栈是空的，就抛出`InvalidOperationException`异常}}
+ `Peek` : {{c1::返回顶的元素，但不删除它}}
+ `Contains` : {{c1::确定某个元素是否在栈中，如果是，就返回true}}

### `LinkedList<T>` [ ](C#_20210327100148630)
+ 作用: {{c1::`Linkedlist<T>`是一个双向链表，其元素指向它前面和后面的元素}}
+ `LinkedListNode<T>`定义了属性 : {{c1::`List`、`Next`、 `Previous`和 `Value`。}}

### `SortedList<TKey, TValue>` [ ](C#_20210327100148632)
+ 作用: {{c1::这个类**按照键**给元素排序。这个集合中的值和键都可以使用任意类型。}}
+ 简单例子：
  ```C#
  //{{c1::
    var books = new SortedList<string, string>();
    books.Add("Professional WPF Programming", "978–0–470–04180–2");
    books.Add("Professional ASP.NET MVC 5", "978–1–118-79475–3");

    books["Beginning C# 6 Programming"] = "978-1-119-09668-9";
    books["Professional C# 6 and .NET Core 1.0"] = "978-1-119-09660-3";

    foreach (KeyValuePair<string, string> book in books)
    {
        Console.WriteLine($"{book.Key}, {book.Value}");
    }

    foreach (string isbn in books.Values)
    {
        Console.WriteLine(isbn);
    }

    foreach (string title in books.Keys)
    {
        Console.WriteLine(title);
    }

    {
        string title = "Professional C# 8";
        if (!books.TryGetValue(title, out string isbn))
        {
            Console.WriteLine($"{title} not found");
        }
    }
  //}}
  ```

### 字典: `Dictionary<TKey, T Value>` [ ](C#_20210327100148636)
+ 作用：{{c1:: 字典表示一种非常复杂的数据结构，这种数据结构允许按照某个键来访问元素。字典也称为映射或散列表。字典的主要特性是能根据键快速查找值。也可以自由地添加和删除元素，这有点像`List<T>`类，但没有在内存中移动后续元素的性能开销。 }}
+ 初始化：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210326092509.png)}}
+ 字段键的限制: {{c1:: 用作字典中键的类型必须重写 `Object`类的`GetHashCode()`方法。只要字典类需要确定元素的位置，它就要调用`GetHashCode`方法。}}
+ 注意: {{c1:: 字典的性能取决于 Gethash Codeo方法的实现代码 }}
+ `Sorteddictionary.<TKey, Tvalue>`: {{c1:: 是一个二叉搜索树，其中的元素根据键排序。该键类型必须实现`Icomparable<TKey>`接口。如果键的类型不能排序，则还可以创建一个实现了`IComparer<TKey>`接口的比较器，将比较器用作有序字典的构造函数的一个参数 }}

### Lookup类 [ ](C#_20210327100148638)

+ 作用：{{c1:: `Dictionary<Tkey, Tvalue>`类支持每个键关联一个值。 `Lookup<Tkey, Telement>`类非常类似于`Dictionary<Tkey, Tvalue>`类，但把键映射到一个值集合上。 }}
+ 注意:{{c1:: `Lookup<Tke, Telement>`类不能像一般的字典那样创建，而必须调用`ToLookup()`方法，该方法返回一个`Lookup<TKey, Telement>`对象。 `ToLookup()`方法是一个扩展方法，它可以用于实现`IEnumerable<T>`接口的所有类。 }}
+ 使用例：
  ```C#
  //{{c1::
    var racers = new List<Racer>();
    racers.Add(new Racer(26, "Jacques", "Villeneuve", "Canada", 11));
    racers.Add(new Racer(18, "Alan", "Jones", "Australia", 12));
    racers.Add(new Racer(11, "Jackie", "Stewart", "United Kingdom", 27));
    racers.Add(new Racer(15, "James", "Hunt", "United Kingdom", 10));
    racers.Add(new Racer(5, "Jack", "Brabham", "Australia", 14));

    var lookupRacers = racers.ToLookup(r => r.Country);

    foreach (Racer r in lookupRacers["Australia"])
    {
        Console.WriteLine(r);
    }
  //}}
  ```

### 集：Set [ ](C#_20210327100148641)
+ 作用：{{c1:: .NET Core包含两个集(`Hashset<T>`和`Sortedset<T>`),它们都实现`ISet<T>`接口。`Hashset<T>`集包含不重复元素的无序列表，`Sortedset<T>`集包含不重复元素的有序列表 }}
+ 使用例：
```C#
//{{c1::
  var companyTeams = new HashSet<string>() { "Ferrari", "McLaren", "Mercedes" };
  var traditionalTeams = new HashSet<string>() { "Ferrari", "McLaren" };
  var privateTeams = new HashSet<string>() { "Red Bull", "Lotus", "Toro Rosso", "Force India", "Sauber" };

  if (privateTeams.Add("Williams"))
      Console.WriteLine("Williams added");
  if (!companyTeams.Add("McLaren"))
      Console.WriteLine("McLaren was already in this set");

  if (traditionalTeams.IsSubsetOf(companyTeams))
  {
      Console.WriteLine("traditionalTeams is subset of companyTeams");
  }

  if (companyTeams.IsSupersetOf(traditionalTeams))
  {
      Console.WriteLine("companyTeams is a superset of traditionalTeams");
  }

  traditionalTeams.Add("Williams");
  if (privateTeams.Overlaps(traditionalTeams))
  {
      Console.WriteLine("At least one team is the same with traditional and private teams");
  }

  var allTeams = new SortedSet<string>(companyTeams);
  allTeams.UnionWith(privateTeams);
  allTeams.UnionWith(traditionalTeams);

  Console.WriteLine();
  Console.WriteLine("all teams");
  foreach (var team in allTeams)
  {
      Console.WriteLine(team);
  }

  allTeams.ExceptWith(privateTeams);
  Console.WriteLine();
  Console.WriteLine("no private team left");
  foreach (var team in allTeams)
  {
      Console.WriteLine(team);
  }
//}}
```

## 第11章 特殊的集合  [ ](C#_20210327100148643)

### BitArray类 [ ](C#_20210327100148645)

+ 常用方法:
  + `Count Length`:{{c1:: `Count`和`Length`属性的`get`访问器返回数组中的位数。使用 Length属性还可以定义新的数组大小重新设置集合的大小 }}
  + `Item Get Set`:{{c1:: 可以使用索引器读写数组中的位。索引器是布尔类型。除了使用素引器之外，还可以使用Get()和Set()方法访问数组中的位 }}
  + `SetAll`: {{c1:: 根据传送给该方法的参数，`SetAll`方法设置所有位的值 }} 
  + `Not`: {{c1:: `Not()`方法对数组中所有位的值取反 }}
  + `And Or Xor`: {{c1:: 使用`And()`、`Or()`和`Xor()`方法，可以合并两个`Bitarray`对象 }}
+ 注意：{{c1:: 如果事先不知道需要的位数，就可以使用`Bitarray`类，它可以包含非常多的位。`BitVector32`结构是基于栈的，因此比较快。 `BitVector32`结构仅包含32位，它们存储在一个整数中。}}
+ BitArray类使用例：
```C#
//{{c1::
var bits1 = new BitArray(9);
bits1.SetAll(true);
bits1.Set(1, false);
bits1[5] = false;
bits1[7] = false;
Console.Write("initialized: ");
Console.WriteLine(bits1.GetBitsFormat());
Console.WriteLine("_________________________");

Console.Write("not ");
Console.Write(bits1.GetBitsFormat());
bits1.Not();
Console.Write(" = ");
Console.WriteLine(bits1.GetBitsFormat());
Console.WriteLine("_________________________");

var bits2 = new BitArray(bits1);
bits2[0] = true;
bits2[1] = false;
bits2[4] = true;
Console.Write($"{bits1.GetBitsFormat()} OR {bits2.GetBitsFormat()}");
Console.Write(" = ");
bits1.Or(bits2);
Console.WriteLine(bits1.GetBitsFormat());
Console.WriteLine("_________________________");

Console.Write($"{bits2.GetBitsFormat()} AND {bits1.GetBitsFormat()}");
Console.Write(" = ");
bits2.And(bits1);
Console.WriteLine(bits2.GetBitsFormat());

Console.WriteLine("_________________________");
Console.Write($"{bits1.GetBitsFormat()} XOR {bits2.GetBitsFormat()}");
bits1.Xor(bits2);
Console.Write(" = ");
Console.WriteLine(bits1.GetBitsFormat());
Console.WriteLine("_________________________");
//}}
```

### BitVector32 [ ](C#_20210327100148647)

+ 作用：{{c1:: 用一个32位的数来表示数据，那么初始化BitVector32结构时必须制定一个最初值，用户可以传入一个int或者另一个已经存在的BitVector32来构造一个新的BitVector32. }}
+ 创建掩码用于设置位：
  ```C#
  //{{c1::
  var bits1 = new BitVector32();
  int bit1 = BitVector32.CreateMask();
  int bit2 = BitVector32.CreateMask(bit1);
  int bit3 = BitVector32.CreateMask(bit2);
  int bit4 = BitVector32.CreateMask(bit3);
  int bit5 = BitVector32.CreateMask(bit4);

  bits1[bit1] = true;
  bits1[bit2] = false;
  bits1[bit3] = true;
  bits1[bit4] = true;
  bits1[bit5] = true;
  Console.WriteLine(bits1);
  //}}
  ```
+ 创建片段用以访问位
  ```C#
  //{{c1::
  int received = 0x79ab_cdef;
  BitVector32 bits2 = new BitVector32(received);
  Console.WriteLine(bits2);
  BitVector32.Section sectionA = BitVector32.CreateSection(0xfff);
  BitVector32.Section sectionB = BitVector32.CreateSection(0xff, sectionA);
  BitVector32.Section sectionC = BitVector32.CreateSection(0xf, sectionB);
  BitVector32.Section sectionD = BitVector32.CreateSection(0x7, sectionC);
  BitVector32.Section sectionE = BitVector32.CreateSection(0x7, sectionD);
  BitVector32.Section sectionF = BitVector32.CreateSection(0x3, sectionE);
  
  Console.WriteLine($"Section A: {bits2[sectionA].ToBinaryString()}");
  Console.WriteLine($"Section B: {bits2[sectionB].ToBinaryString()}");
  Console.WriteLine($"Section C: {bits2[sectionC].ToBinaryString()}");
  Console.WriteLine($"Section D: {bits2[sectionD].ToBinaryString()}");
  Console.WriteLine($"Section E: {bits2[sectionE].ToBinaryString()}");
  Console.WriteLine($"Section F: {bits2[sectionF].ToBinaryString()}");
  //}}
  ```

### 可观察的集合:`ObservableCollection<T>` [ ](C#_20210327100148649)
+ 主要思路： 
  1. {{c1:: `CollectionChanged`事件的注册 }}
  2. {{c1:: `NotifyCollectionChangedEventArgs`参数含义 }}
```C#
//{{c1::
namespace ObservableCollectionSample
{
    class Program
    {
        static void Main()
        {
            var data = new ObservableCollection<string>();
            
            data.CollectionChanged += Data_CollectionChanged;
            data.Add("One");
            data.Add("Two");
            data.Insert(1, "Three");
            data.Remove("One");

            data.CollectionChanged -= Data_CollectionChanged;

            Console.ReadLine();
        }

        public static void Data_CollectionChanged(object sender, NotifyCollectionChangedEventArgs e)
        {
            Console.WriteLine($"action: {e.Action.ToString()}");

            if (e.OldItems != null)
            {
                Console.WriteLine($"starting index for old item(s): {e.OldStartingIndex}");
                Console.WriteLine("old item(s):");
                foreach (var item in e.OldItems)
                {
                    Console.WriteLine(item);
                }
            }
            if (e.NewItems != null)
            {
                Console.WriteLine($"starting index for new item(s): {e.NewStartingIndex}");
                Console.WriteLine("new item(s): ");
                foreach (var item in e.NewItems)
                {
                    Console.WriteLine(item);
                }
            }
            Console.WriteLine();
        }
    }
}
//}}
```

### 不可变集合:ImmutableList [ ](C#_20210327100148652)
+ 创建不可变集合:
```C#
//{{c1::
var accounts = new List<Account>() {
    new Account("Scrooge McDuck", 667377678765m),
    new Account("Donald Duck", -200m),
    new Account("Ludwig von Drake", 20000m)
};
ImmutableList<Account> immutableAccounts = accounts.ToImmutableList();
//}}
```
+ 注意：{{c1::`Add、 Addrange、 Remove、 Removeat、 Removerange、 Replace`等方法，会返回一个新的不可变集合。}}
+ 使用构造器构造不可变集合:
```C#
//{{c1::
  public static void UsingABuilder(ImmutableList<Account> immutableAccounts)
  {
      ImmutableList<Account>.Builder builder = immutableAccounts.ToBuilder();
      for (int i = 0; i < builder.Count; i++)
      {
          Account a = builder[i];
          if (a.Amount > 0)
          {
              builder.Remove(a);
          }
      }
      ImmutableList<Account> overdrawnAccounts = builder.ToImmutable();
      overdrawnAccounts.ForEach(a => Console.WriteLine($"{a.Name} {a.Amount}"));
  }
//}}
```

## 第12章 LINQ [ ](C#_20210327100148654)

### LINQ概述 [ ](C#_20210327100148656)
+ `LINQ`：{{c1::`Language Integrated Query`,语言集成查询}}
+ 实体查询例子：
  ```C#
  //{{c1::
    static void LINQQuery()
    {
        var query = from r in Formula1.GetChampions()
                    where r.Country == "Brazil"
                    orderby r.Wins descending
                    select r;

        foreach (var r in query)
        {
            Console.WriteLine($"{r:A}");
        }
        Console.WriteLine();
    }
  //}}
  ```
+ 相应的拓展方法如下：
  ```C#
  //{{c1::
  static void ExtensionMethods()
  {
      var champions = new List<Racer>(Formula1.GetChampions());
      IEnumerable<Racer> brazilChampions =
          champions.Where(r => r.Country == "Brazil")
              .OrderByDescending(r => r.Wins)
              .Select(r => r);

      foreach (Racer r in brazilChampions)
      {
          Console.WriteLine($"{r:A}");
      }
      Console.WriteLine();
  }
  //}}
  ```
  
### LINQ 推迟查询的执行 [ ](C#_20210327100148659)
+ 作用：{{c1::在运行期间定义查询表达式时，查询不会运行。査询只会在迭代数据项时运行。}}
  ```C#
  //{{c1::
  static void DeferredQuery()
  {
      var names = new List<string> { "Nino", "Alberto", "Juan", "Mike", "Phil" };

      var namesWithJ = from n in names
                        where n.StartsWith("J")
                        orderby n
                        select n;

      Console.WriteLine("First iteration");
      foreach (string name in namesWithJ)
      {
          Console.WriteLine(name);
      }
      Console.WriteLine();

      names.Add("John");
      names.Add("Jim");
      names.Add("Jack");
      names.Add("Denny");

      Console.WriteLine("Second iteration");
      foreach (string name in namesWithJ)
      {
          Console.WriteLine(name);
      }
      Console.WriteLine();
  }
  //}}
  ```

### 标准的查询操作符LINQ：`where` `OfType` `from`  [ ](C#_20210327100148661)
+ where的使用：
  ```C#
  // 找出赢得至少15场比赛的巴西和奥地利赛车手
  //{{c1::
  public static void Filtering()
  {
      var racers = from r in Formula1.GetChampions()
                    where r.Wins > 15 && (r.Country == "Brazil" || r.Country == "Austria")
                    select r;

      foreach (var r in racers)
      {
          Console.WriteLine($"{r:A}");
      }
  }
  //}}
  // 使用索引返回姓氏以A开头、索引为偶数的赛车手
  //{{c1::
  public static void FilteringWithIndex()
  {
      var racers = Formula1.GetChampions()
          .Where((r, index) => r.LastName.StartsWith("A") && index % 2 != 0);
      foreach (var r in racers)
      {
          Console.WriteLine($"{r:A}");
      }
  }
  //}}
  // 拓展方法版
  //{{c1::
  public static void FilteringWithMethods()
  {
      var racers = Formula1.GetChampions()
          .Where(r => r.Wins > 15 && (r.Country == "Brazil" || r.Country == "Austria"));

      foreach (var r in racers)
      {
          Console.WriteLine($"{r:A}");
      }
  }
  //}}
  ```
+ OfType的使用：
  ```C#
  //{{c1::
  public static void TypeFiltering()
  {
      object[] data = { "one", 2, 3, "four", "five", 6 };
      var query = data.OfType<string>();
      foreach (var s in query)
      {
          Console.WriteLine(s);
      }
  }
  //}}
  ```
+ 复合的from子句（SelectMany的使用）：筛选驾驶法拉利的所有冠军
  ```C#
    //LINQ实现
    //{{c1::
    public static void CompoundFrom()
    {
        var ferrariDrivers = from r in Formula1.GetChampions()
                              from c in r.Cars
                              where c == "Ferrari"
                              orderby r.LastName
                              select $"{r.FirstName} {r.LastName}";

        foreach (var racer in ferrariDrivers)
        {
            Console.WriteLine(racer);
        }
    }
    //}}

    //拓展方法实现
    //{{c1::
    //SelectMany迭代序列的序列。
    public static void CompoundFromWithMethods()
    {
        var ferrariDrivers = Formula1.GetChampions()
            .SelectMany(r => r.Cars, (r1, cars) => new { Racer1 = r1, Cars1 = cars })
            .Where(item => item.Cars1.Contains("Ferrari"))
            .OrderBy(item => item.Racer1.LastName)
            .Select(item => $"{item.Racer1.FirstName} {item.Racer1.LastName}");

        foreach (var racer in ferrariDrivers)
        {
            Console.WriteLine(racer);
        }
    }
    //}}
  ```

### 标准的查询操作符LINQ： `orderby`排序 [ ](C#_20210327100148663)
+ 例子：赛车手按照赢得比赛的次数进行降序排序
  + LINQ实现：
    ```C#
    //{{c1::
    var racers = from r in Formula1.GetChampions()
                where r.Country == "Brazil"
                orderby r.Wins descending
                select r;
    //}}
    ```
  + 拓展方法实现：
    ```C#
    //{{c1::
    var racers = Formula1.GetChampions()
        .Where(r => r.Country == "Brazil")
        .OrderByDescending(r => r.Wins);
    //}}
    ```
+ 多组排序：所有的赛车手先按照国家排序，再按照姓氏排序，最后按照名字排序,返回前10个结果
  + LINQ实现：
    ```C#
    //{{c1::
    var racers = (from r in Formula1.GetChampions()
                  orderby r.Country, r.LastName, r.FirstName
                  select r).Take(10);
    //}}
    ```
  + 拓展方法实现：
    ```C#
    //{{c1::
    var racers = Formula1.GetChampions()
                    .OrderBy(r => r.Country)
                    .ThenBy(r => r.LastName)
                    .ThenBy(r => r.FirstName)
                    .Take(10);
    //}}
    ```


### 标准的查询操作符LINQ： `group`分组 [ ](C#_20210327100148666)

+ 现在一级方程式冠军应按照国家分组，并列出冠军数大于2的国家。
  + LINQ实现：
    ```C#
    //{{c1::
    var countries = from r in Formula1.GetChampions()
                group r by r.Country into g
                orderby g.Count() descending, g.Key
                where g.Count() >= 2
                select new
                {
                    Country = g.Key,
                    Count = g.Count()
                };
    //}}
    ```
  + 使用let的LINQ实现：
    ```C#
    //{{c1::
    var countries = from r in Formula1.GetChampions()
                    group r by r.Country into g
                    let count = g.Count()
                    orderby count descending, g.Key
                    where count >= 2
                    select new
                    {
                        Country = g.Key,
                        Count = count
                    };
    //}}
    ```
  + 拓展方法实现：
    ```C#
    //{{c1::
    var countries = Formula1.GetChampions()
      .GroupBy(r => r.Country)
      .OrderByDescending(g => g.Count())
      .ThenBy(g => g.Key)
      .Where(g => g.Count() >= 2)
      .Select(g => new
      {
          Country = g.Key,
          Count = g.Count()
      });
    //}}
    ```
  + 基于匿名类型的拓展方法实现：
    ```C#
    //{{c1::
    var countries = Formula1.GetChampions()
      .GroupBy(r => r.Country)
      .Select(g => new { Group = g, Count = g.Count() })
      .OrderByDescending(g => g.Count)
      .ThenBy(g => g.Group.Key)
      .Where(g => g.Count >= 2)
      .Select(g => new
      {
          Country = g.Group.Key,
          g.Count
      });
    //}}
    ```

### 标准的查询操作符LINQ：嵌套对象分组 [ ](C#_20210327100148668)
+ 例子：现在一级方程式冠军应按照国家分组，并列出冠军数大于2的国家，**以及赛车手的名序列**
+ LINQ实现：
```c# 
 //{{c1::
  var countries = from r in Formula1.GetChampions()
                  group r by r.Country into g
                  let count = g.Count()
                  orderby count descending, g.Key
                  where count >= 2
                  select new
                  {
                      Country = g.Key,
                      Count = count,
                      Racers = from r1 in g
                                orderby r1.LastName
                                select r1.FirstName + " " + r1.LastName
                  };
 //}}
```
+ 拓展方法版：
```c# 
 //{{c1::
  var countries = Formula1.GetChampions()
      .GroupBy(r => r.Country)
      .Select(g => new
      {
          Group = g,
          g.Key,
          Count = g.Count()
      })
      .OrderByDescending(g => g.Count)
      .ThenBy(g => g.Key)
      .Where(g => g.Count >= 2)
      .Select(g => new
      {
          Country = g.Key,
          g.Count,
          Racers = g.Group.OrderBy(r => r.LastName).Select(r => r.FirstName + " " + r.LastName)
      });
  //}}
```

### 标准的查询操作符LINQ：内连接 [ ](C#_20210327100148670)
+ 示例：显示了在同时有了赛车手冠军和车队冠军的前10年
  + LINQ实现：
    ```C#
    //{{c1::
      var racers = from r in Formula1.GetChampions()
                    from y in r.Years
                    select new
                    {
                        Year = y,
                        Name = r.FirstName + " " + r.LastName
                    };

      var teams = from t in Formula1.GetConstructorChampions()
                  from y in t.Years
                  select new
                  {
                      Year = y,
                      t.Name
                  };

      var racersAndTeams =
            (from r in racers
              join t in teams on r.Year equals t.Year
              orderby t.Year
              select new
              {
                  r.Year,
                  Champion = r.Name,
                  Constructor = t.Name
              }).Take(10);
    //}}
    ```
  + 拓展方法版：
    ```C#
    //{{c1::
    var racers = Formula1.GetChampions()
    .SelectMany(r => r.Years, (r1, year) =>
    new
    {
        Year = year,
        Name = $"{r1.FirstName} {r1.LastName}"
    });

    var teams = Formula1.GetConstructorChampions()
        .SelectMany(t => t.Years, (t, year) =>
        new
        {
            Year = year,
            t.Name
        });

    var racersAndTeams = racers.Join(
        teams,
        r => r.Year,
        t => t.Year,
        (r, t) =>
            new
            {
                r.Year,
                Champion = r.Name,
                Constructor = t.Name
            }).OrderBy(item => item.Year).Take(10);
    //}}
    ```


### 标准的查询操作符LINQ：内连接 左外连接实现： [ ](C#_20210327100148673)
+ LINQ实现：
  ```C#
  //{{c1::
  var racersAndTeams =
  (from r in racers
    join t in teams on r.Year equals t.Year into rt
    from t in rt.DefaultIfEmpty()
    orderby r.Year
    select new
    {
        r.Year,
        Champion = r.Name,
        Constructor = t == null ? "no constructor championship" : t.Name
    }).Take(10);
  //}}	
  ```
+ 拓展方法版：
  ```C#
  //{{c1::
  var racersAndTeams =
    racers.GroupJoin(
        teams,
        r => r.Year,
        t => t.Year,
        (r, ts) => new
        {
            Year = r.Year,
            Champion = r.Name,
            Constructors = ts
        })
        .SelectMany(
            item => item.Constructors.DefaultIfEmpty(),
            (r, t) => new
            {
                Year = r.Year,
                Champion = r.Champion,
                Constructor = t?.Name ?? "no constructor championship"
            });
  //}}
  ```

### 标准的查询操作符LINQ：组连接 [ ](C#_20210327100148676)
+ LINQ实现:
  ```C#
  //{{c1::
  var racers = from cs in Formula1.GetChampionships()
                from r in new List<(int Year, int Position, string FirstName, string LastName)>()
                {
                    (cs.Year, Position: 1, FirstName: cs.First.FirstName(), LastName: cs.First.LastName()),
                    (cs.Year, Position: 2, FirstName: cs.Second.FirstName(), LastName: cs.Second.LastName()),
                    (cs.Year, Position: 3, FirstName: cs.Third.FirstName(), LastName: cs.Third.LastName())
                }
                select r;
  var q = (from r in Formula1.GetChampions()
            join r2 in racers on
            (
                r.FirstName,
                r.LastName
            )
            equals
            (
                r2.FirstName,
                r2.LastName
            )
            into yearResults
            select
            (
                r.FirstName,
                r.LastName,
                r.Wins,
                r.Starts,
                Results: yearResults
            ));

  foreach (var r in q)
  {
      Console.WriteLine($"{r.FirstName} {r.LastName}");
      foreach (var results in r.Results)
      {
          Console.WriteLine($"\t{results.Year} {results.Position}");
      }
  }
  //}}
  ```
+ 拓展方法实现：
  ```C#
  //{{c1::
  var racers = Formula1.GetChampionships()
  .SelectMany(cs => new List<(int Year, int Position, string FirstName, string LastName)>
  {
      (cs.Year, Position: 1, FirstName: cs.First.FirstName(), LastName: cs.First.LastName()),
      (cs.Year, Position: 2, FirstName: cs.Second.FirstName(), LastName: cs.Second.LastName()),
      (cs.Year, Position: 3, FirstName: cs.Third.FirstName(), LastName: cs.Third.LastName())
  });

  var q = Formula1.GetChampions()
      .GroupJoin(racers,
          r1 => (r1.FirstName, r1.LastName),
          r2 => (r2.FirstName, r2.LastName),
          (r1, r2s) => (r1.FirstName, r1.LastName, r1.Wins, r1.Starts, Results: r2s));

  foreach (var r in q)
  {
      Console.WriteLine($"{r.FirstName} {r.LastName}");
      foreach (var results in r.Results)
      {
          Console.WriteLine($"{results.Year} {results.Position}");
      }
  }
  //}}
  ```

### 标准的查询操作符LINQ：集合操作 [ ](C#_20210327100148678)
+ 集合操作拓展方法：{{c1::`Distinct()、Union()、Intersect()、Except()`都是集合操作}}
+ 使用例：
  ```C#
  //{{c1::
  IEnumerable<Racer> racersByCar(string car) =>
      from r in Formula1.GetChampions()
      from c in r.Cars
      where c == car
      orderby r.LastName
      select r;
  
  Console.WriteLine("World champion with Ferrari and McLaren");
  foreach (var racer in racersByCar("Ferrari").Intersect(racersByCar("McLaren")))
  {
      Console.WriteLine(racer);
  }
  //}}
  ```

### 标准的查询操作符LINQ：合并操作 [ ](C#_20210327100148680)

+ zip方法作用：{{c1::第一个集合中的第一项会与第二个集合中的第一项合并，第一个集合中的第二项会与第二个集合中的第二项合并，以此类推。如果两个序列的项数不同，`Zip()`方法就在到达较小集合的末尾时停止。}}
+ 使用例：
  ```C#
  //{{c1::
  var racerNames = from r in Formula1.GetChampions()
                  where r.Country == "Italy"
                  orderby r.Wins descending
                  select new
                  {
                      Name = r.FirstName + " " + r.LastName
                  };
  var racerNamesAndStarts = from r in Formula1.GetChampions()
                            where r.Country == "Italy"
                            orderby r.Wins descending
                            select new
                            {
                                r.LastName,
                                r.Starts
                            };
    var racers = racerNames.Zip(racerNamesAndStarts, (first, second) => first.Name + ", starts: " + second.Starts);
    foreach (var r in racers)
    {
        Console.WriteLine(r);
    }
  //}}
  ```

### 标准的查询操作符LINQ：使用Skip与Take实现集合分页 [ ](C#_20210327100148682)
+ 使用例：
```C#
//{{c1::
  public static void Partitioning()
  {
      int pageSize = 5;

      int numberPages = (int)Math.Ceiling(Formula1.GetChampions().Count() /
            (double)pageSize);

      for (int page = 0; page < numberPages; page++)
      {
          Console.WriteLine($"Page {page}");

          var racers =
              (from r in Formula1.GetChampions()
              orderby r.LastName, r.FirstName
              select r.FirstName + " " + r.LastName).
              Skip(page * pageSize).Take(pageSize);

          foreach (var name in racers)
          {
              Console.WriteLine(name);
          }
          Console.WriteLine();
      }
  }
//}}
```
+ 提升：{{c1::使用`Takewhile()`和`SkipWhile()`扩展方法，还可以传递一个谓词，根据谓词的结果提取或跳过某些项。}}


### 标准的查询操作符LINQ：聚合操作符

+ 作用：{{c1::聚合操作符(如 Count、Sum、Min、Max、 Average和 Aggregate操作符)不返回一个序列，而返回一个值。}}
+ 使用例：
  ```C#
  //{{c1::
  public static void AggregateSum()
  {
      var countries = (from c in
                            from r in Formula1.GetChampions()
                            group r by r.Country into c
                            select new
                            {
                                Country = c.Key,
                                Wins = (from r1 in c
                                        select r1.Wins).Sum()
                            }
                        orderby c.Wins descending, c.Country
                        select c).Take(5);

      foreach (var country in countries)
      {
          Console.WriteLine($"{country.Country} {country.Wins}");
      }
  }

  public static void AggregateCount()
  {
      var query = from r in Formula1.GetChampions()
                  let numberYears = r.Years.Count()
                  where numberYears >= 3
                  orderby numberYears descending, r.LastName
                  select new
                  {
                      Name = r.FirstName + " " + r.LastName,
                      TimesChampion = numberYears
                  };

      foreach (var r in query)
      {
          Console.WriteLine($"{r.Name} {r.TimesChampion}");
      }
  }
  //}}
  ```

### 标准的查询操作符LINQ：转换操作符

+ `ToList`示例：
  ```C#
  //{{c1::
  List<Racer> racers = (from r in Formula1.GetChampions()
                        where r.Starts > 200
                        orderby r.Starts descending
                        select r).ToList();
  //}}
  ```
  + 注意：{{c1::调用`Tolist()`扩展方法，立即执行查询，得到的结果放在`List<T>`类中}}
+ `ToLook`示例：
  
  ```C#
  //{{c1::
  var racers = (from r in Formula1.GetChampions()
                from c in r.Cars
                select new
                {
                    Car = c,
                    Racer = r
                }).ToLookup(cr => cr.Car, cr => cr.Racer);
  //}}
  ```
  + 注意：{{c1:: `Dictionary<TKey, Tvalue>`类只支持一个健对应一个值。在`System.Linq`名称空间的类`Lookup<TKeyElemen>`类中，一个键可以对应多个值。}}
+ `Cast<T>`示例:
  ```C#
  //{{c1::
  var query = from r in list.Cast<Racer>()
              where r.Country == "USA"
              orderby r.Wins descending
              select r;
  //}}
  ```
  + 注意：{{c1:: 如果需要在非类型化的集合上(如 `Arraylist()`使用`LINQ`查询，就可以使用`Cast()`方法。}}

### 标准的查询操作符LINQ：生成操作符
+ `Range()`:{{c1::填充一个范围的数字}}
+ `Repeat()`:{{c1::方法返回一个迭代器，该迭代器把同一个值重复特定的次数。}}
+ `Empty()`:{{c1::返回一个不返回值的迭代器}}
+ 使用例：
  ```c#
  //{{c1::
  var values = Enumerable.Range(1, 20);
  foreach (var item in values)
  {
      Console.Write($"{item} ", item);
  }
  Console.WriteLine();
  //}}
  ```

### 标准的查询操作符LINQ：并行查询

+ LINQ使用：
  ```C#
  //{{c1::
  static void LinqQuery(IEnumerable<int> data)
  {
      Console.WriteLine(nameof(LinqQuery));
      var res = (from x in data.AsParallel()
                 where Math.Log(x) < 4
                 select x).Average();
      Console.WriteLine($"result from {nameof(LinqQuery)}: {res}");
      Console.WriteLine();
  }
  //}}
  ```
  + 注意:{{c1::`AsParallel()`的作用}}
+ 拓展方法例：
  ```C#
  //{{c1::
  static void ExtensionMethods(IEnumerable<int> data)
  {
      Console.WriteLine(nameof(ExtensionMethods));
      var res = data.AsParallel()
          .Where(x => Math.Log(x) < 4)
          .Select(x => x).Average();
          
      Console.WriteLine($"result from {nameof(ExtensionMethods)}: {res}");
      Console.WriteLine();
  }
  //}}
  ```
+ 分区器例：
  ```C#
  //{{c1::
  static void UseAPartitioner(IList<int> data)
  {
      Console.WriteLine(nameof(UseAPartitioner));
      var res = (from x in Partitioner.Create(data, loadBalance: true).AsParallel()
                where Math.Log(x) < 4
                select x).Average();
          
      Console.WriteLine($"result from {nameof(UseAPartitioner)}: {res}");
      Console.WriteLine();
  }
  //}}
  ```
  + 注意:{{c1::`Partitioner`的作用}}

### 标准的查询操作符LINQ：取消并行查询
+ 主要思路：{{c1::`CancellationTokenSource`创建`token,WithCancellation()`注册`token`，使用`CancellationTokenSource`实例`cancel()`方法}}
+ 使用例：
  ```C#
  //{{c1::
  Console.WriteLine(nameof(UseCancellation));
  var cts = new CancellationTokenSource();
  Task.Run(() =>
  {
      try
      {
          var res = (from x in data.AsParallel().WithCancellation(cts.Token)
                      where Math.Log(x) < 4
                      select x).Average();

          Console.WriteLine($"query finished, sum: {res}");
      }
      catch (OperationCanceledException ex)
      {
          Console.WriteLine(ex.Message);
      }
  });

  Console.WriteLine("query started");
  Console.Write("cancel? ");
  string input = Console.ReadLine();
  if (input.ToLower().Equals("y"))
  {
      cts.Cancel();
  }
  Console.WriteLine();
  //}}
  ```

## 第13章 C#函数式编程

### 实际例子：高阶函数以函数作为参数，或者返回一个函数，或者返回两个函数。在处理函数时，可以将两个函数合并到一个函数中。
+ 定义：
  ```C#
  //{{c1::
  public static Func<T1, TResult> Compose<T1, T2, TResult>(Func<T1, T2> f1, 
      Func<T2, TResult> f2) =>
      a => f2(f1(a));
  //}}
  ```
+ 调用：
  ```C#
  //{{c1::
  Func<int, int> f1 = x => x + 1;
  Func<int, int> f2 = x => x + 2;
  Func<int, int> f3 = Compose(f1, f2);
  var x1 = f3(39);
  WriteLine(x1);  //42
  //}}
  ```

### 本地函数  
+ 与lambda相比，本地函数语法更加简洁，例:
  ```C#
    //{{c1::
    //lambda实现：
    private static void IntroWithLambdaExpression()
    {
        Func<int, int, int> add = (x, y) =>
        {
            return x + y;
        };
        int result = add(37, 5);
        Console.WriteLine(result);
    }
    //本地函数实现：
    private static void IntroWithLocalFunctionsWithExpressionBodies()
    {
        int add(int x, int y) => x + y;

        int result = add(37, 5);
        Console.WriteLine(result);
    }
    //}}
  ```
+ 由于`yield`延迟执行问题，对空值的检查被延迟了，问题例：
  ```C# 
  //{{c1::
  public static IEnumerable<T> Where1<T>(this IEnumerable<T> source, Func<T, bool> predicate)
  {
      if (source == null) throw new ArgumentNullException(nameof(source));
      if (predicate == null) throw new ArgumentNullException(nameof(predicate));

      foreach (T item in source)
      {
          if (predicate(item))
          {
              yield return item;
          }
      }
  }

  private static void YieldSampleSimple()
  {
  #line 1000
      Console.WriteLine(nameof(YieldSampleSimple));
      try
      {
          string[] names = { "James", "Niki", "John", "Gerhard", "Jack" };
          var q = names.Where1(null);

          foreach (var n in q)  // callstack position for exception
          {
              Console.WriteLine(n);
          }
      }
      catch (ArgumentNullException ex)
      {
          Console.WriteLine(ex);
      }
      Console.WriteLine();
  }
  //}}
  ```
+ 由于`yield`延迟执行问题，对空值的检查被延迟了，本地函数解决例：
  ```C#
  //{{c1::
  public static IEnumerable<T> Where3<T>(this IEnumerable<T> source, Func<T, bool> predicate)
  {
      if (source == null) throw new ArgumentNullException(nameof(source));
      if (predicate == null) throw new ArgumentNullException(nameof(predicate));

      return Iterator();

      IEnumerable<T> Iterator()
      {
          foreach (T item in source)
          {
              if (predicate(item))
              {
                  yield return item;
              }
          }
      }
  }

  private static void YieldSampleWithPrivateMethod()
  {
      Console.WriteLine(nameof(YieldSampleWithPrivateMethod));
      try
      {
          string[] names = { "James", "Niki", "John", "Gerhard", "Jack" };
          var q = names.Where3(null);  // callstack position for exception

          foreach (var n in q)
          {
              Console.WriteLine(n);
          }
      }
      catch (ArgumentNullException ex)
      {
          Console.WriteLine(ex);
      }
      Console.WriteLine();
  }
  //}}
  ```

### 递归本地函数:实现快速排序
  ```C#
  //{{c1::
  public static void QuickSort<T>(T[] elements) where T : IComparable<T>
  {
      void Sort(int start, int end)
      {
          int i = start, j = end;
          var pivot = elements[(start + end) / 2];

          while (i <= j)
          {
              while (elements[i].CompareTo(pivot) < 0) i++;
              while (elements[j].CompareTo(pivot) > 0) j--;
              if (i <= j)
              {
                  T tmp = elements[i];
                  elements[i] = elements[j];
                  elements[j] = tmp;
                  i++;
                  j--;
              }
          }
          if (start < j) Sort(start, j);
          if (i < end) Sort(i, end);
      }
      Sort(0, elements.Length - 1);
  }
  //}}
  ```
### 元组
+ 定义：{{c1::使用数组可以组合相同类型的对象，而元组能够组合**不同类型**的对象。}}
+ 元组有助于减少以下2个需求
  1. {{c1::定义自定义类或结构，以返回多个值}}
  2. {{c1::定义参数，从方法中返回多个值}}

### 元组的声明和初始化
+ 完整声明：
  ```c#
  //{{c1::
  (string s, int i, Person p) t = ("magic", 42, new Person("Matthias", "Nagel"));
  Console.WriteLine($"s: {t.s}, i: {t.i}, p: {t.p}");
  //}}
  ```
+ 类型推断：
  ```c#
  //{{c1::
  var t2 = ("magic", 42, new Person("Matthias", "Nagel"));
  Console.WriteLine($"string: {t2.Item1}, int: {t2.Item2}, person: {t2.Item3}");
  //}}
  ```
+ 类型推断加别名：
  ```c#
  //{{c1::
  var t3 = (s: "magic", i: 42, p: new Person("Matthias", "Nagel"));
  Console.WriteLine($"s: {t3.s}, i: {t3.i}, p: {t3.p}");
  //}}
  ```
+ 元组类型转换：
  ```c#
  //{{c1::
  (string astring, int anumber, Person aperson) t4 = t3;
  Console.WriteLine($"s: {t4.astring}, i: {t4.anumber}, p: {t4.aperson}");
  //}}
  ```

### 元组解构
+ 完整解构：
  ```c#
  //{{c1::
  (string s, int i, Person p) = ("magic", 42, new Person("Stephanie", "Nagel"));
  Console.WriteLine($"s: {s}, i: {i}, p: {p}");
  //}}
  ```
+ 类型推断解构：
  ```c#
  //{{c1::
  (var s1, var i1, var p1) = ("magic", 42, new Person("Stephanie", "Nagel"));
  Console.WriteLine($"s: {s1}, i: {i1}, p: {p1}");

            string s2;
            int i2;
            Person p2;
            (s2, i2, p2) = ("magic", 42, new Person("Katharina", "Nagel"));
            Console.WriteLine($"s: {s2}, i: {i2}, p: {p2}");
  //}}
  ```

### 元组的返回
+ 方法定义：
  ```C#
  //{{c1::
  static (int result, int remainder) Divide(int dividend, int divisor)
  {
      int result = dividend / divisor;
      int remainder = dividend % divisor;
      return (result, remainder);
  }
  //}}
  ```
+ 调用：
  ```C#
  //{{c1::
  private static void ReturningTuples()
  {
      (int result, int remainder) = Divide(7, 2);
      Console.WriteLine($"7 / 2 - result: {result}, remainder: {remainder}");
  }
  //}}
  ```

### 任意类型的元组解构定义

+ 任意类型元组解构**调用**：
  ```C#
    private static void Deconstruct()
    {
        var p1 = new Person("Katharina", "Nagel");

        (var first, var last) = p1;
        Console.WriteLine($"{first} {last}");
    }
  ```
+ 任意类型元组解构**普通定义**：
  ```C#
  //{{c1::
    public class Person
    {
        public Person(string firstName, string lastName)
        {
            FirstName = firstName;
            LastName = lastName;
        }
        public string FirstName { get; }
        public string LastName { get; }

        public override string ToString() => $"{FirstName} {LastName}";

        public void Deconstruct(out string firstName, out string lastName)
        {
            firstName = FirstName;
            lastName = LastName;
        }
    }
  //}}
  ```
+ 任意类型元组解构**元组定义**：
  ```C#
  //{{c1::
  public static class RacerExtensions
  {
      public static void Deconstruct(this Racer r, out string firstName, out string lastName, out int starts, out int wins)
      {
          firstName = r.FirstName;
          lastName = r.LastName;
          starts = r.Starts;
          wins = r.Wins;
      }
  }

  //调用
  static void DeconstructWithExtensionsMethods()
  {
      var racer = Formula1.GetChampions().Where(r => r.LastName == "Lauda").First();
      //下面的代码片段将 Racer分解为变量 first和 last. Starts和wins被忽略
      (string first, string last, _, _) = racer;
      Console.WriteLine($"{first} {last}");
  }
  //}}
  ```

## 第14章 错误与异常

### C#异常继承体系图
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210408203549.png)}}

### System.Exception类属性：

+ `Data`:{{c1:: 这个属性可以给异常添加键/值语句，以提供关于异常的额外信息 }}
+ `Helplink`:{{c1:: 链接到一个帮助文件上，以提供关于该异常的更多信息 }}
+ `InnerException`:{{c1:: 如果此异常是在 catch块中抛出的，它就会包含把代码发送 }}到 catch块中的异常对象
+ `Message`:{{c1:: 描述错误情况的文本 }}
+ `Source`:{{c1:: 导致异常的应用程序名或对象名 }}
+ `StackTrace`:{{c1:: 栈上方法调用的详细信息，它有助于跟踪抛出异常的方法 }}
+ `HResult`:{{c1:: 分配给异常的一个数值 }}
+ `TargetSite`:{{c1:: NET反射对象，描述了抛出异常的方法 }}
+ 使用示例：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210408204132.png)

### 异常过滤器
+ 作用：{{c1::catch块仅在过滤器返回true时执行。捕获不同的异常类型时，可以有行为不同的 catch块。}}
+ 使用示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210408204712.png)}}

### 重新抛出异常用法示例：
+ 不改变异常直接抛出：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210408211406.png)}}
+ 改变异常再抛出：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210408211439.png)}}
+ 不改变异常直接抛出简写：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210408211516.png)}}
+ 使用过滤器添加功能：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210408211546.png)}}
  + 注意:{{c1::异常过滤器也可以用于其他效果，比如写入日志信息。}}
