
- [基础](#基础)
<!-- /code_chunk_output -->
## 基础

### **Python 的解释器** 如今有多个语言的实现，包括：

* `CPython` —— 官方版本的 C 语言实现
* `Jython` —— 可以运行在 Java 平台
* `IronPython` —— 可以运行在 .NET 和 Mono 平台
* `PyPy` —— Python 实现的，支持 JIT 即时编译

### 交互式Python 程序

1. 官方交互式: 直接在终端中运行`python`   `python3` 进入交互程序
   1. 退出命令：`exit()`
2. IPython:IPython 是一个 python 的 **交互式 shell**，比默认的 `python shell` 好用得多
   1. 退出命令：`In [1]: exit`

### python注释

1. 单行注释 - 以**#和空格**开头的部分
2. 多行注释 - 三个引号`"""`开头，三个引号`"""`结尾

### Python 变量和类型

- 整型：Python中可以处理任意大小的整数（Python 2.x中有`int`和`long`两种类型的整数，但这种区分对Python来说意义不大，因此在Python 3.x中整数只有int这一种了），而且支持二进制（如`0b100`，换算成十进制是4）、八进制（如`0o100`，换算成十进制是64）、十进制（`100`）和十六进制（`0x100`，换算成十进制是256）的表示法。
- 浮点型：浮点数也就是小数，之所以称为浮点数，是因为按照科学记数法表示时，一个浮点数的小数点位置是可变的，浮点数除了数学写法（如`123.456`）之外还支持科学计数法（如`1.23456e2`）。
- 字符串型：字符串是以单引号或双引号括起来的任意文本，比如`'hello'`和`"hello"`,字符串还有原始字符串表示法、字节字符串表示法、Unicode字符串表示法，而且可以书写成多行的形式（用三个单引号或三个双引号开头，**三个单引号**或**三个双引号**结尾）。
- 布尔型：布尔值只有`True`、`False`两种值，要么是`True`，要么是`False`，在Python中，可以直接用`True`、`False`表示布尔值（请注意大小写），也可以通过布尔运算计算出来（例如`3 < 5`会产生布尔值`True`，而`2 == 1`会产生布尔值`False`）。
- 复数型：形如`3+5j`，跟数学上的复数表示一样，唯一不同的是虚部的`i`换成了`j`。实际上，这个类型并不常用，大家了解一下就可以了。

### Python检查变量的类型

```Python
a = 100
b = 12.345
c = 1 + 5j
d = 'hello, world'
e = True
print(type(a))    # <class 'int'>
print(type(b))    # <class 'float'>
print(type(c))    # <class 'complex'>
print(type(d))    # <class 'str'>
print(type(e))    # <class 'bool'>
```

### Python运算符

| 运算符                                                       | 描述                           |
| ------------------------------------------------------------ | ------------------------------ |
| `[]` `[:]`                                                   | 下标，切片                     |
| `**`                                                         | 指数                           |
| `~` `+` `-`                                                  | 按位取反, 正负号               |
| `*` `/` `%` `//`                                             | 乘，除，模，整除               |
| `+` `-`                                                      | 加，减                         |
| `>>` `<<`                                                    | 右移，左移                     |
| `&`                                                          | 按位与                         |
| `^` `\|`                                                     | 按位异或，按位或               |
| `<=` `<` `>` `>=`                                            | 小于等于，小于，大于，大于等于 |
| `==` `!=`                                                    | 等于，不等于                   |
| `is`  `is not`                                               | 身份运算符                     |
| `in` `not in`                                                | 成员运算符                     |
| `not` `or` `and`                                             | 逻辑运算符                     |
| `=` `+=` `-=` `*=` `/=` `%=` `//=` `**=` `&=` `|=` `^=` `>>=` `<<=` | （复合）赋值运算符             |

### python分支语句:对分段函数求值

![](https://gitee.com/xieyun714/nodeimage/raw/master/img/formula_1.png)

```python
# {{c1::
x = float(input('x = '))
if x > 1:
    y = 3 * x - 5
elif x >= -1:
    y = x + 2
else:
    y = 5 * x + 3
print('f(%.2f) = %.2f' % (x, y))
# }}
```

### for循环与`range`

- `range(101)`：可以用来产生0到100范围的整数，需要注意的是取不到101。

- `range(1, 101)`：可以用来产生1到100范围的整数，相当于前面是闭区间后面是开区间。

- `range(1, 101, 2)`：可以用来产生1到100的奇数，其中2是步长，即每次数值递增的值。

- `range(100, 0, -2)`：可以用来产生100到1的偶数，其中-2是步长，即每次数字递减的值。

- 例：用for循环实现1~100之间的偶数求和

  ```python
  sum = 0
  for x in range(2, 101, 2):
      sum += x
  print(sum)
  ```

### while循环

- 猜数字例子：

  ```python
  import random
  answer = random.randint(1, 100)
  counter = 0
  while True:
      counter += 1
      number = int(input('请输入: '))
      if number < answer:
          print('大一点')
      elif number > answer:
          print('小一点')
      else:
          print('恭喜你猜对了!')
          break
  print('你总共猜了%d次' % counter)
  if counter > 7:
      print('你的智商余额明显不足')
  ```

+ `break`：终止当前循环
+ `continue`：忽略`continue`之后本次循环代码

## 函数和模块

### 函数：定义求阶乘函数

```python
def fac(num):
    """求阶乘"""
    result = 1
    for n in range(1, num + 1):
        result *= n
    return result
m = int(input('m = '))
n = int(input('n = '))
# 当需要计算阶乘的时候不用再写循环求阶乘而是直接调用已经定义好的函数
print(fac(m) // fac(n) // fac(m - n))
```

### 函数的参数

- 带默认值 :`def add(a=0, b=0, c=0)：` 没有带参数就使用默认值
- 不按照顺序调用：`print(add(c=50, a=100, b=200))`  需要携带参数名
- 可变参数：`def add(*args)`   可以传入0个或多个参数



### 用模块管理函数

+ Python中每个文件就代表了一个模块（module）

+ 分开导入模块：

  ```python
  from module1 import foo
  
  # 输出hello, world!
  foo()
  
  from module2 import foo
  
  # 输出goodbye, world!
  foo()
  ```

+ 为模块起别名：

  ```python
  import module1 as m1
  import module2 as m2
  
  m1.foo()
  m2.foo()
  ```

+ 防止导入模块内的默认运行：

  ```python
  def foo():
      pass
  
  
  def bar():
      pass
  
  
  # __name__是Python中一个隐含的变量它代表了模块的名字
  # 只有被Python解释器直接执行的模块的名字才是__main__
  if __name__ == '__main__':
      print('call foo()')
      foo()
      print('call bar()')
      bar()
  ```

### 变量的作用域`global` `nonlocal`

 `global` ：在局部作用域中定义全局变量

```python
def foo():
    global a
    a = 200
    print(a)  # 200


if __name__ == '__main__':
    a = 100
    foo()
    print(a)  # 200
```

`nonlocal`实现闭包：

```python
def add():
    count = 1
    def fun():
        nonlocal count
        print(count)
        count += 1
    return fun

a = add()
a()
a()
```

## 字符串和常用数据结构

### python 3种字符串类型

```python
s1 = 'hello, world!'
s2 = "hello, world!"
# 以三个双引号或单引号开头的字符串可以折行
s3 = """
hello, 
world!
"""
print(s1, s2, s3, end='')
```

### python 字符串的运算操作

+ `s1 = 'hello ' * 3   print(s1)` : {{c1:: ` # hello hello hello ` }}
+ `s2 = 'world'  s1 += s2 print(s1)` : {{c1:: ` # hello hello hello world` }}
+ `print('ll' in s1)` : {{c1:: ` # True` }}
+ `print('good' in s1)` : {{c1:: ` # False` }}
+ `str2 = 'abc123456'` : {{c1:: ` # 从字符串中取出指定位置的字符(下标运算)` }}
+ `print(str2[2])` : {{c1:: ` # c` }}
+ `print(str2[2:5])` : {{c1:: ` # c12` }}
+ `print(str2[2:])` : {{c1:: ` # c123456` }}
+ `print(str2[2::2])` : {{c1:: ` # c246` }}
+ `print(str2[::2])` : {{c1:: ` # ac246` }}
+ `print(str2[::-1])` : {{c1:: ` # 654321cba` }}
+ `print(str2[-3:-1])` : {{c1:: ` # 45` }}

### 字符串常见函数
+ 串：`str1 = 'hello, world!'`
+ 常见操作：
+ 通过内置函数len计算字符串的长度 :{{c1:: `print(len(str1)) # 13` }}
+ 获得字符串首字母大写的拷贝 :{{c1:: `print(str1.capitalize()) # Hello,  }}world!`
+ 获得字符串每个单词首字母大写的拷贝 :{{c1:: `print(str1.title()) #  }}Hello, World!`
+ 获得字符串变大写后的拷贝 :{{c1:: `print(str1.upper()) # HELLO, WORLD!` }}
+ 从字符串中查找子串所在位置 :{{c1:: `print(str1.find('or')) # 8 :{ }}{c1:: `print(str1.find('shit')) # -1` }}
+ 与find类似但找不到子串时会引发异常:{{c1:: `print(str1.index('or'))  }}print(str1.index('shit'))`
+ 检查字符串是否以指定的字符串开头 :{{c1:: `print(str1.startswith('He'))  }}# False print(str1.startswith('hel')) # True`
+ 检查字符串是否以指定的字符串结尾 :{{c1:: `print(str1.endswith('!')) #  }}True`
+ 将字符串以指定的宽度居中并在两侧填充指定的字符 :{{c1:: `print(str1.center(50, '*'))`
+ 将字符串以指定的宽度靠右放置左侧填充指定的字符 :{{c1:: `print(str1.rjust(50, ' '))`
+ 串：`str2 = 'abc123456'`
+ 常见操作：
+ 检查字符串是否由数字构成 :{{c1:: `print(str2.isdigit())  # False` }}
+ 检查字符串是否以字母构成 :{{c1:: `print(str2.isalpha())  # False` }}
+ 检查字符串是否以数字和字母构成 :{{c1:: `print(str2.isalnum())  # True` }}
+ 获得字符串修剪左右两侧空格之后的拷贝 :{{c1:: `print(str3.strip())` }}


### 字符串：格式化输出
+ 变量声明：`a, b = 5, 10`
+ 几种格式输出
  1. {{c1:: `print('%d * %d = %d' % (a, b, a * b))` }}
  2. {{c1:: `print('{0} * {1} = {2}'.format(a, b, a * b))` }}
     + 语法糖： {{c1:: `print(f'{a} * {b} = {a * b}')` }}

### 列表：运算操作

+ 注意以下代码的输出

  ```python
  list1 = [1, 3, 5, 7, 100]
  print(list1)
  # 乘号表示列表元素的重复
  list2 = ['hello'] * 3
  print(list2)
  # 计算列表长度(元素个数)
  print(len(list1))
  print(list1[0])
  print(list1[4]) 
  # print(list1[5])  # IndexError: list index out of range
  print(list1[-1])
  print(list1[-3])
  list1[2] = 300
  print(list1)
  ```
  
+ 输出：

  ```
  #{{c1::
  [1, 3, 5, 7, 100]
  ['hello', 'hello', 'hello']
  5
  1
  100
  100
  5
  [1, 3, 300, 7, 100]
  #}}
  ```

### 列表：遍历

- 注意以下代码的输出

  ```python
  list1 = [1, 3, 5, 7, 100]
  # 通过循环用下标遍历列表元素
  for index in range(len(list1)):
      print(list1[index])
  # 通过for循环遍历列表元素
  for elem in list1:
      print(elem)
  # 通过enumerate函数处理列表之后再遍历可以同时获得元素索引和值
  for index, elem in enumerate(list1):
      print(index, elem)
  ```
+ 输出

  ```python
  #{{c1::
  1
  3
  5
  7
  100
  1
  3
  5
  7
  100
  0 1
  1 3
  2 5
  3 7
  4 100
  #}}
  ```

### 列表：增删查改

+ 列表声明：`list1 = [1, 3, 5, 7, 100]`
+ 添加元素
    ```python
    #{{c1::
    list1.append(200)
    list1.insert(1, 400)
    #}}
    ```
+ 合并两个列表
    ```python
    #{{c1::
    # list1.extend([1000, 2000])
    list1 += [1000, 2000]
    print(list1) # [1, 400, 3, 5, 7, 100, 200, 1000, 2000]
    print(len(list1)) # 9
    #}}
    ```
+ 先通过成员运算判断元素是否在列表中，如果存在就删除该元素
    ```python
    #{{c1::
    if 3 in list1:
        list1.remove(3)
    if 1234 in list1:
    list1.remove(1234)
    print(list1) # [1, 400, 5, 7, 100, 200, 1000, 2000]
    #}}
    ```
+ 从指定的位置删除元素
    ```python
    #{{c1::
    list1.pop(0)
    list1.pop(len(list1) - 1)
    print(list1) # [400, 5, 7, 100, 200, 1000]
    #}}
    ```
+ 清空列表元素
    ```python
    #{{c1::
    list1.clear()
    print(list1) # []
    #}}
    ```
### 列表：切片操作
+ 注意以下代码输出
    ```python
    fruits = ['grape', 'apple', 'strawberry', 'waxberry']
    fruits += ['pitaya', 'pear', 'mango']

    fruits2 = fruits[1:4]
    print(fruits2) 

    fruits3 = fruits[:]
    print(fruits3) 

    fruits4 = fruits[-3:-1]
    print(fruits4) 

    fruits5 = fruits[::-1]
    print(fruits5)
    ```
    
+ 输出

    ```python
    #{{c1::
    ['apple', 'strawberry', 'waxberry']
    ['grape', 'apple', 'strawberry', 'waxberry', 'pitaya', 'pear', 'mango']
    ['pitaya', 'pear']
    ['mango', 'pear', 'pitaya', 'waxberry', 'strawberry', 'apple', 'grape']
    #}}
    ```

### 列表：排序

+ 声明列表：`list1 = ['orange', 'apple', 'zoo', 'internationalization', 'blueberry']`

+ 默认排序：`sorted(list1)`
+ 反转排序：`sorted(list1, reverse=True)`
+ 根据字符串长度进行排序:`sorted(list1, key=len)`

+ 直接在列表对象上进行排序:`list1.sort(reverse=True)`

### 列表：生成式和生成器