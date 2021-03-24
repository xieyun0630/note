
## C#基础

### .NET Core 编译命令
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

### 变量
+ 类型推断var关键字：{{c1::`var someNumbyer = 0;` 等价于 `int someNumber;`}}
+ 常量声明：{{c1::`const int a = 100;`}}
+ `sbyte` `short` `int` `long` `byte` `ushort` `uint` `ulong`对应的.NET数据类型：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322114223.png)}}

### 字符串字面量
+ `@`前缀：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322115013.png)
+ `$`前缀：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322115024.png)

### using关键字
+ 作用：{{c1::为类型建立层次结构}}
+ using定义层次结构图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322115245.png)}}
+ 名称空间别名图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322115340.png)}}

### C#的3种注释
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322115436.png)}}

### C#预处理器指令
+ `#define #undef` : {{c1::相当于boolean值}}
+ `#if #elif #else #endif` :{{c1::根据`#define`所定义的常量进行判断}}
+ `#warning #error` ::{{c1:: `#warning` 编译时发出警告信息，`#error`发送错误信息且停止编译。}}
+ `#region #endregion` : {{c1::为代码区域命名}}
+ `#pragma`: {{c1::抑制或还原指定的编译警告}}

## 第3章 对象和类型 

### C# 类与结构
+ 声明类语法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322130633.png)}}
+ 声明结构语法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322130654.png)}}
+ 声明实例：{{c1::对于类和结构，都使用关键字new来声明实例![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322131019.png)}}
+ 类与结构重要区别：{{c1::类型的对象通过引用传递，结构类型的对象按值传递}}

### C# 字段
+ 字段声明：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322131344.png)
+ 字段声明：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322131551.png)
  + 注意：{{c1::如果只读字段是一个实例字段，就要在实例构造函数中初始化它。}}

### C# 属性
+ 常规语法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322132646.png)}}
+ 具有表达式体的属性访问器：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322132708.png)}}
+ 自动实现的属性：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322132744.png)}}
+ 属性的访问修饰符：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322133005.png)}}

### C# 只读属性
+ 只读属性：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322133101.png) }}
+ 自动实现的只读属性：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322133444.png)}}
+ 表达式体属性：{{c1:: 是带有get访问器的属性，但不需要get关键字![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322133755.png) }}
  

### C# 匿名类型
+ 注意点：
  + 匿名类型只是一个继承自{{c1::Object且没有名称的类。}}
  + 根据字段名来区分各个类，{{c1::具有完全相同字段的两个类，类型相同。}}
  + 如果所设置的值来自于另一个对象，{{c1::则可以推断匿名类型成员的名称}}
+ 语法:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322134326.png)}}

### C# 方法
+ 表达式体方法声明：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322134906.png)}}
+ 命名的参数方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322142022.png)}}
+ 可选参数方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322142124.png)}}
+ 可变参数方法：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322142307.png) }}

### C# 构造函数
+ 表达式体构造函数:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322142428.png)}}
+ 从构造函数中调用其他构造函数:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322142501.png)}}
+ 静态构造函数：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322142548.png)}}

### C# 结构
+ 结构的继承体系:{{c1::每个结构派生自System.ValueType类，System.ValueType派生自System.Object类。}}
+ 结构是值类型，具体到代码上与类的区别：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322143050.png)}}
+ 只读结构的声明：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322143115.png)}}

### C# 按值和按引用传递参数
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

### C# 可空类型
+ 声明语法：{{c1:: `int? x = null;` }}
+ 注意：可空类型转换为普通类型时，{{c1:: 需要类型强制转换，如果是null会抛出异常 }}
+ HasValue与Value属性：{{c1:: `int x5 = x3.HasValue ? x3.Value : -1;` }}
+ 合并运算符结合可空类型使用：{{c1:: `int x6 = x3 ?? -1; `}}

### C# 枚举类型
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

### C# Enum类常用工具方法
+ Enum.TryParse:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322154805.png)}}
+ Enum.GetNames:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322154815.png)}}
+ Enum.GetValues:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322154824.png)}}

### C# 部分类
+ 作用：{{c1:: `partial`关键字允许把类、结构、方法或接口放在多个文件中。}}
+ 用法：{{c1::把 `partial`放在 `class` `struct` 或 `interface`关键字的前面。}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322161219.png)}}
+ 部分方法的作用：{{c1:: 使用生成的代码调用了可能不存在的方法，可以使用部分方法避免编译错误。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322161448.png) }}

### C# 拓展方法
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

## 第4章 继承

### 实现继承
+ 类继承：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322164204.png)}}
+ 结构继承（只能继承接口)：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322164151.png)}}

### 虚方法
+ 作用：{{c1::指明基类中的方法可以被子类重写。}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322164422.png)}}

### 隐藏方法
+ 定义：{{c1:: 如果签名相同的方法在基类和派生类中都进行了声明，但该方法没有分别声明为 virtual和 override,派生类方法就会隐藏基类方法 }}
 + new关键字抑制编译警告：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322170107.png)

### 调用方法的基类版本
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322171723.png)}}

### 抽象类
+ 语法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322171903.png)}}
+ 处理待定实现的抽象方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322172005.png)}}

### sealed关键字
+ 作用：{{c1::给类`sealed`，不允许创建该类的子类。给方法`sealed`，表示不能重写该类的方法。}}
+ 注意：{{c1::需要密封的方法，要声明为virtual。}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322172412.png)}}

### C#调用基类的构造函数
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322174202.png)}}

### C# 访问修饰符

+ `public`:{{c1::公有访问。不受任何限制。}}
+ `private`:{{c1::私有访问。只限于本类成员访问，子类，实例都不能访问。}}
+ `protected`:{{c1::保护访问。只限于本类和子类访问，实例不能访问。}}
+ `internal`:{{c1::内部访问。只限于本项目内访问，其他不能访问。}}
+ `protected internal`:{{c1::内部保护访问。只限于本项目或是子类访问，其他不能访问 `protected` 或 `internal`}}
+ `private protected`:  {{c1::`private` 且 `protected`}}

### is和as运算符
+ is使用例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322175532.png)}}
+ as使用例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322175545.png)}}
+ 体会主要区别:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323083210.png)}}

## 第5章 泛型

### 泛型对性能的提升
+ 主要原因：{{c1::泛型可以减少装修与拆箱带来的性能损失}}
+ 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322180038.png)}}

### C# 泛型中default关键字
+ 作用：{{c1::将null赋予引用类型，将0赋予值类型。}}
+ 示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322180751.png)}}

### C#泛型约束

+ `where T: struct` : {{c1:: 对于结构约束，类型T必须是值类型 }}
+ `where T: class` : {{c1:: 类约束指定类型T必须是引用类型 }}
+ `where T: Ifoo` : {{c1:: 指定类型T必须实现接口IFoo }}
+ `where T: Foo` : {{c1:: 指定类型T必须派生自基类Foo }}
+ `where T: new()` : {{c1:: 这是一个构造函数约東，指定类型T必须有一个默认构造函数 }}
+ `where TI: T2` : {{c1:: 这个约束也可以指定，类型T1派生自泛型类型T2 }}
+ 合并多个约束：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322181413.png)}}
+ 带约束泛型方法图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323080856.png)}}

### C# 泛型继承
+ 前提条件：{{c1::必须重复接口的泛型类型，或者必须指定基类的类型}}
  + 必须重复接口的泛型类型: {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322183019.png) }}
  + 指定基类的类型: {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322183040.png) }}
+ 部分泛型继承：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322183235.png)}}

### 泛型类的静态成员
+ 需注意的点:{{c1::泛型类的静态成员只能在类的一个实例中共享。}}
+ 图示:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210322183449.png)}}

### 协变和抗变
+ 定义：{{c1::.net中**参数类型**是**抗变的**,方法**返回类型**是**协变的**。}}
+ 如果泛型类型用`in`关键字标注，{{c1:: 泛型接口就是**抗变的**。这样，接口只能把泛型类型T用作其方法的**参数**输入 }}
+ 如果泛型类型用`out`关键字标注，{{c1:: 泛型接口就是**协变的**。这也意味着**返回类型**只能是T }}
## 第6章 运算符和类型强制转换

### 带委托的泛型方法
+ 调用图示：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323082215.png)
+ 实现图示:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323082140.png) }}

### 溢出检查
+ checked关键字：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323082810.png) }}
+ 全局开启与unchecked：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323082836.png) }}

### 常用运算符
+ `sizeof`：{{c1::运算符可以确定栈中值类型需要的长度（单位是字节）}}
+ `typeof`: {{c1::typeof运算符返回一个表示特定类型的 System.Type对象。}}
+ `nameof`: {{c1::该运算符接受一个符号、属性或方法，并返回其名称。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323083840.png)}}
+ `??`：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323084021.png) }}


### 空值条件运算符处理空值
+ 空值条件运算符：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323131158.png)}}
+ 使用空值条件运算简化以下代码：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323133658.png)
  + 简化后：{{c1::`string city = p?.HomeAddress?.City;`}}
+ 判断数组是否为空：{{c1::`int x1 = arr?[0] ?? 0;`}}

### 比较对象的相等性
1. `ReferenceEquals()`方法:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323164909.png)}}
2. `Equals()`虚方法
3. 静态`Equals()`方法
4. 比较运算符(`==`)

### 比较运算符的重载
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


### 实现自定义的索引运算符
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
### 用户定义的类型强制转换
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


## 第7章 数组

### `C#`数组声明与初始化

+ 声明：{{c1::`int[] myArray;`}}
+ 几种初始化：
  1. {{c1::`int[] myArray = new int[4];`}}
  2. {{c1::`int[] myArray = new int[4]{1,2,3,4};`}}
  3. {{c1::`int[] myArray = new int[]{1,2,3,4};`}}
  4. {{c1::`int[] myArray = {1,2,3,4};`}}

### 创建数组：`CreateInstance()`,`SetValue()`,`GetValue()`

+ 使用示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323173155.png) }}
+ `setValue()`对应维数：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323173227.png) }}

### 复制数组
+ 浅复制：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323214637.png)}}

### IComparable<T>与IComparer<T>区别：
+ `IComparable`数组排序：{{c1::`Array.Sort(persons,new PersonComparer(PersonCompareType.FirstName));`}}
+ `IComparer`数组排序：{{c1::`Array.Sort(persons);`}}

### foreach语句调用迭代器解析
```C#
  foreach(var p in persons){
    Console.WriteLine(p);
  }
```
+ 以上foreach语句会解析为下面的代码段:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323215907.png)}}

### 迭代集合的不同方式
+ 类得默认迭代：
  + 定义迭代器：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323221608.png) }}
  + 调用：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323221635.png) }}
+ 命名得迭代：
  + 定义迭代器：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323221741.png) }}
  + 调用：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210323221814.png) }}

### 用 `yield return`返回枚举器

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
### 结构比较

+ `IStructuralequatable`接口:{{c1::用于比较两个元组或数组是否有相同的内容}}
+ `IStructuralComparable`接口:{{c1::用于给元组或数组排序}}

### 数组池
+ 创建数组池:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210324100721.png)}}
+ 从池中租用内存:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210324100832.png)}}
+ 将内存返回给池:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210324100847.png)}}

## 第8章 委托、lambda 表达式和事件

### 委托
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

### `Action<T>`和`Func<T>`委托

+ `Action<T>`: {{c1:: 没有泛型参数的 `Action`类可调用没有参数的方法。 `Action<in T>`调用带一个参数的方法，`Action<in T1>`,inT2>调用带两个参数的方法， `Action<in T1,in T2,in T3,in T4,in TS,in T6,in T,in T8>`调用带8个参数的方法。 }}
+ `Func<T>`: {{c1:: `Func< out Tresult>`委托类型可以调用带返回类型且无参数的方法，`Func<in T, out Tresult>`调用带一个参数的方法， `Func<in TI,in T2,in T3,in T4,out Tresult>`调用带4个参数的方法。 }}

### 多播委托

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

### C# 匿名方法与lambda表达式
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
