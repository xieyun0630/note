
- [基础](#基础)
<!-- /code_chunk_output -->
## 基础 [	](python_20201224023254431)

### **Python 的解释器** 如今有多个语言的实现，包括： [	](python_20201224023254433)

* `CPython`:{{c1:: 官方版本的 C 语言实现  }}
* `Jython`:{{c1:: 可以运行在 Java 平台  }}
* `IronPython`:{{c1:: 可以运行在 .NET 和 Mono 平台  }}
* `PyPy`:{{c1:: Python 实现的，支持 JIT 即时编译  }}

### 交互式Python 程序 [	](python_20201224023254436)

1. 官方交互式: {{c1:: 直接在终端中运行`python` `python3` 进入交互程序 }}
   1. 退出命令：{{c1:: `exit()` }}
2. IPython: {{c1:: IPython 是一个 python 的 **交互式 shell**，比默认的 `python shell` 好用得多 }}
   1. 退出命令：{{c1:: `In [1]: exit` }}
   2. python注释 

1. 单行注释:{{c1:: 以**#和空格**开头的部分 }}
2. 多行注释:{{c1:: 三个引号`"""`开头，三个引号`"""`结尾 }}

### Python 变量和类型 [	](python_20201224023254441)

- 整型：{{c1:: Python中可以处理任意大小的整数（Python 2.x中有`int`和`long`两种类型的整数，但这种区分对Python来说意义不大，因此在Python 3.x中整数只有int这一种了），而且支持二进制（如`0b100`，换算成十进制是4）、八进制（如`0o100`，换算成十进制是64）、十进制（`100`）和十六进制（`0x100`，换算成十进制是256）的表示法。}}
- 浮点型：{{c1:: 浮点数也就是小数，之所以称为浮点数，是因为按照科学记数法表示时，一个浮点数的小数点位置是可变的，浮点数除了数学写法（如`123.456`）之外还支持科学计数法（如`1.23456e2`）。}}
- 字符串型：{{c1:: 字符串是以单引号或双引号括起来的任意文本，比如`'hello'`和`"hello"`,字符串还有原始字符串表示法、字节字符串表示法、Unicode字符串表示法，而且可以书写成多行的形式（用三个单引号或三个双引号开头，**三个单引号**或**三个双引号**结尾）。}}
- 布尔型：{{c1:: 布尔值只有`True`、`False`两种值，要么是`True`，要么是`False`，在Python中，可以直接用`True`、`False`表示布尔值（请注意大小写），也可以通过布尔运算计算出来（例如`3 < 5`会产生布尔值`True`，而`2 == 1`会产生布尔值`False`）。}}
- 复数型：{{c1:: 形如`3+5j`，跟数学上的复数表示一样，唯一不同的是虚部的`i`换成了`j`。实际上，这个类型并不常用，大家了解一下就可以了。}}

### Python检查变量的类型 [	](python_20201224023254443)

```Python
a = 100
b = 12.345
c = 1 + 5j
d = 'hello, world'
e = True

# type(a)
#{{c1::
print(type(a))    # <class 'int'>
print(type(b))    # <class 'float'>
print(type(c))    # <class 'complex'>
print(type(d))    # <class 'str'>
print(type(e))    # <class 'bool'>
#}}
```

### Python运算符 [	](python_20201224023254445)

| 运算符                                                       | 描述                           |
| ------------------------------------------------------------ | ------------------------------ |
| `[]` `[:]`                                                   | {{c1:: 下标，切片                    }} |
| `**`                                                         | {{c1:: 指数                          }} |
| `~` `+` `-`                                                  | {{c1:: 按位取反, 正负号              }} |
| `*` `/` `%` `//`                                             | {{c1:: 乘，除，模，整除              }} |
| `+` `-`                                                      | {{c1:: 加，减                        }} |
| `>>` `<<`                                                    | {{c1:: 右移，左移                    }} |
| `&`                                                          | {{c1:: 按位与                        }} |
| `^` `\|`                                                     | {{c1:: 按位异或，按位或              }} |
| `<=` `<` `>` `>=`                                            | {{c1:: 小于等于，小于，大于，大于等于}} |
| `==` `!=`                                                    | {{c1:: 等于，不等于                  }} |
| `is`  `is not`                                               | {{c1:: 身份运算符                    }} |
| `in` `not in`                                                | {{c1:: 成员运算符                    }} |
| `not` `or` `and`                                             | {{c1:: 逻辑运算符                    }} |
| `=` `+=` `-=` `*=` `/=` `%=` `//=` `**=` `&=` `|=` `^=` `>>=` `<<=` | {{c1:: （复合）赋值运算符            }} |

### python分支语句:对分段函数求值 [	](python_20201224023254448)

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

### python　for循环与`range` [	](python_20201224023254451)

- `range(101)`：{{c1:: 可以用来产生0到100范围的整数，需要注意的是取不到101。 }}

- `range(1, 101)`：{{c1:: 可以用来产生1到100范围的整数，相当于前面是闭区间后面是开区间。 }}

- `range(1, 101, 2)`：{{c1:: 可以用来产生1到100的奇数，其中2是步长，即每次数值递增的值。 }}

- `range(100, 0, -2)`：{{c1:: 可以用来产生100到1的偶数，其中-2是步长，即每次数字递减的值。 }}

- 例：用for循环实现1~100之间的偶数求和

  ```python
  #{{c1::
  sum = 0
  for x in range(2, 101, 2):
	  sum += x
  print(sum)
  #}}
  ```

### python　while循环 [	](python_20201224023254454)

- 猜数字例子：
  ```python
  #{{c1::
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
  #}}
  ```

+ `break`：{{c1:: 终止当前循环 }}
+ `continue`：{{c1:: 忽略`continue`之后本次循环代码 }}
## 模块与包 [ ](python_20201227010951594)
### python模块 [	](python_20201224023254466)

+ python模块定义：{{c1:: Python中每个文件就代表了一个模块 （module），在导入时，文件中**所有没有任何缩进的代码** 都会被执行一遍！ }}
+ 模块内置属性:
  + `__name__`：{{c1:: 是被其他文件导入的，`__name__`就是模块名，如果是当前执行的程序`__name__`是`__main__` }}
  + `__file__`：{{c1:: **查看模块** 的 **完整路径** }}
+ 导入模块中部分内容：
  ```python
  #{{c1::
  from module1 import foo
  foo()
  #}}
  ```
+ 为模块起别名：
  ```python
  #{{c1::
  import module1 as m1
  m1.foo()
  #}}
  ```
+ 防止导入模块内的默认运行：
  ```python
  #{{c1::
  def foo():
	  pass
  def bar():
	  pass
  if __name__ == '__main__':
	  print('call foo()')
	  foo()
	  print('call bar()')
	  bar()
  #}}
  ```

### python包  [ ](python_20201227010951597)
+ 概念: {{c1:: **包含多个模块**以及`__init__.py`文件的 **特殊目录** }}
+ 作用: {{c1:: 使用 `import 包名` 可以一次性导入 **包** 中 **所有的模块** }}
+ `__init__.py`文件
  + 作用：{{c1:: 要在外界使用 **包** 中的模块，需要在 `__init__.py` 中指定 **对外界提供的模块列表** }}
    ```python
    #{{c1::
    # 从当前目录导入模块列表
    from . import send_message
    from . import receive_message
    #}}
    ```
### python　`pip` 安装第三方模块 [ ](python_20201227010951599)
+ 安装和卸载命令如下：
  ```bash
  # {{c1::
  # 将模块安装到 Python 2.x 环境
  $ sudo pip install pygame
  $ sudo pip uninstall pygame

  # 将模块安装到 Python 3.x 环境
  $ sudo pip3 install pygame
  $ sudo pip3 uninstall pygame
  #}}
  ```


## 函数 [	](python_20201224023254457)

### python函数：定义 [	](python_20201224023254461)
+ 案例：求阶乘函数
	```python
    #{{c1::
	def fac(num):
		"""求阶乘"""
		result = 1
		for n in range(1, num + 1):
			result *= n
		return result
	m = int(input('m = '))
	n = int(input('n = '))
    #}}
	# 当需要计算阶乘的时候不用再写循环求阶乘而是直接调用已经定义好的函数
	print(fac(m) // fac(n) // fac(m - n))
	```

### python函数的参数 [	](python_20201224023254464)

- 带默认值定义:{{c1:: `def add(a=0, b=0, c=0)：` 没有带参数就使用默认值 }}
- 不按照顺序调用：{{c1:: `print(add(c=50, a=100, b=200))`  需要携带参数名 }}
- 可变参数定义：{{c1:: `def add(*args)`   可以传入0个或多个参数 }}


### python变量的作用域`global` `nonlocal` [	](python_20201224023254469)

+ `global`关键字作用：{{c1:: 指示`foo`函数中的变量`a`来自于全局作用域}}
+ `nonlocal`关键字作用：{{c1:: 指示变量来自于嵌套作用域}}
+ `global` ：修改全局作用域中的`a`，代码如下所示
  
    ```python
    #{{c1::
    def foo():
        global a
        a = 200
        print(a)  # 200
    if __name__ == '__main__':
        a = 100
        foo()
        print(a)  # 200
    #}}
    ```
+ `nonlocal`实现闭包：
  
  ```python
  #{{c1::
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
  #}}
  ```

## 字符串和常用数据结构 [	](python_20201224023254472)

### python 3种字符串类型 [	](python_20201224023254474)

```python
#{{c1::
s1 = 'hello, world!'
s2 = "hello, world!"
# 以三个双引号或单引号开头的字符串可以折行
s3 = """
hello, 
world!
"""
print(s1, s2, s3, end='')
#}}
```

### python 字符串的运算操作 [	](python_20201224023254478)

+ `s1 = 'hello ' * 3   print(s1)` : {{c1:: ` # hello hello hello ` }}
+ `s2 = 'world'  s1 += s2 print(s1)` : {{c1:: ` # hello hello hello world` }}
+ `print('ll' in s1)` : {{c1:: ` # True` }}
+ `print('good' in s1)` : {{c1:: ` # False` }}
+ 串：`str2 = 'abc123456'`
  + `print(str2[2])` : {{c1:: ` # c` }}
  + `print(str2[2:5])` : {{c1:: ` # c12` }}
  + `print(str2[2:])` : {{c1:: ` # c123456` }}
  + `print(str2[2::2])` : {{c1:: ` # c246` }}
  + `print(str2[::2])` : {{c1:: ` # ac246` }}
  + `print(str2[::-1])` : {{c1:: ` # 654321cba` }}
  + `print(str2[-3:-1])` : {{c1:: ` # 45` }}

### python字符串常见函数 [	](python_20201224023254481)
+ 串：`str1 = 'hello, world!'`
+ 常见操作：
+ 通过内置函数len计算字符串的长度 :{{c1:: `print(len(str1)) # 13` }}
+ 首字母大写的拷贝 :{{c1:: `print(str1.capitalize()) # Hello,world!`}}
+ 每个单词首字母大写的拷贝 :{{c1:: `print(str1.title()) #Hello, World!`}}
+ 变大写后的拷贝 :{{c1:: `print(str1.upper()) # HELLO, WORLD!` }}
+ 查找子串所在位置 :{{c1:: `print(str1.find('or')) # 8  print(str1.find('shit')) # -1` }}
+ 与find类似但找不到子串时会引发异常:{{c1:: `print(str1.index('or'))  print(str1.index('shit'))`}}
+ 是否以指定的字符串开头 :{{c1:: `print(str1.startswith('He'))  # False print(str1.startswith('hel')) # True`}}
+ 是否以指定的字符串结尾 :{{c1:: `print(str1.endswith('!')) #  True`}}
+ 以指定的宽度居中并在两侧填充指定的字符 :{{c1:: `print(str1.center(50, '*'))`}}
+ 以指定的宽度靠右放置左侧填充指定的字符 :{{c1:: `print(str1.rjust(50, ' '))`}}
+ 串：`str2 = 'abc123456'`
+ 常见操作：
+ 是否由数字构成 :{{c1:: `print(str2.isdigit())  # False` }}
+ 是否以字母构成 :{{c1:: `print(str2.isalpha())  # False` }}
+ 是否以数字和字母构成 :{{c1:: `print(str2.isalnum())  # True` }}
+ 修剪左右两侧空格之后的拷贝 :{{c1:: `print(str3.strip())` }}

### python字符串：格式化输出 [	](python_20201224023254484)
+ 变量声明：`a, b = 5, 10`
+ 几种格式输出
  1. {{c1:: `print('%d * %d = %d' % (a, b, a * b))` }}
  2. {{c1:: `print('{0} * {1} = {2}'.format(a, b, a * b))` }}
	 + 语法糖： {{c1:: `print(f'{a} * {b} = {a * b}')` }}

### python列表：运算操作 [	](python_20201224023254488)

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

### python列表：遍历 [	](python_20201224023254491)

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

### python列表：增删查改 [	](python_20201224023254494)

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
### python列表：切片操作 [	](python_20201224023254496)
+ 列表定义：`fruits = ['grape', 'apple', 'strawberry', 'waxberry', 'pitaya', 'pear', 'mango']`
+ 输出:
    + `fruits[1:4]`:{{c1:: `['apple', 'strawberry', 'waxberry']` }}
    + `fruits[:]`:{{c1:: `['grape', 'apple', 'strawberry', 'waxberry', 'pitaya', 'pear', 'mango']` }}
    + `fruits[-3:-1]`:{{c1:: `['pitaya', 'pear']` }}
    + `fruits[::-1]`:{{c1:: `['mango', 'pear', 'pitaya', 'waxberry', 'strawberry', 'apple', 'grape']` }}

### python列表：排序 [	](python_20201224023254498)

+ 声明列表：`list1 = ['orange', 'apple', 'zoo', 'internationalization', 'blueberry']`
+ 操作
  + 默认排序：{{c1:: `sorted(list1)` }}
  + 反转排序：{{c1:: `sorted(list1, reverse=True)` }}
  + 根据字符串长度进行排序:{{c1:: `sorted(list1, key=len)` }}
  + 直接在列表对象上进行排序:{{c1:: `list1.sort(reverse=True)` }}

### python列表：生成式和生成器 [	](python_20201224023254500)

+ 生成式生成列表
  + 单循环：{{c1:: `f = [x for x in range(1, 10)]` }}
  + 嵌套循环：{{c1:: `f = [x + y for x in 'ABCDE' for y in '1234567']` }}
  + 定义表达式：{{c1:: `f = [x ** 2 for x in range(1, 1000)]` }}
+ 生成器的声明：{{c1:: `f = (x ** 2 for x in range(1, 1000))` }}
  + 使用：{{c1:: `print(f)` `for val in f:` }}

### python使用`yield`实现一个生成斐波拉切数列的生成器 [ ](python_20201227010951601)
+ 函数定义:
    ```python
    #{{c1::
    def fib(n):
        a, b = 0, 1
        for _ in range(n):
            a, b = b, a + b
            yield a
    #}}
    ```
+ 函数调用:
    ```python
    #{{c1::
    def main():
        for val in fib(20):
            print(val)
    if __name__ == '__main__':
        main()
    #}}
    ```

### python元组 [ ](python_20201227010951605)
+ 与列表的区别：{{c1:: 在于元组的元素不能修改，其他操作几乎一样 }}
+ 元组的使用
  + 定义元组：{{c1:: `t = ('骆昊', 38, True, '四川成都')` }}
  + 获取元组中的元素：{{c1:: `print(t[0])` `print(t[3])` }}
  + 遍历：{{c1:: `for member in t:` }}
  + 重新给元组赋值:{{c1:: `#t[0] = '王大锤'  # TypeError` }}
  + 将元组转换成列表：{{c1:: `list(t)` }}
  + 将列表转换成元组:{{c1::  `tuple(fruits_list)` }}
+ 已经有了列表,为什么需要元组:
  + **线程安全**：{{c1:: 多线程环境（后面会讲到）中可能更喜欢使用的是那些不变对象 }}
  + **性能优势**：{{c1:: 元组在创建时间和占用的空间上面都优于列表。 }}

### python集合 [ ](python_20201227010951609)
+ 特点：乱序，唯一性
+ 定义集合
  + 字面量定义：{{c1:: `set1 = {1, 2, 3, 3, 3, 2}` }}
  + 构造器语法定义：{{c1:: `set2 = set(range(1, 10))`  `set3 = set((1, 2, 3, 3, 2, 1))` }}
  + 推导式语法定义：{{c1:: `set4 = {num for num in range(1, 100) if num % 3 == 0 or num % 5 == 0}` }}
+ 增删操作：
  + 增：{{c1:: `set1.add(4)` `set2.update([11, 12])` }}
  + 删：{{c1:: `set3.pop() set2.discard(5)` `set2.remove(4)` }}
  + 查改：{{c1:: `if 4 in set2: set2.remove(4)` }}
+ 集合运算：
  + 求交集：{{c1:: `print(set1 & set2)` `print(set1.intersection(set2))` }}
  + 求并集：{{c1:: `print(set1 | set2)` `print(set1.union(set2))` }}
  + 求差集: {{c1:: `print(set1 - set2)` `print(set1.difference(set2))` }}
  + 求对称差：{{c1:: `print(set1 ^ set2)` `print(set1.symmetric_difference(set2))` }}
  + 是否子集：{{c1:: `print(set2 <= set1)` `print(set2.issubset(set1))` }}
  + 是否超集：{{c1:: `print(set1 >= set3)` `print(set1.issuperset(set3))` }}

### python字典 [ ](python_20201227010951612)
+ 定义字段：
  + 字面量语法：{{c1:: `scores = {'骆昊': 95, '白元芳': 78, '狄仁杰': 82}` }}
  + 构造器语法：{{c1:: `items1 = dict(one=1, two=2, three=3, four=4)` }}
  + 通过zip函数将两个序列压成字典:{{c1:: `items2 = dict(zip(['a', 'b', 'c'], '123'))` }}
  + 推导式语法:{{c1:: `items3 = {num: num ** 2 for num in range(1, 10)}` }}
+ 获取字典的值：{{c1:: `scores['骆昊']` `scores.get('武则天')` `scores.get('武则天', 60)` }}
+ 遍历：{{c1:: `for key in scores: print(f'{key}: {scores[key]}')` }}
+ 更新：{{c1:: `scores['白元芳'] = 65` }}
+ 同时更新多个：{{c1:: `scores.update(冷面=67, 方启鹤=85)` }}
+ 删除：
  + 删除最后：{{c1:: `scores.popitem()`}}
  + 删除指定: {{c1:: `scores.pop('骆昊', 100)`}}

## 面向对象 [ ](python_20201227010951614)

### python类的定义与使用 [ ](python_20201227010951617)
+ 定义类
  ```python
    #{{c1::
    class Student(object):

    # __init__是一个特殊方法用于在创建对象时进行初始化操作
    # 通过这个方法我们可以为学生对象绑定name和age两个属性
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def study(self, course_name):
        print('%s正在学习%s.' % (self.name, course_name))

    # PEP 8要求标识符的名字用全小写多个单词用下划线连接
    # 但是部分程序员和公司更倾向于使用驼峰命名法(驼峰标识)
    def watch_movie(self):
        if self.age < 18:
            print('%s只能观看《熊出没》.' % self.name)
        else:
            print('%s正在观看岛国爱情大电影.' % self.name)
    #}}
  ```
+ 创建和使用对象:
  ```python
  #{{c1::
  def main():
    # 创建学生对象并指定姓名和年龄
    stu1 = Student('骆昊', 38)
    # 给对象发study消息
    stu1.study('Python程序设计')
    # 给对象发watch_av消息
    stu1.watch_movie()
    stu2 = Student('王大锤', 15)
    stu2.study('思想品德')
    stu2.watch_movie()
  if __name__ == '__main__':
      main()
  #}}
  ```
### python类的语法细节 [ ](python_20201227010951619)
+ `dir()`内置函数：{{c1:: `dir()`,传入 **标识符** / **数据**，可以查看对象内的 **所有属性及方法** }}
+ 常用的内置方法
  | 序号 |   方法名   | 类型 | 作用                                         |
  | :--: | :--------: | :--: | -------------------------------------------- |
  |  01  | `__new__`  | {{c1::方法 }} | {{c1::**创建对象**时，会被 **自动** 调用          }} |
  |  02  | `__init__` | {{c1::方法 }} | {{c1::**对象被初始化**时，会被 **自动** 调用      }} |
  |  03  | `__del__`  | {{c1::方法 }} | {{c1::**对象被从内存中销毁**前，会被 **自动** 调用}} |
  |  04  | `__str__`  | {{c1::方法 }} | {{c1::返回**对象的描述信息**，必须返回一个字符串，`print` 函数输出使用}} |
+ python的访问可见性：
  + 默认：{{c1:: 只有2种，默认是公开的，私有属性的方法在name前面加`__` }}
    + 例：{{c1:: ` def __bar(self):`  ` self.__foo = foo` }}
  + 在外部访问私有属性：{{c1:: `Python`的私有属性只是改变了名称使外部无法访问,在 **名称** 前面加上 `_类名` => `_类名__名称`即可访问 }}
  + 使用可见性建议：{{c1:: 不建议使用`__`，可以使用`_`暗示属性是受保护的。 }}
+ 身份运算符: {{c1:: `x is y，类似 id(x) == id(y)` `x is not y，类似 id(a) != id(b)` }}
+ `is`与`==`区别：{{c1:: `is` 用于判断 **两个变量 引用对象是否为同一个**,`==` 用于判断 **引用变量的值** 是否相等 }}

### python的getter与setter设置 [ ](python_20201227010951622)
```python
#{{c1::
class Person(object):
    # 限定Person对象只能绑定_name, _age和_gender属性
    __slots__ = ('_name', '_age', '_gender')
    def __init__(self, name, age):
        self._name = name
        self._age = age
    @property
    def name(self):
        return self._name
    @property
    def age(self):
        return self._age
    @age.setter
    def age(self, age):
        self._age = age
def main():
  # person.name = '白元芳'  # AttributeError: can't set attribute
#}}
```
### 类属性与类方法的定义 [ ](python_20201227010951624)
+ 基本概念：{{c1:: python中类是一个特殊的对象 }}
```python
#{{c1::
class Tool(object):
    # 使用赋值语句，定义类属性，记录创建工具对象的总数
    count = 0
    def __init__(self, name):
        self.name = name
        # 针对类属性做一个计数+1
        Tool.count += 1
    
    @classmethod
    def 类方法名(cls):
    pass
#}}
```

### python静态方法 [ ](python_20201227010951627)
+ 使用理由：{{c1:: 在开发时，如果需要在类中封装一个方法，这个方法,既不需要访问**实例属性**或者调用**实例方法**也不需要访问**类属性**或者调用**类方法**这个时候，可以把这个方法封装成一个**静态方法** }}
+ 语法：
  ```python
  #{{c1::
  @staticmethod
  def 静态方法名():
      pass
  #}}
  ```

### python重写`__new__`方法,实现单例模式 [ ](python_20201227010951630)
+ python实现单例模式2个注意点：
  + `__new__`:{{c1:: 返回对象引用 }}
  + `__init__`:{{c1:: 只调用一次 }}
+ `*args`和`**kwargs`的区别：{{c1:: 分别将参数打包成**元组**与**字典** }}
```python
#{{c1::
class MusicPlayer(object):

    # 记录第一个被创建对象的引用
    instance = None
    # 让初始化动作只被执行一次
    init_flag = False

    def __new__(cls, *args, **kwargs):

        # 1. 判断类属性是否是空对象
        if cls.instance is None:
            # 2. 调用父类的方法，为第一个对象分配空间
            cls.instance = super().__new__(cls)
        # 3. 返回类属性保存的对象引用
        return cls.instance

    def __init__(self):

        if not MusicPlayer.init_flag:
            print("初始化音乐播放器")
            MusicPlayer.init_flag = True
#}}
```


### python的继承，多态，多继承 [ ](python_20201227010951633)
+ 继承的语法
  ```python
  #{{c1::
  # 单继承
  class 类名(父类名):
      pass
  # 多继承
  class 类名(父类名1,父类名2):
      pass
  #}}
  ```
+ 覆盖父类的方法：{{c1:: 相当于在 **子类中** 定义了一个 **和父类同名的方法并且实现** }}
+ 调用父类方法：{{c1:: `super().父类方法` }}
+ 父类的私有属性和私有方法:{{c1::子类对象可以通过父类的公有方法**间接访问**到私有属性或私有方法 }}
+ 查询方法搜索顺序:{{c1:: `print(ClassName.__mro__)` }}

### python　`eval`函数与执行终端命令 [ ](python_20201227010951635)
+ 作用：{{c1:: **将字符串** 当成 **有效的表达式** 来求值 并 **返回计算结果** }}
+ 例：
  + 基本的数学计算:{{c1:: `eval("1 + 1")` }}
  + 字符串重复:{{c1:: `eval("'*' * 10")` }}
  + 将字符串转换成列表:{{c1:: `type(eval("[1, 2, 3, 4, 5]"))` }}
  + 将字符串转换成字典:{{c1:: `type(eval("{'name': 'xiaoming', 'age': 18}"))` }}
+ 执行终端命令：{{c1:: `import os` `os.system("终端命令")` }}
+ 注意：{{c1:: 为了安全性,在开发时千万不要使用 `eval` 直接转换 `input` 的结果 }}


## 异常 [ ](python_20201227010951637)

### python异常捕获完整语法 [ ](python_20201227010951640)
```python
#{{C1::
try:
    # 尝试执行的代码
    pass
except 错误类型1:
    # 针对错误类型1，对应的代码处理
    pass
except 错误类型2:
    # 针对错误类型2，对应的代码处理
    pass
except (错误类型3, 错误类型4):
    # 针对错误类型3 和 4，对应的代码处理
    pass
except Exception as result:
    # 打印错误信息
    print(result)
else:
    # 没有异常才会执行的代码
    pass
finally:
    # 无论是否有异常，都会执行的代码
    print("无论是否有异常，都会执行的代码")
#}}
```

### python抛出异常 [ ](python_20201227010951643)
```python
#{{c1::
def input_password():
    # 1. 提示用户输入密码
    pwd = input("请输入密码：")
    # 2. 判断密码长度，如果长度 >= 8，返回用户输入的密码
    if len(pwd) >= 8:
        return pwd
    # 3. 密码长度不够，需要抛出异常
    # 1> 创建异常对象 - 使用异常的错误信息字符串作为参数
    ex = Exception("密码长度不够")
    # 2> 抛出异常对象
    raise ex
try:
    user_pwd = input_password()
    print(user_pwd)
except Exception as result:
    print("发现错误：%s" % result)
#}}
```

## python文件 [ ](python_20201227010951646)

### python文件的操作模式 [ ](python_20201227010951648)
| 操作模式 | 具体含义                                                     |
| -------- | ------------------------------------------------------------ |
| `'r'`    | {{c1:: 读取 （默认）                                               }} |
| `'w'`     | {{c1:: 以**只写**方式打开文件。如果文件存在会被覆盖。如果文件不存在，创建新文件}} |
| `'x'`    | {{c1:: 写入，如果文件已经存在会产生异常                            }} |
| `'a'`    | {{c1:: 追加，将内容写入到已有文件的末尾                            }} |
| `'b'`    | {{c1:: 二进制模式                                                  }} |
| `'t'`    | {{c1:: 文本模式（默认）                                            }} |
| `'+'`    | {{c1:: 更新（既可以读又可以写）                                    }} |

### python读取文本文件 [ ](python_20201227010951651)
+ 一次性读取整个文件内容
  ```python
  #{{c1::
  with open('致橡树.txt', 'r', encoding='utf-8') as file:
      print(file.read())
  #}}
  ```
+ 通过for-in循环逐行读取
  ```python
  #{{c1::
  with open('致橡树.txt', mode='r') as file:
      for line in file:
          print(line, end='')
          time.sleep(0.5)
  #}}
  ```
+ 读取文件按行读取到列表中
  ```python
  #{{c1::
  with open('致橡树.txt') as file:
      lines = file.readlines()
  #}}
  ```

### python读写二进制文件:复制图片文件的功能 [ ](python_20201227010951654)
```python
#{{c1::
def main():
        with open('guido.jpg', 'rb') as fs1:
            data = fs1.read()
            print(type(data))
        with open('吉多.jpg', 'wb') as fs2:
            fs2.write(data)
#}}
```

### python读写JSON文件 [ ](python_20201227010951658)
```python
#{{c1::
    #将字典转换为json格式写入文件
    with open('data.json', 'w', encoding='utf-8') as fs:
        json.dump(mydict, fs)
    #读取文本为python数据类型
    resp = requests.get('http://api.tianapi.com/guonei/?key=APIKey&num=10')
    data_model = json.loads(resp.text)
#}}
```
+ json模块主要有四个比较重要的函数，分别是：
- `dump`：{{c1:: 将Python对象按照JSON格式序列化到文件中 }}
- `dumps`：{{c1:: 将Python对象处理成JSON格式的字符串 }}
- `load`：{{c1:: 将文件中的JSON数据反序列化成对象 }}
- `loads`：{{c1:: 将字符串的内容反序列化成Python对象 }}

### python数据类型与JOSN数据的转换 [ ](python_20201227010951661)
| Python                                 | JSON         |
| -------------------------------------- | ------------ |
| `dict`                                   | {{c1:: `object` }}       |
| `list, tuple`                            | {{c1:: `array` }}        |
| `str`                                    | {{c1:: `string` }}       |
| `int, float, int- & float-derived Enums` | {{c1:: `number` }}       |
| `True / False`                           | {{c1:: `true / false` }} |
| `None`                                   | {{c1:: `null` }}         |

### python文件/目录的常用管理操作 [ ](python_20201227010951664)
+ 文件操作
  | 序号 | 方法名 | 说明       | 示例                              |
  | ---- | ------ | ---------- | --------------------------------- |
  | 01   | rename | 重命名文件 | {{c1:: `os.rename(源文件名, 目标文件名)`}} |
  | 02   | remove | 删除文件   | {{c1:: `os.remove(文件名)`              }} |
+ 目录操作
  | 序号 | 方法名     | 说明           | 示例                      |
  | ---- | ---------- | -------------- | ------------------------- |
  | 01   | listdir    | 目录列表       | {{c1:: `os.listdir(目录名)`     }} |
  | 02   | mkdir      | 创建目录       | {{c1:: `os.mkdir(目录名)`       }} |
  | 03   | rmdir      | 删除目录       | {{c1:: `os.rmdir(目录名)`       }} |
  | 04   | getcwd     | 获取当前目录   | {{c1:: `os.getcwd()`            }} |
  | 05   | chdir      | 修改工作目录   | {{c1:: `os.chdir(目标目录)`     }} |
  | 06   | path.isdir | 判断是否是文件 | {{c1:: `os.path.isdir(文件路径)`}} |
> 注意：{{c1:: 文件或者目录操作都支持 **相对路径** 和 **绝对路径** }}