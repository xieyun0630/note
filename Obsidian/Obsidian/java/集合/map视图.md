# map视图
+ 3种map视图：
	+ 含义：{{c1::键集、值集合（**不是一个Set**）以及键/值对集。}}
	+ 获取方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210801101659.png)	}}
		+ 注意：
			+ {{c1::`keyset`不是 `HashSet`或 `TreeSet`,而是实现了`Set`接口的另外某个类的对象。}}
			+ {{c1::如果在键集视图上调用迭代器的`remove方法`，实际上会从映射中删除这个键和与它关联的值。不过，不能向键集视图中添加元素。}}
			+ 视图有一些限制: {{c1:: 可能只读，可能无法改変大小，或者可能只支持删除而不支持插入（如映射的键视图）。如果试图执行不恰当的操作，受限制的视图就会抛出一个nsupportedoperationexception}} 
