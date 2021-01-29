## c数据结构基本概念 [	](dataStructure_20200928050450150)

### 数据 [	](dataStructure_20200928050450152)
+ 含义：{{c1:: 数据是信息的载体，是描述客观事物属性的数、字符及所有能输入到计算机中并被计算机程序识别
和处理的符号的集合。 }}

### 数据元素、数据项 [	](dataStructure_20200928050450154)
+ 数据元素：{{c1:: 数据元素是数据的基本单位，通常作为一个整体进行考虑和处理。 }}
+ 数据项：{{c1:: 一个数据元素可由若干数据项组成，数据项是构成数据元素的不可分割的最小单位。 }}

### 数据对象、数据结构 [	](dataStructure_20200928050450156)
+ 数据结构:{{c1:: 相互之间存在一种或多种特定关系的数据元素的集合。 }}
+ 数据对象:{{c1:: 具有相同性质的数据元素的集合，是数据的一个子集。 }}

### 数据类型、抽象数据类型（ADT） [	](dataStructure_20200928050450158)
+ 含义：{{c1:: （Abstract Data Type，ADT）用数学化的语言定义数据的逻辑结构、定义运算。与具体的实现无关。 }}
+ 定义一个ADT，就是定义了数据的逻辑结构、数据的运算。也就是定义了一个数据结构。

### 数据结构三要素 [	](dataStructure_20200928050450160)
1. 逻辑结构
    + 集合
        + 特点：{{c1:: 各个元素同属一个集合，别无其他关系 }}
    + 线性结构
        + 特点：{{c1:: 除了第一个元素，所有元素都有唯一前驱；除了最后一个元素，所有元素都有唯一后继； }}
    + 树形结构
        + 特点：{{c1:: 数据元素之间是一对多的关系 }}
    + 网状结构
        + 特点：{{c1:: 数据元素之间是多对多的关系 }}
2. 存储结构（物理结构）
    + 顺序存储
        + 特点：{{c1:: 逻辑上相邻的元素存储在物理位置上也相邻的存储单元中 }}
    + 链式存储
        + 特点：{{c1:: 逻辑上相邻的元素在物理位置上可以不相邻 }}
    + 索引存储
        + 特点：{{c1:: 索引表中的每项称为索引项，索引项的一般形式是（关键字，地址） }}
    + 散列存储
        + 特点：{{c1:: 根据元素的关键字直接计算出该元素的存储地址，又称哈希（Hash）存储 }}
3. 数据的运算：{{c1:: 运算的定义是针对逻辑结构的,指出运算的功能；运算的实现是针对存储结构的，指出运算的具体操作步骤 }}

## 算法的基本概念 [	](dataStructure_20200928050450162)

+ 什么是算法：{{c1:: 程序 = 数据结构 + 算法，（要处理的信息 + 处理信息的步骤） }}
+ 算法的五大特性：{{c1:: 有穷，确定，可行，输入，输出 }}
+ 好算法的特质：{{c1:: 正确，可读，健壮，高效率与低存储量需求 }}

### 算法的时间复杂度：概念 [	](dataStructure_20201109090319176)
+ 大O表示“同阶”，同等数量级。即：{{c1:: 当n趋近无穷时，二者之比为常数 }}
  + 如图：{{c1::![image-20201028081250811](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201028081250811.png)}}
+ 加法规则：{{c1:: `T(n) = T1(n) + T2(n) = O(f(n)) + O(g(n)) = O(max(f(n), g(n)))` }}
+ 乘法规则: {{c1:: `T(n) = T1(n)×T2(n) = O(f(n))×O(g(n)) = O(f(n)×g(n))` }}
+ 例(图):{{c1:: ![image-20201028082144384](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201028082144384.png) }}

### 算法的时间复杂度：判断时间复杂度大小 [	](dataStructure_20201109090319179)
+ 口诀：{{c1::常对幂指阶 }}
+ 时间复杂度的几种类型，函数对比图：{{c1:: ![image-20201028082720604](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201028082720604.png) }}

### 计算代码的时间复杂度:计算步骤 [	](dataStructure_20201109090319182)
+ 如何计算：
  1. {{c1:: 找到一个基本操作（最深层循环） }}
  2. {{c1:: 分析该基本操作的执行次数x与问题规模n的关系x=f(n) }}
  3. {{c1:: x的数量级O(x）就是算法时间复杂度T(n) }}

### 计算代码的时间复杂度T(n):指数递增型 [	](dataStructure_20201109090319185)
+ C代码如图：![image-20201028083306983](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201028083306983.png)
+ 解答：
  + {{c1:: ![image-20201028083557860](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201028083557860.png) }}

### 计算代码的时间复杂度T(n):搜索数字型 [	](dataStructure_20201109090319189)
+ ![image-20201028084423890](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201028084423890.png)
+ 解答：{{c1:: ![image-20201028084445848](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201028084445848.png) }}

### 计算代码算法的空间复杂度T(n):递归程序 [	](dataStructure_20201109090319194)

+ 例题：![image-20201029152330813](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201029152330813.png)
+ 解答：{{c1:: ![image-20201029152644992](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201029152644992.png) }}

+ 计算步骤:
  1. {{c1:: 找到递归调用的深度x与问题规模n的关系x=f(n) }}
  2. {{c1:: x的数量级O(x）就是算法空间复杂度S(n) }}
  3. {{c1:: 注：有的算法各层函数所需存储空间不同，分析方法略有区别 }}
## 线性表 [	](dataStructure_20201109090319197)

### 线性表定义(Linear List) [	](dataStructure_20201109090319199)
+ 定义：{{c1:: 线性表是具有**相同类型**的n个数据元素的**有限序列** }}
+ 主要特点：{{c1:: 除第一个元素外，每个元素有且仅有一个直接前驱；除最后一个元素外，每个元素有且仅有一个直接后继 }}

### 线性表的基本运算/操作定义(C++定义) [	](dataStructure_20201109090319202)
+ `InitList(&L)`：{{c1:: **初始化**表。构造一个空的线性表L，**分配内存空间**。 }}
+ `DestroyList(&L)`：{{c1:: **销毁**操作。销毁线性表，并**释放**线性表L所占用的**内存空间**。 }}
+ `ListInsert(&L,i,e)`：**插入**操作。在表L中的第i个位置上插入指定元素e。
+ `ListDelete(&L,i,&e)`：{{c1:: **删除**操作。删除表L中第i个位置的元素，并用e返回删除元素的值。 }}
+ `LocateElem(L,e)`：{{c1:: **按值查找**操作。在表L中查找具有给定关键字值的元素。 }}
+ `GetElem(L,i)`：{{c1:: **按位查找**操作。获取表L中第i个位置的元素的值。 }}
+ 什么时候要传入引用`&`:{{c1:: 对参数的修改结果需要**带回来**}}

### 顺序表（顺序结构） [	](dataStructure_20201109090319204)
+ 定义：{{c1:: 用**顺序存储**的方式实现**线性表**。}}
+ 特点：{{c1:: 把**逻辑上相邻**的元素存储在**物理位置上**也**相邻**的存储单元中 }}
+ 元素间的关系：{{c1:: 元素之间的关系由**存储单元的邻接关系**来体现。 }}
### 顺序表实现：静态分配（数据结构定义） [	](dataStructure_20201109090319207)

+ 特点：{{c1:: 静态分配的存储空间一旦确定就不可变 }}
  ```c
  //{{c1::
  #define MaxSize 10					//定义最大长度
  typedef struct{
    ElemType data[MaxSize]; 	//用静态的“数组”存放数据元素
    int length;							  //顺序表的当前长度
  }SqList; 										//顺序表的类型定义（静态分配方式）
  //}}
  ```

### 顺序表的实现：动态分配（数据结构定义） [	](dataStructure_20201109090319209)

```c
//{{c1::
#define InitSize 10 //顺序表的初始长度
typedef struct{
  ElemType *data; 	//指示动态分配数组的指针
  int MaxSize; 			//顺序表的最大容量
  int length; 			//顺序表的当前长度
} SeqList; 					//顺序表的类型定义（动态分配方式）
//}}
```

### 顺序表的实现：动态分配（初始化表操作） [	](dataStructure_20201109090319212)

```c
//{{c1::
void initList(SeqList &L){
  	//申请内存空间
    L.data=(int *)malloc(InitSize*sizeof(int));
    L.length=0;
    L.MaxSize=InitSize;
}
//}}
```

### 顺序表的实现：动态分配（增加动态数据长度操作） [	](dataStructure_20201109090319214)

```c
//{{c1::
void IncreaseSize(SeqList &L,int len){
    int *p =L.data;
    L.data=(int *)malloc((L.MaxSize+len)*sizeof(int));
    for(int i=0;i<L.length;i++){
        L.data[i]=p[i];
    }
    L.MaxSize = L.MaxSize + len;
    free(p);
}
//}}
```

### 顺序表的实现：动态分配（插入操作） [	](dataStructure_20201109090319216)

```c
//{{c1::
bool ListInsert(SqList &L,int i,int e){
    if(i<1 || i>L.Length+1)  //判断i的范围
        return false;
    if(L.length>=MaxSize)    //存储空间是否已满
        return false;
    for(int j=L.length;j>=i;j--) //移出插入元素的位置
        L.data[j]=L.data[j-1];
    L.data[i-1]=e;
    L.length++;
    return true;
}
//}}
```

+ 时间复杂度分析：{{c1::![image-20201030131159344](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201030131159344.png)}}

### 顺序表的特点：  [	](dataStructure_20201109090319218)

1. {{c1:: **随机访问** }}
2. {{c1:: **存储密度高** }}
3. {{c1:: **拓展容量不方便** }}
4. {{c1:: **插入、删除操作不方便** }}

### 单链表实现：数据结构定义 [	](dataStructure_20201109090319220)

```c
//{{c1::
typedef struct LNode{
    ElemType data;
    struct LNode *next;
}LNode,*LinkList;
//}}
```

### 单链表实现：头插法建立单链表 [	](dataStructure_20201109090319222)

```c
//{{c1::
LinkList List_HeadInsert(LinkList &L){
    LNode *s; int x;
    L = (LinkList) malloc(sizeof(LNode));
    L->next=NULL;
    scanf("%d",&x);
    while(x!=9999){
        s=(LNode*)malloc(sizeof(LNode));
        s->data=x;
        s->next=L->next;
        L->next=s;
        scanf("%d",&x);
    }
    return L;
}
//}}
```

+ 主要思路：{{c1:: ![image-20201030151026718](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201030151026718.png) }}

### 单链表实现：初始化操作 [	](dataStructure_20201109090319224)

+ 带头节点

  ```c
  //{{c1::
  bool InitList(LinkList &L){
    L = (LNode *) malloc(sizeof(LNode));
    if(L==NULL)
    		return false;
    L->next = NULL;
    return true;
  }
  //}}
  ```

+ 不带头结点

  ```c
  //{{c1::
  bool InitList(LinkList &L){
  	L = NULL；
  	return false;
  }
  //}}
  ```

### 单链表实现：按位插入 [	](dataStructure_20201124103028993)

+ 带头节点:
+ {{c1:: ![image-20201030142950126](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201030142950126.png) }}
+ 不带节点:
+ {{c1:: ![image-20201030143239923](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201030143239923.png) }}

### 单链表实现：前后插操作 [	](dataStructure_20201109090319226)

+ 后插操作:
+ {{c1:: ![image-20201030143428032](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201030143428032.png) }}

+ 前插操作:
+ {{c1:: ![image-20201030143924193](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201030143924193.png) }}

### 单链表实现：按位删除（带头节点） [	](dataStructure_20201109090319229)
+ 主要思路：找到i-1的节点
+ 边际问题注意：
  + 注意最后一个元素
  + 注意i是否超范围
{{c1::![image-20201030144304774](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201030144304774.png)  }}

### 单链表实现：指定结点的删除 [	](dataStructure_20201109090319232)

{{c1:: ![image-20201030144510894](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201030144510894.png)  }}

### 双链表实现：数据结构 [	](dataStructure_20201109090319234)

```c
//{{c1::
typedef struct DNode{
    ElemType data;
    struct DNode *prior,*next;
}DNode,*DLinkList;
//}}
```

### 双链表实现：初始化 [	](dataStructure_20201109090319237)

{{c1:: ![image-20201030152011675](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201030152011675.png) }}

### 双链表实现：指定节点后添加节点（后插操作） [	](dataStructure_20201109090319243)

{{c1:: ![image-20201030151749646](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201030151749646.png) ![image-20201109170334280](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201109170334280.png)}}

### 双链表实现：删除后继节点 [	](dataStructure_20201109051135495)

{{c1:: ![image-20201109113854463](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201109113854463.png)}}

### 双链表实现：遍历 [	](dataStructure_20201109051135498)

{{c1::![image-20201109113534288](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201109113534288.png)}}

### 静态链表实现:定义 [	](dataStructure_20201109051135500)

{{c1::![image-20201109165218388](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201109165218388.png)}}

### 循环链表概况 [	](dataStructure_20201109051135502)

![image-20201109170839312](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201109170839312.png)

{{c1::![image-20201109170655284](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201109170655284.png)}}

## 栈 [	](dataStructure_20201115082829738)

### 栈（Stack):基本概念 [	](dataStructure_20201115082829740)
+ 定义:{{c1:: 只允许在一端进行插入或删除操作的**线性表** }}
+ 栈的基本操作
  + `InitStack(&S)`：{{c1:: 初始化栈。构造一个空栈 S，分配内存空间。 }}
  + `DestroyStack(&S)`：{{c1:: 销毁栈。销毁并释放栈 S 所占用的内存空间。 }}
  + `Push(&S,x)`：{{c1:: 进栈，若栈S未满，则将x加入使之成为新栈顶。 }}
  + `Pop(&S,&x)`：{{c1:: 出栈，若栈S非空，则弹出栈顶元素，并用x返回。 }}
  + `GetTop(S, &x)`：{{c1:: 读栈顶元素。若栈 S 非空，则用 x 返回栈顶元素 }}
  + `StackEmpty(S)`：{{c1:: 判断一个栈 S 是否为空。若S为空，则返回true，否则返回false。 }}
+ 出栈元素不同排列的个数计算：{{c1:: ![image-20201111131912827](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201111131912827.png) }}

### 栈的顺序存储实现 [	](dataStructure_20201115082829744)
+ 顺序存储定义
  ```c
  //{{c1::
  #define Maxsize 10 //定义栈中元素的最大个数
  typedef struct{
    Elemtype data [Maxsize]; //静态数组存放栈中元素
    int top; //栈顶指针
  } Sqstack；
  //}}
  ```
+ 初始化操作：
  ```c
  //{{c1::
  void InitStack(SqStack &S){
      S.top=-1;
  }
  //}}
  ```

### 共享栈的实现 [	](dataStructure_20201115082829747)
+ 顺序存储定义
  ```c
  //{{c1::
  #define Maxsize 10 //定义栈中元素的最大个数
  typedef struct{
    Elemtype data [Maxsize]; //静态数组存放栈中元素
    int top0; //0号栈顶指针
    int top1; //1号栈顶指针
  } Sqstack；
  //}}
  ```
  
+ 初始化操作：
  ```c
  //{{c1::
  void InitStack(SqStack &S){
      S.top=-1;
      S.top1=MaxSize;
  }
  //}}
  ```
  
+ 栈满的条件：{{c1:: `top0 + 1 == top1` }}

### 栈的应用：用栈实现字符串的括号匹配 [	](dataStructure_20201115082829750)
+ 主要思路：{{c1:: 依次扫描所有字符，遇到左括号入栈，遇到右括号则弹出栈顶元素检查是否匹配。 }}
+ 匹配失败情况：{{c1:: ①左括号单身、②右括号单身、③左右括号不匹配 }}
+ 算法实现：
  + 正面：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201115171455.png)
  + 回答：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201115171552.png) }}

### 栈的应用：表达式求值 [	](dataStructure_20201115082829752)

### 后缀/前缀表达式的计算（机算） [	](dataStructure_20201115082829755)
+ 用栈实现后缀表达式的计算：
  1. {{c1:: 从左往右扫描下一个元素，直到处理完所有元素 }}
  2. {{c1:: 若扫描到操作数则压入栈，并回到①；否则执行③ }}
  3. {{c1:: 若扫描到运算符，则弹出两个栈顶元素，执行相应运算，运算结果压回栈顶，回到① }}
  + 注意：{{c1:: 第二步，先出栈的是“右操作数” }}
+ 过程动画：
  
  + {{c1:: ![zdXEoElMxF](dataStructure.assets/zdXEoEl1MxF.gif)}}
+ 用栈实现前缀表达式的计算：
  1. {{c1:: **从右往左**扫描下一个元素，直到处理完所有元素 }}
  2. {{c1:: 若扫描到操作数则压入栈，并回到①；否则执行③ }}
  3. {{c1:: 若扫描到运算符，则弹出两个栈顶元素，执行相应运算，运算结果压回栈顶，回到① }}

### 中缀表达式转后缀表达式（手算） [	](dataStructure_20201115082829758)

+ 转换成后缀表达式：
  
  + ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201115175721.png)
+ 手算步骤：
  1. {{c1:: 确定中缀表达式中**各个运算符的运算顺序** }}
  2. {{c1:: 选择下一个运算符，按照 **「左操作数 右操作数 运算符」** 的方式组合成一个新的操作数 }}
  3. {{c1:: 如果还有运算符没被处理，就继续② }}
  + 左优先”原则：{{C1:: 只要左边的运算符能先计算，就优先算左边的 }}
+ 结果：
  
  + {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201115175840.png) }}

### 中缀表达式转前缀表达式（手算） [	](dataStructure_20201115082829761)
+ 转换成前缀表达式：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201115195440.png)
+ 手算步骤：
  1. {{c1:: 确定中缀表达式中各个运算符的**运算顺序** }}
  2. {{c1:: 选择下一个运算符，按照**「运算符 左操作 数右操作数」**的方式组合成一个新的操作数 }}
  3. {{c1:: 如果还有运算符没被处理，就继续② }}
  + 右优先”原则：{{C1:: 只要右边的运算符能先计算，就优先算右边的 }}
+ 结果：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201115195456.png) }}

### 中缀表达式转后缀表达式（机算） [	](dataStructure_20201202040742332)
+ 初始化一个栈，用于保存暂时还不能确定运算顺序的运算符。
+ 从左到右处理各个元素，直到末尾。可能遇到三种情况：
  1. {{c1:: 遇到操作数。直接加入后缀表达式。 }}
  2. {{c1:: 遇到界限符。遇到“(”直接入栈；遇到“)”则依次弹出栈内运算符并加入后缀表达式，直到弹出“(”为止。注意：“(”不加入后缀表达式。 }}
  3. {{c1:: 遇到运算符。依次弹出栈中优先级**高于或等于当前**运算符的所有运算符，并加入后缀表达式，若碰到“(” 或栈空则停止。之后再把当前运算符入栈。 }}
+ 按上述方法处理完所有字符后，将栈中剩余运算符依次弹出，并加入后缀表达式。

### 中缀表达式的计算（用栈实现） [	](dataStructure_20201202040742335)
+ 两个算法的结合:{{c1:: 中缀转后缀 + 后缀表达式求值 }}
+ 用栈实现中缀表达式的计算：
  + 初始化两个栈，操作数栈和运算符栈
  + 若扫描到操作数，压入操作数栈
  + 若扫描到运算符或界限符，则按照“中缀转后缀”相同的逻辑压入运算符栈（期间也会弹出运算符，每当弹出一个运算符时，就需要再弹出两个操作数栈的栈顶元素并执行相应运算，运算结果再压回操作数栈）
+ 例：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201129141129.png)

### 栈的递归 [	](dataStructure_20201202040742338)

## 队列 [	](dataStructure_20201115082829764)

### 队列:基本概念 [	](dataStructure_20201115082829766)
+ 定义: {{c1::队列（Queue）是只允许在一端进行插入，在另一端删除的线性表 }}
+ 队列的特点：{{c1:: First In First Out（FIFO） }}
+ 基本操作:
  + `InitQueue(&Q)`：{{c1:: **初始化**队列，构造一个空队列Q。 }}
  + `DestroyQueue(&Q)`：{{c1:: **销毁**队列。销毁并释放队列Q所占用的内存空间。 }}
  + `EnQueue(&Q,x)`：{{c1:: **入队**，若队列Q未满，将x加入，使之成为新的队尾。 }}
  + `DeQueue(&Q,&x)`：{{c1:: **出队**，若队列Q非空，删除队头元素，并用x返回。 }}
  + `GetHead(Q,&x)`：{{c1:: **读队头元素**，若队列Q非空，则将队头元素赋值给x。 }}
+ 其他常用操作：
  + `QueueEmpty(Q)`：{{c1:: 判队列空，若队列Q为空返回true，否则返回false。 }}


### 队列顺序存储实现 [	](dataStructure_20201115082829769)
+ 顺序存储定义
  ```c
    //{{c1::
    #define Maxsize 10
    typedef struct{
      Elemtype data[Maxsize]; //用静态数组存放队列元素
      int front,rear; //队头指针和队尾指针
    }SqQueue;
    //}}
  ```
+ 循环队列实现思路：{{c1:: 用模运算（取余）将存储空间在逻辑上变为"环状 }}
  + 队尾指针公式：{{c1:: `Q.rear=(Q.rear+1)%MaxSize` }}
  + 队头指针公式：{{c1:: `Q.front=(Q.front+1)%MaxSize` }}

### 循环队列确定判空判满的方法: [	](dataStructure_20201203041420407)

  1. 牺牲一个存储单元判满：
     1. 判满：{{c1:: `(Q.rear+1)%MaxSize==Q.front`  }}
     2. 判空：{{c1:: `Q.rear==Q.front` }}
     3. 注意：{{c1:: 两个指针都指向一个位置代表队列为**空** }}
  2. 增加`size`变量记录队列长度
     1. 判满：{{c1:: `rear = front = 0 and size = MaxSize`  }}
     2. 判空：{{c1:: `rear = front = 0 and size = 0` }}
  3. 增加`tag=0/1`用于表示删除/插入
     1. 判满：{{c1:: `rear = front = 0 and tag = 1` }}
     2. 判空：{{c1:: `rear = front = 0 and tag = 0` }}

### 队列的链式存储定义 [	](dataStructure_20201115082829774)
+ 链式存储定义：
  ```c
    //{{c1::
      typedef struct Linknode{//链式队列结点
        Elemtype data;
        struct Linknode *next;
      }LinkNode;
      typedef struct{       //链式队列
        Linknode* front,*rear;//队列的队头和队尾指针
      }LinkQueue;
    //}}
  ```
+ 初始化注意点:注意是否带头节点

### 队列变种:双端队列 [	](dataStructure_20201115082829778)
+ 双端队列：{{c1:: 允许从两端插入、两端删除的队列 }}
+ 输入受限的双端队列：{{c1:: 允许从两端刑除、从一端插入的队列 }}
+ 输出受限的双端队列：{{c1:: 允许从两端插入、从一端删刪除的队列 }}

### 对称矩阵的压缩存储 [	](dataStructure_20201202040742340)
+ 思路：{{c1::关键在于`i,j`如何映射到一维数组下标`k`}}
+ 正面：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/1_back.png)
+ 回答：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/1.png) }}

### 串的存储结构总结 [	](dataStructure_20201202040742342)
+ 正面：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/%E4%B8%B22_ques.png)
+ 回答：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/%E4%B8%B22.png) }}

### KMP算法总结 [	](dataStructure_20201202040742344)
+ 朴素模式匹配算法的缺点：{{c1:: 若模式串长度为m，主串长度为h，则直到匹配成功/匹配失败最多需要`（n-m+1)*m`次比较,最坏时间复杂度：`O(nm)` }}
+ KMP算法：{{c1:: 当子串和模式串不匹配时，主串指针 i 不回溯，模式串指针`j=next[j]`算法平均时间复杂度：`O(n+m)` }}
+ next数组手算方法：{{c1:: 当第j个字符匹配失败，由前 `1~j-1` 个字符组成的串记为`S`，则：**next[j] = S的最长相等前后缀长度+1**,特别地，`next[1]=0` }}
+ nextval数组的求法：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/chrome_NJPCOTCu68.png) }}
  + nextval的作用示意图：{{c1:: ![image-20201203162535480](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201203162535480.png)}}

## 排序 [ ](dataStructure_20210113065733329)

### 冒泡排序实现 [ ](dataStructure_20210121111221922)
+ 排序原理：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210114221831.png) }}
+ 实现：
  ```java
      //{{c1::
      public static void sort(Comparable[] a){
          for(int i=a.length-1;i>0;i--){
              for(int j=0;j<i;j++){
                  //{6,5,4,3,2,1}
                  //比较索引j和索引j+1处的值
                  if (greater(a[j],a[j+1])){
                      exch(a,j,j+1);
                  }
              }
          }
      }
      //}}
  ```
+ 时间复杂度
  + 在**最坏情况下**，也就是假如要排序的元素为{6,5,4,3,2,1}逆序，那么：
      + 元素比较的次数为：{{c1:: (N-1)+(N-2)+(N-3)+...+2+1=((N-1)+1)*(N-1)/2=N^2/2-N/2; }}
      + 元素交换的次数为：{{c1:: (N-1)+(N-2)+(N-3)+...+2+1=((N-1)+1)*(N-1)/2=N^2/2-N/2; }}
      + 总执行次数为：{{c1:: (N^2/2-N/2)+(N^2/2-N/2)=N^2-N; }}
  + 时间复杂度为:{{c1:: `O(N^2)` }}
+ API设计：
  1. `public static void sort(Comparable[] a)`：{{c1:: 对数组内的元素进行排序  }}
  2. `private static boolean greater(Comparable v,Comparable w)`:{{c1:: 判断v是否大于w  }}
  3. `private static void exch(Comparable[] a,int i,int j)`：{{c1:: 交换a数组中，索引i和索引j处的值 }}


### 选择排序 [ ](dataStructure_20210121111221927)
+ 排序原理：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210114223059.png) }}
+ 实现：
  ```java
      //{{c1::
    public static void sort(Comparable[] a){
        for(int i=0;i<=a.length-2;i++){
            //定义一个变量，记录最小元素所在的索引，默认为参与选择排序的第一个元素所在的位置
            int minIndex = i;
            for(int j=i+1;j<a.length;j++){
                //需要比较最小索引minIndex处的值和j索引处的值；
                if (greater(a[minIndex],a[j])){
                    minIndex=j;
                }
            }

            //交换最小元素所在索引minIndex处的值和索引i处的值
            exch(a,i,minIndex);
        }
    }
      //}}
  ```
+ 时间复杂度
  + 在**最坏情况下**:
      + 元素比较的次数为：{{c1:: ` (N-1)+(N-2)+(N-3)+...+2+1=((N-1)+1)*(N-1)/2=N^2/2-N/2;;` }}
      + 元素交换的次数为：{{c1:: `N-1` }}
      + 总执行次数为：{{c1:: `(N^2/2-N/2)+(N^2/2-N/2)=N^2-N;` }}
  + 时间复杂度为:{{c1:: `N^2/2-N/2+（N-1）=N^2/2+N/2-1;`即
 `O(N^2)` }}

### 插入排序 [ ](dataStructure_20210121111221930)
+ 排序原理：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210114223556.png) }}
+ 实现：
  ```java
  //{{c1::
      public static void sort(Comparable[] a){
        for(int i=1;i<a.length;i++){
            for(int j=i;j>0;j--){
                if (greater(a[j-1],a[j])){
                    exch(a,j-1,j);
                }else{
                    break;
                }
            }
        }
    }
  //}}
  ```
+ 时间复杂度
  + 在**最坏情况下**:
      + 元素比较的次数为：{{c1:: `(N-1)+(N-2)+(N-3)+...+2+1=((N-1)+1)*(N-1)/2=N^2/2-N/2;` }}
      + 元素交换的次数为：{{c1:: `(N-1)+(N-2)+(N-3)+...+2+1=((N-1)+1)*(N-1)/2=N^2/2-N/2;` }}
  + 时间复杂度为:{{c1:: `(N^2/2-N/2)+(N^2/2-N/2)=N^2-N`即
`O(N^2)` }}

### 希尔排序 [ ](dataStructure_20210121111221933)

+ 排序原理：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210114230547.png) }}
+ 实现：
  ```java
  //{{c1::
    public static void sort(Comparable[] a){
        //1.根据数组a的长度，确定增长量h的初始值；
        int h = 1;
        while(h<a.length/2){
            h=2*h+1;
        }
        //2.希尔排序
        while(h>=1){
            //排序
            //2.1.找到待插入的元素
            for (int i=h;i<a.length;i++){
                //2.2把待插入的元素插入到有序数列中
                for (int j=i;j>=h;j-=h){

                    //待插入的元素是a[j],比较a[j]和a[j-h]
                    if (greater(a[j-h],a[j])){
                        //交换元素
                        exch(a,j-h,j);
                    }else{
                        //待插入元素已经找到了合适的位置，结束循环；
                        break;
                    }
                }
            }
            h= h/2;
        }
    }
  //}}
  ```
+ 时间复杂度：{{c1:: `O(n^(1.3—2))` }}

### 归并排序 [ ](dataStructure_20210121111221935)
+ 排序原理：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210114232118.png) }}
+ API设计：
  1. `public static void sort(Comparable[] a)`：{{c1:: 对数组内的元素进行排序 }}
  2. `private static void sort(Comparable[] a, int lo, int hi)`：{{c1:: 对数组a中从索引lo到索引hi之间的元素进 }}
  行排序
  3. `private static void merge(Comparable[] a, int lo, int mid, int hi)`:{{c1:: 从索引lo到所以mid为一个子组，从索引mid+1到索引hi为另一个子组，把数组a中的这两个子组的数据合并成一个有序的大组（从索引lo到索引hi） }}
  4. `private static boolean less(Comparable v,Comparable w)`：{{c1:: 判断v是否小于w }}
  5. `private static void exch(Comparable[] a,int i,int j)`：{{c1:: 交换a数组中，索引i和索引j处的值 }}
+ 核心实现：
  ```java
  //{{c1::
    private static void sort(Comparable[] a, int lo, int hi) {
        //做安全性校验；
        if (hi<=lo){
            return;
        }

        //对lo到hi之间的数据进行分为两个组
        int mid = lo+(hi-lo)/2;//   5,9  mid=7

        //分别对每一组数据进行排序
        sort(a,lo,mid);
        sort(a,mid+1,hi);

        //再把两个组中的数据进行归并
        merge(a,lo,mid,hi);
    }

    private static void merge(Comparable[] a, int lo, int mid, int hi) {
        //定义三个指针
        int i=lo;
        int p1=lo;
        int p2=mid+1;

        while(p1<=mid && p2<=hi){
            if (less(a[p1],a[p2])){
                assist[i++] = a[p1++];
            }else{
                assist[i++]=a[p2++];
            }
        }

        while(p1<=mid){
            assist[i++]=a[p1++];
        }
        while(p2<=hi){
            assist[i++]=a[p2++];
        }
        for(int index=lo;index<=hi;index++){
            a[index]=assist[index];
        }

    }
  //}}
  ```
+ 时间复杂度：{{c1:: `O(n^(1.3—2))` }}

### 快速排序 [ ](dataStructure_20210121111221937)
+ 排序原理：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210114232118.png) }}
+ API设计：
  1. `public static void sort(Comparable[] a)`：{{c1:: 对数组内的元素进行排序 }}
  2. `private static void sort(Comparable[] a, int lo, int hi)`：{{c1:: 对数组a中从索引lo到索引hi之间的元素进行排序 }}
  3. `public static int partition(Comparable[] a,int lo,int hi)`: {{c1:: 对数组a中，从索引 lo到索引 hi之间的元素进行分组，并返回分组界限对应的索引 }}
+ 实现：
  ```java
    //{{c1::
    private static void sort(Comparable[] a, int lo, int hi) {
        if (hi<=lo){
            return;
        }
        int partition = partition(a, lo, hi);
        sort(a,lo,partition-1);
        sort(a,partition+1,hi);
    }

    public static int partition(Comparable[] a, int lo, int hi) {
        Comparable key = a[lo];
        int left=lo;
        int right=hi+1;

        while(true){
            while(less(key,a[--right])){
                if (right==lo){
                    break;
                }
            }

            while(less(a[++left],key)){
                if (left==hi){
                    break;
                }
            }
            if (left>=right){
                break;
            }else{
                exch(a,left,right);
            }
        }
        exch(a,lo,right);
       return right;
    }
    //}}
  ```

# 树 [ ](dataStructure_20210121111221939)

## 树的基本概念与术语 [ ](dataStructure_20210129110102584)

### 树的基本概念 [ ](dataStructure_20210121111221941)

+ 树的定义：{{c1:: 树是n(n>0)个节点的有限集。当n=0时，称为空树。 }}
+ 在任意一棵非空树中应满足：
  1. {{c1:: 有且仅有一个特定的称为根的结点。 }}
  2. {{c1:: 当n>1时，其余节点可分为m(m>0)个互不相交的有限集T1,T2…,Tm,其中每个集合本身又是一棵树，并且称为根的子树。 }}
+ 树前驱后继的特点：
  1. {{c1:: 树的根结点没有前驱 ， 除根结点外的所有结点有且只有一个前驱 。 }}
  2. {{c1:: 树中所有结点可以有零个或多个后继 。 }}
+ 树的边：{{c1:: n个结点的树中有n-1条边 }}

### 树的基本术语 [ ](dataStructure_20210121111221943)
+ 示范图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210119204558.png) }}
+ **祖先** **子孙** **双亲** **孩子** **兄弟**：{{c1:: 考虑结点K。根A到结点K的唯一路径上的任意结点，称为结点K的祖先。如结点B是结点K的祖先，而结点K是结点B的子孙。路径上最接近结点K的结点E称为K的双亲，而K为结点E的孩子。根A是树中唯一没有双亲的结点。有相同双亲的结点称为兄弟，如结点K和结点L有相同的双亲E,即K和L为兄弟 }}
+ **结点的度** **树的度**：{{c1:: 树中一个结点的孩子个数称为该**结点的度**，树中结点的最大度数称为**树的度**。如结点B的度为2,结点D的度为3,树的度为3。 }}
+ **分支节点** **叶子节点**：{{c1:: 度大于0的结点称为分支结点（又称非终端结点）度为0（没有子女结点）的结点称为叶子结点（又称终端结点）。在分支结点中，每个结点的分支数就是该结点的度。 }}
+ 结点的**深度**、**高度**和**层次**：{{c1:: **结点的层次**从树根开始定义，根结点为第1层，它的子结点为第2层，以此类推。双亲在同一层的结点互为**堂兄弟**，图5.1中结点G与E,F,H,I,J互为堂兄弟，**结点的深度**是从根结点开始自顶向下逐层累加的。**结点的高度**是从叶结点开始自底向上逐层累加的。**树的高度**（或深度）是树中结点的最大层数。图5.1中树的高度为4。 }}
+ **有序树** **无序树**：{{c1:: 有序树和无序树。树中结点的各子树从左到右是有次序的，不能互换，称该树为有序树，否则称为无序树。假设图5.1为有序树，若将子结点位置互换，则变成一棵不同的树。 }}
+ **路径** **路径长度**：{{c1:: 路径和路径长度。树中两个结点之间的路径是由这两个结点之间所经过的结点序列构成的，而路径长度是路径上所经过的边的个数。注意路径是从上向下的。 }}
+ **森林**：{{c1:: 森林。森林是(m≥0)棵互不相交的树的集合。森林的概念与树的概念十分相近，因为只要把树的根结点删去就成了森林。反之，只要给m棵独立的树加上一个结点，并把这m棵树作为该结点的子树，则森林就变成了树 }}

### 树的基本性质 [ ](dataStructure_20210121111221946)
1. 树的结点数:{{c1:: 树中的结点数等于所有结点的度数加1 }}
2. 度为m的树中第i层上:{{c1:: 至多有m<sup>i-1</sup>个结点(i≥1). }}
3. 求树的总节点数：{{c1:: 高度为h的m又树至多有(m<sup>h</sup>-1)/(m-1)个结点°。 }}
4. 求树的最小高度:{{c1:: 具有n个结点的m叉树的最小高度为log<sub>m</sub>(n(m-1)+1)。 }}

## 二叉树 [ ](dataStructure_20210121111221949)

### 二叉树主要特点 [ ](dataStructure_20210121111221952)
+ 5种基本形态: {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210119212713.png) }}
+ 二叉树与度为2的有序树的区别：
1. 结点树区别：{{c1:: 度为2的树至少有3个结点，而二又树可以为空。 }}
2. 左右次序区别：{{c1:: 度为2的有序树的孩子的左右次序是相对于另一孩子而言的，若某个结点只有一个孩子则这个孩子就**无须区分其左右次序**，而二叉树无论其孩子数是否为2,**均需确定其左右次序**，即二又树的结点次序不是相对于另一结点而言，而是确定的。 }}

### 特殊二叉树 [ ](dataStructure_20210121111221955)
+ **满二叉树**：{{c1:: 高度为h,含有2~h-1个结点的二叉树 }}
+ **完全二叉树**：{{c1:: 在满二叉树的基础上可去掉若干个编号更大的结点 }}
+ **二叉排序树**：{{c1:: 左子树关键字<根节点关键字<右子树关键字 }}
+ **平衡二叉树**：{{c1:: 左右子树深度差不超过1 }}

### 二叉树的性质 [ ](dataStructure_20210121111221958)
+ **n<sub>0</sub>=n<sub>2</sub>+1**推导过程: {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210119221652.png) }}
+ 第i层的结点数：
  + 二叉树：{{c1:: 二叉树第i层至多有**2<sub>i-1</sub>** 个结点（i≥1） }}
  + m叉树：{{c1:: m叉树第i层至多有**m<sub>i-1</sub>**个结点（i≥1） }}
+ 高度为h的树的结点数：
  + 二叉树：{{c1:: 高度为h的二叉树至多有 **2<sub>ℎ</sub> − 1**个结点（满二叉树） }}
  + m叉树：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210119222726.png) }}
    + 等比数列求和公式:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210119222750.png) }}

### 二叉树的顺序存储 [ ](dataStructure_20210121111221960)
+ 二叉树顺序存储定义：
  ```C
  //{{c1::
  #define MaxSize 100
  struct TreeNode {
    ElemType value;
    bool isEmpty;
  };
  TreeNode t[maxSize];
  //}}
  ```
+ 常用基本操作：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210119232317.png) }}
+ 回答：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210119232237.png) }}

### 二叉树的链式存储 [ ](dataStructure_20210121111221962)
+ 二叉树链式存储定义：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210119233500.png) }}
+ 基本操作实现：
  + 定义一颗空树，插入根节点：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210119233539.png) }}
  + 插入新节点：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210119233621.png) }}
+ 二叉链表空指针域的数量：{{c1:: n个结点的二叉链表共有 n+1 个空链域 }}

### 二叉树的遍历（手算练习） [ ](dataStructure_20210121111221965)
+ 问题:![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210120002829.png)
+ 答案：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210120002907.png)

### 二叉树的前/中/后遍历实现 [ ](dataStructure_20210121111221967)
+ 前序：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210120003305.png) }}
+ 中序：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210120003208.png) }}
+ 后序：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210120003228.png) }}

### 二叉树的层次遍历 [ ](dataStructure_20210121111221970)
+ 算法思想：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210120003914.png) }}
+ 实现：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210120003506.png) }}

### 求树的深度实现（例） [ ](dataStructure_20210121111221974)
+ 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210120003734.png) }}

### 由遍历序列构造二叉树 [ ](dataStructure_20210121111221976)
+ 必要条件：{{c1:: 若给出一棵二叉树的 前/中/后/层 序遍历序列中的两种，可以确定唯一二叉树 }}
+ 构造思路：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210120004440.png) }}

### 线索二叉树 [ ](dataStructure_20210122105026658)
+ 作用：{{c1:: 方便从一个指定结点出发，找到其前驱、后继；方便遍历 }}
+ 存储结构定义：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210121233225.png) }}

### 寻找二叉树的中序前驱实现 [ ](dataStructure_20210122105026660)
+ 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210121233642.png) }}
+ 注意：{{c1:: 最后一个结点的 rchild、rtag的处理 }}


### 二叉树线索化:中序线索化实现 [ ](dataStructure_20210122105026663)

+ 推荐版本: {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210121233842.png) }}
+ 教材版本：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210121233909.png) }}

### 二叉树线索化:先序线索化实现 [ ](dataStructure_20210122105026666)

+ 推荐版本:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210121234502.png) }}
+ 教程版本:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210121234529.png) }}
+ 注意：{{c1:: 先序线索化中，注意处理爱滴隨力转圈圈问题，当tag==0时，オ能对左子树先序线索化 }}


### 二叉树线索化:后序线索化实现 [ ](dataStructure_20210122105026669)

+ 推荐版本：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210121234608.png) }}
+ 教材版本:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210121234635.png) }}


## 树 [ ](dataStructure_20210122105026672)

### 树的存储结构 [ ](dataStructure_20210122105026674)
+ 双亲表示法(顺序存储)存储结构定义:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210121235131.png) }}
  + 优点：{{c1:: 查指定结点的双亲很方便 }}
  + 缺点：{{c1:: 查指定结点的孩子只能**从头遍历** }}
  + 与二叉树的顺序存储区别:二叉树的顺序存储结点编号不仅反映了存储位置，也隐含了结点之间的逻辑关系
+ 孩子表示法（顺序+链式存储）定义：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210121235717.png) }}

### 孩子兄弟表示法（链式存储） [ ](dataStructure_20210122105026676)
+ 定义：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210121235853.png) }}
+ 森林与二叉树的转换思路:{{c1:: 用二叉链表存储森林一左孩子右兄弟,森林中各个树的根节点之间视为兄弟关系 }}

### 树、森林、二叉树的遍历对应关系 [ ](dataStructure_20210122105026678)
+ 对应关系：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210122002801.png) }}

## 二叉树的应用 [ ](dataStructure_20210129110102586)

### 二叉排序树：查找操作实现 [ ](dataStructure_20210128043003554)

+ 查找操作实现：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210123120538.png)

### 二叉排序树：插入\构造操作实现 [ ](dataStructure_20210128043003557)
+ 插入操作实现：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210123120923.png) }}
+ 构造操作实现：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210123121046.png) }}

### 二叉排序树：删除节点思路 [ ](dataStructure_20210128043003559)
+ 实现过程思路：
  1. {{c1:: 若被删除结点z是叶结点，则直接删除，不会破坏二叉排序树的性质。 }}
  2. {{c1:: 若结点z只有一棵左子树或右子树，则让z的子树成为z父结点的子树，替代z的位置。 }}
  3. {{c1:: 若结点z有左、右两棵子树，则令z的直接后继（或直接前驱）替代z,然后从二叉排序树中删去这个直接后继（或直接前驱），这样就转换成了第一或第二种情况。 }}

### 二叉排序树：查找效率分析 [ ](dataStructure_20210128043003561)
+ 查找成功，平均查找长度：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210123122037.png) }}
+ 查找失败，平均查找长度：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210123122339.png) }}

### 平衡二叉树 [ ](dataStructure_20210128043003564)
+ 定义：{{c1:: 平衡二叉树（Balanced Binary Tree），简称平衡树（AVL树）——树上任一结点的左子树和右子树的高度之差不超过1。 }}
+ **平衡因子**的定义：{{c1:: 结点的平衡因子=左子树高-右子树高。 }}
  + 平衡二叉树结点的平衡因子:{{c1:: 只可能是−1、0或1,只要有任一结点的平衡因子绝对值大于1，就不是平衡二叉树 }}

### 平衡二叉树的插入 [ ](dataStructure_20210128043003566)
+ 主要思路：{{c1:: 在插入操作中，只要将最小不平衡子树调整平衡，则其他祖先结点都会恢复平衡 }}
  + 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210123123301.png) }}
+ 调整最小不平衡子树4种情况
  1. `LL`:{{c1:: 在A的左孩子的左子树插入导致A不平衡，将A的左孩子右上旋 }}
  2. `RR`:{{c1:: 在A的右孩子的右子树插入导致A不平衡，将A的右孩子左上旋 }}
  3. `LR`:{{c1:: 在A的左孩子的右子树插入导致A不平衡，将A的左孩子的右孩子先左上旋再右上旋 }}
  4. `RL`:{{c1:: 在A的右孩子的左子树插入导致A不平衡，将A的右孩子的左孩子先右上旋再左上旋 }}

### 调整最小不平衡子树代码思路：左旋/右旋 [ ](dataStructure_20210128043003568)
+ 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210123151301.png) }}

### 高为h的平衡二叉树最少有几个结点,递推求解 [ ](dataStructure_20210128043003571)
+ 假设以n<sub>h</sub>表示深度为h的平衡树中含有的最少结点数。则有{{c1:: n<sub>0</sub> = 0, n<sub>1</sub> = 1, n<sub>2</sub> = 2，并且有nh = n<sub>h−1</sub> + n<sub>h−2</sub> + 1 }}

### 哈夫曼树定义 [ ](dataStructure_20210128043003575)
+ 定义：{{c1:: 在含有n个带权叶结点的二叉树中，其中带权路径长度（WPL）最小的二叉树称为哈夫曼树，也称最优二叉树 }}
+ 结点的权：{{c1:: 有某种现实含义的数值（如：表示结点的重要性等） }}
+ 结点的带权路径长度：{{c1:: 从树的根到该结点的**路径长度**（经过的边数）与该结点上**权值**的**乘积** }}
+ 树的带权路径长度：{{c1:: 树中所有**叶结点**的带权路径长度之和（WPL, Weighted Path Length） }}


### 哈夫曼树构造 [ ](dataStructure_20210128043003577)
+ 给定n个权值分别为w1, w2,…, wn的结点，构造哈夫曼树的算法描述如下：
  1. {{c1:: 将这n个结点分别作为n棵仅含一个结点的二叉树，构成森林F。 }}
  2. {{c1:: 构造一个新结点，从F中选取两棵根结点权值最小的树作为新结点的左、右子树，并且将新结点的权值置为左、右子树上根结点的权值之和。 }}
  3. {{c1:: 从F中删除刚才选出的两棵树，同时将新得到的树加入F中。 }}
  4. {{c1:: 重复步骤2）和3），直至F中只剩下一棵树为止。 }}
+ 图示步骤：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210123152905.png) }}

### 哈夫曼编码 [ ](dataStructure_20210128043003579)

+ **固定长度编码**:{{c1:: 每个字符用相等长度的二进制位表示 }}
+ **可变长度编码**:{{c1:: 允许对不同字符用不等长的二进制位表示 }}
+ **前缀编码**:{{c1:: 若没有一个编码是另一个编码的前缀，则称这样的编码为前缀编码 }}
+ **哈夫曼编码**:{{c1:: 将字符频次作为字符结点权值，构造哈夫曼树，即可得哈夫曼编码，可用于数据压缩 }}
  + 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210123154802.png) }}

# 图 [ ](dataStructure_20210128043003582)

## 图的基本概念与术语 [ ](dataStructure_20210129110102590)

### 图的定义 [ ](dataStructure_20210128043003584)

+ 定义：{{c1:: 图G由顶点集V和边集E组成，记为`G=(V,E)`,其中`V(G)`表示图G中顶点的有限非空集，`E(G)`表示图G中顶点之间的关系（边）集合 }}
  + `|V|`:{{c1:: 顶点数 }}
  + `|E|`：{{c1:: 边数,若 `|E|>n-1`，则一定有回路}}
+ 注意：{{c1:: 线性表可以是空表，树可以是空树，但图不可以是空，即V一定是非空集 }}
  

### 图的基本概念与术语 [ ](dataStructure_20210128043003587)
+ **有向图**、**无向图**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210127212308.png) }}
+ **简单图**、**多重图**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210127212424.png) }}

### 图中顶点的度、入度、出度 [ ](dataStructure_20210128043003589)
+ **无向图**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210127212817.png) }}
+ **有向图**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210127212825.png) }}

### 图中顶点-顶点的关系描述 [ ](dataStructure_20210128043003591)
+ **路径**：{{c1:: 顶点v<sub>p</sub>到顶点v<sub>q</sub>之间的一条路径是指顶点序列 ， }}
+ **回路**：{{c1:: 第一个顶点和最后一个顶点相同的路径称为回路或环 }}
+ **简单路径**：{{c1:: 在路径序列中，顶点不重复出现的路径称为简单路径。 }}
+ **简单回路**：{{c1:: 除第一个顶点和最后一个顶点外，其余顶点不重复出现的回路称为简单回路。 }}
+ **路径长度**：{{c1:: 路径上边的数目 }}
+ **距离**：{{c1:: 点到点的距离,从顶点u出发到顶点v的最短路径若存在，则此路径的长度称为从u到v的距离。若从u到v根本不存在路径，则记该距离为无穷（∞）。 }}

### 连通图与强连通图 [ ](dataStructure_20210128043003593)
+ **顶点连通**: {{c1:: 无向图中，若从顶点v到顶点w有路径存在，则称v和w是连通的 }}
+ **顶点强连通**: {{c1:: 有向图中，若从顶点v到顶点w和从顶点w到顶点v之间都有路径，则称这两个顶点是强连通的 }}
+ **连通图**:{{c1:: 若图G中任意两个顶点都是连通的，则称图G为连通图，否则称为非连通图。}}
+ **强连通图**:{{c1:: 若图中任何一对顶点都是强连通的，则称此图为强连通图。 }}
+ 连通图最少边数量：
  + 若G是连通图，{{c1:: 则最少有 n-1 条边 }}
  + 若G是强连通图，{{c1:: 则最少有 n 条边（形成回路） }}

### 子图 [ ](dataStructure_20210128043003595)
+ **子图**:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210127215739.png) }}
+ **生成子图**:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210127215746.png) }}
+ **极大连通子图**:{{c1:: 子图必须连通，且包含尽可能多的顶点和边 }}
+ **极大强连通子图**:{{c1:: 子图必须强连通，同时
保留尽可能多的边 }}
+ **连通分量**:{{c1:: **无向图**中的**极大连通子图**称为**连通分量**。 }}
+ **强连通分量**:{{c1:: 有向图中的**极大强连通子图**称为有向图的**强连通分量** }}

### 生成树 生成森林 [ ](dataStructure_20210128043003598)
+ **生成树** : {{c1:: 连通图的生成树是包含图中全部顶点的一个极小连通子图。 }}
+ **生成森林** : {{c1:: 在非连通图中，连通分量的生成树构成了非连通图的生成森林。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210127220704.png) }}

### 边的权、带权图/网 [ ](dataStructure_20210128043003602)
+ **边的权**:{{c1:: 在一个图中，每条边都可以标上具有某种含义的数值，该数值称为该边的权值。 }}
+ **带权图/网**:{{c1:: 边上带有权值的图称为带权图，也称网。 }}
+ **带权路径长度**:{{c1:: 当图是带权图时，一条路径上所有边的权值之和，称为该路径的带权路径长度 }}

### 特殊形态的图 [ ](dataStructure_20210128043003604)
+ **无向完全图**:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210127221155.png) }}
+ **有向完全图**:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210127221217.png) }}
+ **稀疏图**、**稠密图**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210127221308.png) }}
+ **树**:{{c1:: 不存在回路，且连通的无向图 }}
+ **有向树**:{{c1:: 一个顶点的入度为0、其余顶点的入度均为1的有向图，称为有向树。 }}

### 图的常见结论 [ ](dataStructure_20210129110102592)
+ 对于n个顶点的无向图G：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210128202212.png) }}
+ 对于n个顶点的有向图G：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210128202234.png) }}

## 图的存储结构 [ ](dataStructure_20210129110102594)

### 图的存储结构：邻接矩阵 [ ](dataStructure_20210129110102596)

+ 顺序结构定义：
  ```c++
  //{{c1::
  #define MaxVertexNum 100                //顶点数目的最大值
  typedef struct{                         
    char Vex[MaxVertexNum]                //顶点表
    int Edge[MaxVertexNum][MaxVertexNum]  //邻接矩阵，边表
    int vexnum,arcnum;                    //图的当前顶点数和边数/弧数
  }MGraph;
  //}}
  ```
+ 邻接矩阵法存储带权图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210128204430.png) }}

### 图的存储结构：邻接矩阵法求度 [ ](dataStructure_20210129110102599)
  + 求无向图的度：
    + 第i个结点的度 ={{c1:: 第i行（或第i列）的非零元素个数 }}
  + 有向图的度：
    + 第i个结点的出度 ={{c1:: 第i行的非零元素个数 }}
    + 第i个结点的入度 ={{c1:: 第i列的非零元素个数 }}
    + 第i个结点的度 ={{c1:: 第i行、第i列的非零元素个数之和 }}
  + 邻接矩阵法求顶点的度/出度/入度的时间复杂度为:{{c1:: `O(|V|)` }}

### 图的存储结构：邻接矩阵法的性能 [ ](dataStructure_20210129110102601)
  + 空间复杂度：{{c1:: O(|V|<sub>2</sub>) ——只和顶点数相关，和实际的边数无关 }}
  + 适合用于的图：{{c1:: 存储稠密图 }}
  + 无向图的邻接矩阵是对称矩阵，{{c1:: 可以压缩存储（只存储上三角区/下三角区） }}

### 图的存储结构：邻接矩阵法的重要性质： [ ](dataStructure_20210129110102603)
+ `A<sup>n</sup>[i][j]`表示:{{c1::设图G的邻接矩阵为A（矩阵元素为0/1），则`A<sup>n</sup>`的元素`A<sup>n</sup>[i][j]`等于由顶点i到顶点j的长度为n的路径的数目}}
+ 图解：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210128212658.png)}}


### 图的存储结构：邻接表法（顺序+链式存储）定义 [ ](dataStructure_20210129110102606)
+ 可视化图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210128223110.png)
+ 顶点定义：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210128222934.png)
+ “边/弧”定义：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210128223014.png)
+ 图定义：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210128223033.png)

### 图的存储结构：邻接表VS邻接矩阵 [ ](dataStructure_20210129110102609)

|                  | 邻接表                                                 | 邻接矩阵                                |
| ---------------- | ------------------------------------------------------ | --------------------------------------- |
| 空间复杂度       | {{c1:: 无向图 `O(|V| + 2|E|)` ；有向图`O(|V| + |E|)`}} | {{c1:: **O(\|V\|<sup>2</sup>)**  过高}} |
| 适合用于         | {{c1:: 存储稀疏图}}                                    | {{c1:: 存储稠密图  }}                   |
| 表示方式         | {{c1:: 不唯一    }}                                    | {{c1:: 唯一  }}                         |
| 计算度/出度/入度 | {{c1::计算有向图的度、入度不方便，其余很方便 }}        | {{c1:: 必须遍历对应行或列  }}           |
| 找相邻的边       | {{c1:: **找有向图的入边不方便**，其余很方便}}          | {{c1:: 必须遍历对应行或列 }}            |

###   图的存储结构：十字链表 [ ](dataStructure_20210129110102611)
+ 弧结点结构:{{c1::![image-20210128235152298](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210128235152298.png)}}
+ 顶点结点结构：{{c1::![image-20210128235214230](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210128235214230.png)}}
+ 逻辑图例：{{c1::![image-20210128235319936](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210128235319936.png)}}
+ 如何找到指定顶点的所有出边？{{c1::**顺着绿色线路找**}}
+ 如何找到指定顶点的所有入边？{{c1::**顺着橙色线路找**}}

###   图的存储结构：邻接多重表 [ ](dataStructure_20210129110102613)
+ 边结点结构:{{c1::![image-20210128235935671](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210128235935671.png)}}
+ 顶点结点结构：{{c1::![image-20210128235942664](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210128235942664.png)}}
+ 逻辑图例：{{c1::![image-20210128235954721](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210128235954721.png)}}
+ 删除`A-B`后指针走向：{{c1::![image-20210129000133033](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210129000133033.png)}}
+ 删除E结点后指针走向：{{c1::![image-20210129000242750](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210129000242750.png)}}

### 图的4种存储结构总结 [ ](dataStructure_20210129110102616)
+ 问：![image-20210129001224371](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210129001224371.png)
+ 答：{{c1::![image-20210129000957867](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210129000957867.png)}}

### 图的基本操作 [ ](dataStructure_20210129110102620)
+ `Adjacent(G,x,y)`：判断图G是否存在边`<x, y>`或`(x, y)`。
+ `Neighbors(G,x)`：列出图G中与结点x邻接的边。
+ `InsertVertex(G,x)`：在图G中插入顶点x。
+ `DeleteVertex(G,x)`：从图G中删除顶点x。
+ `AddEdge(G,x,y)`：若无向边`(x, y)`或有向边`<x, y>`不存在，则向图G中添加该边。
+ `RemoveEdge(G,x,y)`：若无向边`(x, y)`或有向边`<x, y>`存在，则从图G中删除该边。
+ `FirstNeighbor(G,x)`：求图G中顶点x的第一个邻接点，若有则返回顶点号。若x没有邻接点或图中不存在x，则返回-1。
+ `NextNeighbor(G,x,y)`：假设图G中顶点y是顶点x的一个邻接点，返回除y之外顶点x的下一个邻接点的顶点号，若y是x的最后一个邻接点，则返回-1。
+ `Get_edge_value(G,x,y)`：获取图G中边`(x, y)`或`<x, y>`对应的权值。
+ `Set_edge_value(G,x,y,v)`：设置图G中边`(x, y)`或`<x, y>`对应的权值为v。
+ 标签：{{c1::理解}}

## 图的遍历 [ ](dataStructure_20210129110102622)

### 图的广度优先遍历 [ ](dataStructure_20210129110102625)

+ ⼴度优先遍历（Breadth-First-Search, BFS）思路：
  1. {{c1:: 找到与⼀个顶点相邻的所有顶点 }}
  2. {{c1:: 标记哪些顶点被访问过 }}
  3. {{c1:: 需要⼀个辅助队列 }}
+ 代码实现：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210129003031.png) }}
+ 基本操作定义：
    + `FirstNeighbor(G,x)`：求图G中顶点x的第⼀个邻接点，若有则返回顶点号。若x没有邻接点或图中不存在x，则返回-1。
    + `NextNeighbor(G,x,y)`：假设图G中顶点y是顶点x的⼀个邻接点，返回除y之外顶点x的下⼀个邻接点的顶点号，若y是x的最后⼀个邻接点，则返回-1。
+ 遍历序列的可变性:{{c1:: 同⼀个图的**邻接矩阵**表示⽅式唯⼀，因此⼴度优先遍历序列**唯⼀**,同⼀个图**邻接表**表示⽅式不唯⼀，因此⼴度优先遍历序列**不唯⼀** }}