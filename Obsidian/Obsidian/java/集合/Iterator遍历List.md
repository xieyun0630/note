# `Iterator`遍历`List`

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

[[容器中迭代器模式]]
[//anki]: # "java_se_20210113065733273"