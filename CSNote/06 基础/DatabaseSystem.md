## 概论 [ ](DatabaseSystem_20210210110450187)

### 数据库核心划分 [ ](DatabaseSystem_20210210110450189)

+ 7大部分图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209201627.png)}}

### 数据库系统课程与其他课程之间的关系 [ ](DatabaseSystem_20210210110450192)

+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209201925.png)}}

### Table的构成暨关于Table的常用术语 [ ](DatabaseSystem_20210210110450194)

+ 列/字段/属性/数据项
+ 行/元组/记录
+ (关系)模式
+ 表/关系
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209203109.png)}}

### 什么是数据库系统? [ ](DatabaseSystem_20210210110450196)

+ **DB**：{{c1::数据库(DB): Database}}
+ **DBMS**：{{c1::数据库管理系统(DBMS): Database Management System}}
+ **DBAP**：{{c1::数据库应用(DBAP): DataBase Application}}
+ **DBA**：{{c1::数据库管理员(DBA): DataBase Administrator}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209203645.png)}}

## 数据库系统的结构抽象 [ ](DatabaseSystem_20210210110450198)

### 数据库系统的标准结构：DBMS管理数据的三个层次 [ ](DatabaseSystem_20210210110450201)

**External Level**: {{c1:: **User Level** 某一用户能够看到与处理的数据,   全局数据中的某一部分}}
**Conceptual Level**: {{c1:: **Logic level** 从全局角度理解/管理的数据, 含相应的关联约束}}
**Internal Level**: {{c1:: **Physical level** 存储在介质上的数据，含存储路径、存储方式 、索引方式等}}

+ 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209211746.png)}}

### 数据库系统的标准结构：数据与数据的结构（模式） [ ](DatabaseSystem_20210210110450203)

+ **Schema**：{{c1::模式(Schema)对数据库中数据所进行的一种结构性的描述，所观察到数据的结构信息}}
+ **View/Data**：{{c1::视图(View)/数据(Data)某一种表现形式下表现出来的数据，库中的数据}}
+ 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209212118.png)}}

### 数据库系统的标准结构：三级模式两层映像 [ ](DatabaseSystem_20210210110450205)

+ 三级模式:
  + **External Schema**:{{c1::(External) View,某一用户能够看到与处理的数据的结构描述}}
  + **(Conceptual) Schema**:{{c1::Conceptual View,从全局角度理解/管理的数据的结构描述, 含相应的关联约束,体现在数据之间的内在本质联系}}
  + **Internal Schema**:{{c1::Internal  View,存储在介质上的数据的结构描述，含存储路径、存储方式 、索引方式等}}
+ 两层映像:
  + **E-C Mapping**：{{c1::**External Schema-Conceptual Schema Mapping**,将外模式映射为概念模式，从而支持实现数据概念视图向外部视图的转换,便于用户观察和使用}}
  + **C-I Mapping**：{{c1::**Conceptual Schema-Internal Schema Mapping**，将概念模式映射为内模式，从而支持实现数据概念视图向内部视图的转换,便于计算机进行存储和处理}}
+ 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209213434.png)}}

### 数据库系统的标准结构：三级模式两层映像 [ ](DatabaseSystem_20210210110450208)

+ 两个独立性
  + 逻辑数据独立性：{{c1::当概念模式变化时，可以不改变外部模式(只需改变E-C Mapping)，从而无需改变应用程序}}
  + 物理数据独立性：{{c1::当内部模式变化时，可以不改变概念模式(只需改变C-I Mapping) ，从而不改变外部模式}}
+ 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209220736.png)}}

### 数据模型 [ ](DatabaseSystem_20210210110450212)

+ 数据模型：{{c1::数据模型是对模式本身结构的抽象，模式是对数据本身结构形式的抽象}}
+ 三大经典数据模型
  + 关系模型：{{c1::表的形式组织数据}}
  + 层次模型：{{c1::树的形式组织数据}}
  + 网状模型：{{c1::图的形式组织数据}}
+ 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209235136.png)}}

### 数据库系统的演变与发展 [ ](DatabaseSystem_20210210110450215)

+ 由文件系统到数据库：{{c1::主要不足为数据的组织及语义紧密依赖于处理该文件的应用程序**高度耦合**}}
+ 由层次/网状模型数据库到关系数据库：{{c1::主要不足为数据之间的关联关系由复杂的指针系统来维系，**结构描述复杂**}}
+ 由关系数据库到对象关系数据库、面向对象数据库：
  + 对象-关系数据库：{{c1::可有效支持不满足关系第
    1范式的数据项，![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209234714.png)}}
  + 面向对象数据库：{{c1::面向对象技术(O-O)与集合/聚集操作技术(SQL)的结合}}
+ 由普通数据库到与各种先进技术结合所形成的新型数据库：
  + {{c1::**Statistical Database**： DB + 统计学。}}
  + {{c1::**Internet Database**： DB + Internet/WWW(网页/HTML文档)。...}}

## 表的严格定义

### “表”的严格定义：关系 [ ](DatabaseSystem_20210210110450217)

+ **Domain**：
  + 定义：{{c1::域(Domain)，一组值的集合，这组值具有相同的数据类型}}
  + **Cardinality**：{{c1::集合中元素的个数称为域的基数(Cardinality)}}
+ 一组域D1 , D2 ,…, Dn的笛卡尔积为:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210210005850.png)}}
  + **n-元组**：{{c1::笛卡尔积的每个元素(d1 , d2 , … , dn)称作一个n-元组（n-tuple）}}
  + **分量**：{{c1::元组(d1 , d2 , … , dn)的每一个值di叫做一个分量(component)}}
  + 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210210010005.png)}}
+ 若D<sup>i</sup>的基数为m<sup>i</sup>，则笛卡尔积的基数，即元组个数为：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210210010947.png)}}
+ 关系(Relation):{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210210011539.png)}}
+ 关系模式描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210210012254.png)}}
+ 关系模式与关系：
  + 同一关系模式下，{{c1::可有很多的关系}}
  + 关系模式是关系的结构：{{c1::关系是关系模式在**某一时刻**的数据}}
  + 关系模式是稳定的：{{c1::而关系是某一时刻的值，是随时间**可能变化的**}}
  + 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210210012720.png)}}
+ 关系定义整体回顾：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210210013200.png)}}

### 关系的特性 [ ](DatabaseSystem_20210210110450221)

+ 列是同质：{{c1::即每一列中的分量来自同一域，是同一类型的数据}}
+ 不同的列可来自同一个域：{{c1::称其中的每一列为一个属性，不同的属性要给予不同的属性名。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210210022142.png)}}
+ 列位置互换性：{{c1::区分哪一列是靠列名}}
+ 行位置互换性：{{c1::区分哪一行是靠**某一**或**某几**列的值(关键字/键字/码字)}}
+ 注意元组的重复：{{c1::理论上，关系的任意两个元组不能完全相同。(集合的要求：集合内不能有相同的两个元素)；现实应用中，**表(Table)**可能并不完全遵守此特性。}}

### 关系的第一范式 [ ](DatabaseSystem_20210210110450224)

+ 第一范式：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210210022538.png)}}

### 关系上的重要概念

+ **Candidate Key**: {{c1::候选码(Candidate Key),关系中的一个**属性组**，其值能**唯一标识**一个元组，若从该属性组中去掉任何一个属性，它就不具有这一性质了，这样的属性组称作候选码。}}
+ **Primary Key**: {{c1::当有多个候选码时，可以选定一个作为主码.DBMS以主码为主要线索管理关系中的各个元组。}}
+ **主属性与非主属性**：{{c1::包含在任何一个候选码中的属性被称作主属性，而其他属性被称作非主属性}}
  + 最简单的，{{c1::候选码只包含一个属性}}
  + 最极端的，{{c1::所有属性构成这个关系的候选码，称为全码(All-Key)。}}
+ **Foreign Key**：{{c1::外码(Foreign Key)/外键，关系R中的一个属性组，它不是R的候选码，但它与另一个关系S的候选码相对应，则称这个属性组为R的外码或外键。}}
+ 关系与表概念对应图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210211041941.png)}}

### 关系模型中的完整性:关系完整性

+ **实体完整性**: {{c1::关系的主码中的属性值不能为空值；若主码为空，则出现不可标识的个体，这是不容许的；}}
+ **参照完整性**: {{c1::如果关系R1的外码**Fk**与关系**R2**的主码**Pk**相对应，则**R1**中的每一个元组的**Fk**值或者等于**R2**中某个元组的**Pk值**，**或者**为**空值**}}
  + 意义：{{c1::如果关系**R1**的某个元组**t1**参照了关系**R2**的某个元组**t2**，则**t2**必须存在}}
+ **用户自定义完整性**: {{c1::用户针对具体的应用环境定义的完整性约束条件}}
+ **DBMS对关系完整性的支持**: {{c1::实体完整性和参照完整性由DBMS系统**自动支持**,它使用户可以自行定义有关的完整性约束条件,当有更新操作发生时，DBMS将自动按照完整性约束条件检验更新操作的正确性，即是否符合用户自定义的完整性}}

## 关系代数

### 关系代数操作：集合操作和纯关系操作

+ 问：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214022227.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214022148.png)}}

### 关系代数概念：并相容性

+ 定义：关系R与关系S存在相容性，当且仅当：
  1. {{c1::关系R和关系S的**属性数目**必须相同；}}
  2. {{c1::对于任意i，关系R的第i个属性的域必须和关系S的第i个属性的**域相同**}}
+ 例：
  + 假设：`R(A1, A2, … , An)` , `S(B1, B2, … ,Bm)`R和S满足并相容性：
  + 那么：{{c1:: `n = m` 并且 `Domain(Ai) = Domain(Bi)` }}

### 关系代数基本操作：“并”操作

+ 定义：{{c1::假设关系R和关系S是并相容的，则关系R与关系S的并运算结果也是一个关系，记作：R ∪S, 它由或者出现在关系R中，或者出现在S中的元组构成。在合并时去掉重复的元组。}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214023344.png)}}
+ 对应汉语：{{c1::汉语中的“或者…或者…”通常意义是并运算的要求。}}

### 关系代数基本操作：“差”操作

+ 定义：{{c1::假设关系R和关系S是并相容的，则关系R与关系S的差运算结果也是一个关系，记作：R-S,它由**出现在**关系R中**但不出现在**关系S中的元组构成。}}
+ 数学描述：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214024051.png)
+ 对应汉语：{{c1::是…但不含…}}

### 关系代数基本操作：“笛卡尔积”操作

+ 定义：{{c1::关系`R(<a1,a2,…,an>)`与关系`S(<b1,b2,…,bm>)`的广义笛卡尔积(简称广义积,或积或笛卡尔积)运算结果也是一个关系，记作：`RxS`,它由关系R中的元组与关系S的元组进行所有可能的拼接(或串接)构成。}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214024254.png)}}
+ 关系R的元组数目是3，度数是3; 关系S的元组数目是4, 度数是3;
  + 则RxS的元组：{{c1::数目是12, 度数是6 ?}}

### 关系代数基本操作：“选择”操作

+ 定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214024950.png)}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214025002.png)}}
+ 运算符的优先次序:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214025414.png)}}

### 关系代数基本操作：“投影”操作

+ 定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214034546.png)}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214034703.png)}}

### 关系代数拓展操作：“交”操作

+ 定义：{{c1::假设关系R和关系S是并相容的，则关系R与关系S的交运算结果也是一个关系，记作：**R∩S**, 它由**同时出现在**关系R和关系S中的元组构成。}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214035424.png)}}
+ 交运算可以通过差运算来实现：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214035449.png)}}
+ 对应汉语例：{{c1::“既…又…”，“…, 并且…”}}

### 关系代数拓展操作：“theta-连接”操作

+ 定义:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214040002.png)}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214040013.png)}}
+ **等值连接**数学描述:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214040539.png)}}
+ DBMS对**theta-连接**操作的处理：{{c1::当引入连接操作后，DBMS可直接进行连接操作，而不必先形成笛卡尔积。}}

### 关系代数拓展操作：“自然连接”操作

+ 定义:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214040636.png)}}
+ 数学描述:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214040928.png)}}
+ 特点：
  1. **相同属性组**：{{c1::要求关系R和关系S必须有相同的属性组B(如R,S共有一个属性B1,则B是B1 , 如R, S共有一组属性`B1, B2, …, Bn`，则B是这些共有的所有属性)}}
  2. **值相等**:{{c1::R, S属性相同，值必须相等才能连接，即`R.B1 = S.B1 and R.B2 = S.B2 … and R.Bn = S.Bn`才能连接}}
  3. **去掉重复列**:{{c1::要在结果中去掉重复的属性列}}

### 关系代数的基本书写思路：

1. {{c1::选出将用到的关系/表}}
2. {{c1::做“积”运算(可用连接运算替换)}}
3. {{c1::做选择运算保留所需的行/元组}}
4. {{c1::做投影运算保留所需的列/属性}}

### 关系代数练习

+ 问：![image-20210214063757529](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210214063757529.png)![image-20210214063839810](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210214063839810.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214064715.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214064054.png)}}

### 关系代数扩展操作:除(Division）

+ 常用于求解:{{c1::**“查询… 全部的/所有的…”**问题}}
+ 前提条件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214065239.png)}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214070714.png)}}
+ 定义
  + R除S结果的属性应有哪些：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214065804.png)}}
  + R除S结果的元组怎样形成：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214070514.png)}}

### 关系代数扩展操作:除(Division）练习

+ 表结构：![image-20210214071621781](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210214071621781.png)
+ 题：![image-20210214071751337](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210214071751337.png)
+ 答：{{c1::![image-20210214071735115](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210214071735115.png)}}

### 关系代数扩展操作:“外连接”操作

+  外连接的形式：{{c1::左外连接、右外连接、全外连接}}
   + 左外连接 = {{c1::自然连接(或theta连接) + 左侧表中**失配的元组**}}
   + 右外连接 = {{c1::自然连接(或theta连接) + 右侧表中**失配的元组**}}
   + 全外连接 = {{c1::自然连接(或theta连接) + 两侧表中**失配的元组**}}
+  左外连接(Left Outer Join)记为：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214072559.png)}}
+  右外连接(Right Outer Join)记为：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214072611.png)}}
+  全外连接(Full Outer Join)记为：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214072620.png)}}

## 关系元组演算

+ 关系元组演算公式的基本形式：{{c1::`{ t | P(t) }`}}
+ 详：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214075752.png)}}

### 关系元组演算例子：全都学过
+ 题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074234.png)
+ 答：
  + 关系代数：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074322.png)}}
  + 关系元组演算：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074330.png)}}


### 关系元组演算例子：全都学过
+ 题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074451.png)
+ 答：
  + 关系代数：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074459.png)}}
  + 关系元组演算：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074509.png)}}


### 关系元组演算例子：至少有一学过
+ 题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074612.png)
+ 答：
  + 关系代数：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074626.png)}}
  + 关系元组演算：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074633.png)}}

### 关系元组演算例子：至少有一没学过
+ 题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074854.png)
+ 答：
  + 关系代数：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074909.png)}}
  + 关系元组演算：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074918.png)}}

### 关系代数转换为元组演算
+ 问：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214075126.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214075530.png)}}

## 关系域演算

### 关系域演算例子
+ 问：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214080340.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214080437.png)}}

## 关系运算总结

### 关系运算的安全性
+ 定义：{{c1::“不产生无限关系和无穷验证的运算被称为是安全的}}
+ 各运算的安全性：
  + 关系代数：{{c1::关系代数是一种集合运算，是安全的}}
  + 关系演算：{{c1::不一定是安全的![image-20210214081134592](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210214081134592.png)}}

### 关系运算总结

+ 关系运算有三种：{{c1::关系代数、关系元组演算和关系域演算}}
+ 三种关系运算都是抽象的数学运算，体现了三种不同的思维
  + 关系代数：{{c1::以集合为对象的操作思维，由集合到集合的变换}}
  + 元组演算：{{c1::以元组为对象的操作思维，取出关系的每一个元组进行验证，有一个元组变量则可能需要一个循环，多个元组变量则需要多个循环}}
  + 域演算：{{c1::以域变量为对象的操作思维，取出域的每一个变量进行验证看其是否满足条件}}

+ **三种运算之间是等价的**：{{c1::关系代数 与 安全的元组演算表达式 与 安的域演算表达式 是等价的。即一种形式的表达式可以被等价地转换为另一种形式}}
+ **三种关系运算都可说是非过程性的**：{{c1::相比之下：域演算的非过程性最，元组演算次之，关系代数最差}}
+ **三种关系运算虽是抽象的，但却是衡量数据库语言完备性的基础**：{{c1::一个数据库语言如果能够等价地实现这三种关系运算的操作，则说该语言是完备的。目前多数数据库语言都能够实现这三种运算的操作，在此基础上还增加了许多其他的操作，如赋值操作、聚集操作等}}

## SQL语言

### SQL语言的功能概述
+ DDL语句引导词：{{c1::Create(建立),Alter(修改),Drop(撤消)}}
+ DML语句引导词：{{c1::Insert ,Delete, Update, Select}}
+ DCL语句引导词：{{c1::Grant,Revoke}}
+ 交互式SQL->嵌入式SQL->动态SQL等

### SQL语言:结果唯一性问题
+ 问题引出：关系模型不允许出现重复元组。但现实DBMS，却允许出现重复元组，但也允许无重复元组。
+ 解决：{{c1::在**Table**中要求无重复元组是通过定义**Primary key**或**Unique**来保证的;而在检索结果中要求无重复元组, 是通过**DISTINCT**保留字的使用来实现的。}}

### `not in` `some` `all` 联系与区别
+ 问：![image-20210217051138257](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210217051138257.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217051201.png)
+ 答：{{c1::注意`<>some`的语义,some等价于any,any由于语义问题被弃用.}}

### EXISTS 子查询
+ 语义：{{c1::子查询结果中有无元组存在}}
+ 示例：检索选修了赵三老师主讲课程的所有同学的姓名:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214090753.png)}}

## SQL语言实现关系代数操作

### SQL语言:并-交-差的处理
+ **SQL语言**：{{c1::并运算 UNION, 交运算INTERSECT, 差运算EXCEPT}}
+ **基本语法形式**：{{c1::子查询 { Union [ALL] | Intersect [ALL] | Except [ALL] 子查询 }}}
+ **通常情况下自动删除重复元组**：{{c1::不带ALL。若要保留重复的元组，则要带ALL。}}
+ 假设子查询1的一个元组出现m次，子查询2的一个元组出现n次
，则该元组在：
  + 子查询1 Union ALL 子查询2 ，{{c1::出现m + n次}}
  + 子查询1 Intersect ALL 子查询2 ，{{c1::出现min(m,n)次}}
  + 子查询1 Except ALL 子查询2 ，{{c1::出现max(0, m – n)次}}
+ 注意：{{c1::有些DBMS不支持INTERSECT,EXCEPT}}

### SQL语言:现行DBMS的空值处理小结
+  除is[not]null之外，{{c1::空值不满足任何查找条件}}
+  如果null参与算术运算，{{c1::则该算术表达式的值为null}}
+  如果null参与比较运算，{{c1::则结果可视为false。在SQL-92中可看成unknown}}
+  如果null参与聚集运算，{{c1::则除count(*)之外其它聚集函数都忽略null}}

### SQL视图更新
+ 原则：{{c1::视图更新要保证原有表的实体完整性。}}
+ 各种视图更新情况：
  + 聚集函数：{{c1::如果视图的select目标列包含聚集函数，则不能更新}}
  + unique或distinct：{{c1::如果视图的select子句使用了unique或distinct，则不能更新}}
  + groupby：{{c1::如果视图中包括了groupby子句，则不能更新}}
  + 算术表达式：{{c1::如果视图中包括经算术表达式计算出来的列，则不能更新}}
  + 主键：{{c1::如果视图是由单个表的列构成，但并没有包括主键，则不能更新}}

## 数据库完整性和安全性

### 数据库完整性
+ 为什么会引发数据库完整性的问题: {{c1::不正当的数据库操作，如输入错误、操作失误、程序处理失误等}}
+ DBMS怎样自动保证完整性呢？
  + {{c1::DBMS允许用户定义一些完整性约束规则(用SQL-DDL来定义)}}
  + {{c1::当有DB更新操作时，DBMS自动按照完整性约束条件进行检查，以确保更新操作符合语义完整性}}
+ 完整性分类：{{c1::![image-20210215165354352](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215165354352.png)}}
+ 完整性约束条件(或称完整性约束规则)的一般形式:{{c1::![image-20210215163705366](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215163705366.png)}}

### SQL语言实现约束的方法-断言

+ 语法形式为：{{c1::`CREATE ASSERTION <assertion-name> CHECK <predicate>`}}
+ 注意：{{c1::断言测试增加了数据库维护的负担，要小心使用复杂的断言。}}
+ 示例：“每笔贷款,要求至少一位借款者账户中存有最低数目的余额，例如1000元”
  ```sql
  #{{c1::
  create assertion balance_constraint check
  (not exists (
    select * from loan
  
    where not exists (
      select * from borrower, depositor, account
      where loan.loan_number = borrower.loan_number
        and borrower.customer_name = depositor.customer_name
        and depositor.account_number = account.account_number
        and account.balance >= 1000)))
  #}}
  ```
### 触发器Trigger
+ 作用：Create Table中的表约束和列约束基本上都是静态的约束，也基本上都是对单一列或单一元组的约束(尽管有参照完整性)，为实现动态约束以及多个元组之间的完整性约束，就需要触发器技术Trigger
+ 示例：设计一个触发器当进行Teacher表更新元组时, 使其工资只能升不能降：{{c1::![image-20210215165016404](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215165016404.png)}}

### 数据库安全性
+ 作用：{{c1::数据库安全性是指DBMS应该保证的数据库的一种特性(机制或手段)：免受非法、非授权用户的使用、泄漏、更改或破坏}}
+ 数据的安全级别: {{c1::绝密(Top Secret), 机密(Secret),可信(Confidential)和无分类(Unclassified) }}
+ 数据库系统DBS的安全级别：{{c1::物理控制、网络控制、操作系统控制、DBMS控制}}

### 自主安全性
+ 数据库自主安全性访问规则：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217051032.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217051049.png)}}
+ 自主安全性的实现方式:
  + 存储矩阵:{{c1::![image-20210215170039634](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215170039634.png)}}
  + 视图:{{c1::![image-20210215170046269](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215170046269.png)}}

### 自主安全性的授权过程及其问题
+ 授权过程:{{c1::![image-20210215210903945](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215210903945.png)}}
+ 传播范围包括两个方面：
+ 水平传播数量: {{c1::是授权者的再授权用户数目(树的广度)}}
+ 垂直传播数量: {{c1::是授权者传播给被授权者，再被传播给另一个被授权者, …传播的深度(树的深度)}}

### 嵌入式SQL语言
+ 需解决的8大问题：
  1. **连接处理**： {{c1::如何与数据库连接和断开连接}}
  2. **变量传递**： {{c1::如何将宿主程序的变量传递给SQL语句}}
  3. **如何执行SQL**： {{c1::SQL语句如何执行}}
  4. **检索结果处理**： {{c1::如何将SQL检索到的结果传递回宿主程序进行处理，变量，游标}}
  5. **常量处理**： {{c1::静态SQL,SQL语句中的常量更换为变量}}
  6. **错误处理**： {{c1::宿主程序如何知道SQL语句的执行状态，是否发生错误}}
  7. **数据库元数据已知的**： {{c1::动态SQL, 依据条件动态构造SQL语句,但欲访问的表名和字段名对编程者是已知的}}
  8. **数据库元数据未知的**： {{c1::动态SQL, 依据条件动态构造SQL语句,但欲访问的表名和字段名对编程者是未知的}}
+ 知识结构：{{c1::![image-20210215212409893](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215212409893.png)}}
  + 需解决问题图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050803.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050841.png)}}

## 数据库建模

### 数据模型与概念模型
+ 数据模型: {{c1:: 表达计算机世界的模型称数据模型； }}
+ 概念模型: {{c1:: 表达信息世界的模型称概念数据模型，简称概念模型，信息世界是对现实世界的理解与抽象 }}
+ 图示：{{c1::![image-20210215214823019](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215214823019.png)}}

### 怎样抽象—理解-区分-命名-表达?
+ 现实世界需要**理解**：{{c1::现实中的卡片、单据、表格、报表… …}}
+ 理解的标志是**区分**：{{c1::表与表的区分，表内数据项的区分，数据项之间关系的区分，表之间关系的区分？}}
+ 区分的标志是**命名**：{{c1::命名表、命名数据项、命名表之间的联系}}
+ 抽象的最终结果是正确的**表达**：{{c1::用其他人能理解的表达方法来表达(E-R图/Crow's Foot/IDEF1X)}}


### E-R模型
+ E-R模型：{{c1::**Entity-Relationship Model**。1976年，P.P.S.Chen提出E-R模型，用E-R图来描述概念模型。}}
+ E-R模型的基本观点：{{c1::世界是由一组称作**实体**的基本对象和这些对象之间的**联系**构成的}}
+ E-R模型4个基本概念：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210215221521.png)}}

### E-R模型：实体/属性/关键字
+ 实体：{{c1::客观存在并可相互区分的事物}}
+ 属性：{{c1::属性，实体所具有的某一方面特性}}
+ 实体与实例的差别：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210215222444.png)}}
+ 属性的分类
  + **单一属性**与**复合属性**：{{c1::复合属性示例： 家庭住址：省份, 详细住址}}
  + **单值属性**和**多值属性**：{{c1::多值属性示例：电话号码，一个人可能有多个电话号码}}
  + **可空值属性**和**非空值属性**：{{c1::每个实例的该属性值可以是或不能是空值}}
  + **导出属性**：{{c1::由其他属性计算而得，例如由“出生年份” 可以得出“年龄}}
+ **关键字/码**：{{c1::实体中能够用其值唯一区分开每一实例的属性或属性组合}}

### E-R模型：联系
+ **联系**：{{c1:: 指一个实体的实例和其他实体实例之间所可能发生的联系，联系是要表达的要素。无联系的实体是没有意义的}}
+ **度**或**元**：{{c1:: 参与发生联系的实体的数目，称为联系的度或元。}}
  + **一元联系**：{{c1:: ![image-20210217050615124](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210217050615124.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050642.png)}}
  + **二元联系**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210215230405.png)}}
  + **多元联系**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050429.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050455.png)}}
+ **角色(作用)**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050327.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050348.png)}}
+ 联系的**基数**：{{c1:: Cardinalities，实体实例之间的联系的数量，即一个实体的实例通过一个联系能与另一实体中相关联的实例的数目}}
+ 常见的映射基数如：{{c1:: 一对一的（1:1），一对多的（1:m），多对多的（m:n）几种情况}}
+ **完全参与联系**：{{c1:: 即该端实例至少有一个参与到联系中,最小基数为1(1..m)}}
+ **部分参与联系**：{{c1:: 即该端实例可以不参与联系，最小基数为0(0..m)}}
+ 示例：完全参与联系和部分参与联系：{{c1::![image-20210217050137288](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210217050137288.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050201.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210215232143.png)}}

### E-R模型:Chen方法的基本图元及其含义
+ 图示结构（根据以下图元填充）：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216000500.png)}}
+ **实体**：{{c1::矩形框}}
+ **属性**：{{c1::椭圆}}
  + **多值属性**：{{c1::双线椭圆}}
  + **导出属性**：{{c1::虚线椭圆}}
+ **关键字/码**：{{c1::下划线}}
+ **连接实体和属性**：{{c1::直线}}
+ **联系**：{{c1::菱形框}}
+ **连接实体与联系**：{{c1::直线}}
+ **连接联系和属性**：{{c1::直线}}
+ **复合关键字**：{{c1::标有相同数字}}
+ **多组关键字**：{{c1::标有不同数字}}
+ 注意：{{c1::每个实体至少要给出关键字实体的关键字要作为联系的属性}}

### E-R模型:Chen方法中不同“联系”的区分方法
+ 图示结构（根据以下图元填充）：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216000844.png)}}
+ **1:1联系**：{{c1::箭头直线，由联系指向实体}}
+ **1:m联系**：{{c1::指向1端为箭头直线，指向多端为无箭头直线}}
+ **m:n联系**：{{c1::无箭头直线}}
+ **完全参与联系**：{{c1::双直线}}
+ **部分参与联系**：{{c1::单直线}}
+ `1:1, 1:m, m:n`的联系也可以如下区分:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216001008.png)}}
    + 注意：{{c1::最小基数0的为部分参与联系}}

### 示例：仓储管理的E-R Diagram
+ 需求理解：
  + 管理零件
  + 管理零件的来源—哪些零件来自于哪些供应商
  + 管理零件的去向—哪个零件供应给哪一个项目使用
  + 管理多个仓库---哪个零件存在哪个仓库中
  + 管理职工---哪个职工管理哪个仓库
+ 运用E-R模型理解需求并建模的步骤:
  1. {{c1::理解需求，寻找实体}}
  2. {{c1::用属性刻画每一个实体}}
  3. {{c1::确定每一个实体的关键字/码}}
  4. {{c1::数据建模的重点是分析实体之间的联系}}
  5. {{c1::检查是否覆盖了需求}}
+ 结果示例(Chen方法)：{{c1::![20210216002056](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216002056.png)}}
+ 结果示例(Crow’s foot方法)：{{c1::![20210216010623](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216010623.png)}}

### E-R模型:Crow’s foot方法的基本图元及其含义
+ 图示结构（根据以下图元填充）：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216010326.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216010427.png)}}
+ **实体**：{{c1::矩形框，实体的名称写在横线上面}}
+ **属性**：{{c1::实体框横线的下面}}
+ **关键字**：{{c1::属性下加下划线}}
+ **联系**：{{c1::菱形框表示，也可以将菱形框省略而直接以联系名来替代}}

### IDEF1x对E-R图概念的细分
+ 实体(Entity)
  + {{c1::独立标识符实体/独立实体Identifier-IndependentEntity)--强实体}}
  + {{c1::从属标识符实体/从属实体Identifier-dependentEntity)--弱实体}}
+ 联系(Relationship)
  + {{c1::可标定连接联系(IdentifyingConnectionRelationship)}}
  + {{c1::非标定连接联系(Non-IdentifyingConnectionRelationship)}}
  + {{c1::分类联系(CategorizationRelationship)}}
  + {{c1::非确定联系(Non-SpecificRelationship)}}
+ 属性/关键字(Attribute/Key)
  + 主关键字：{{c1::主关键字/主码(PrimaryKeys)--主属性}}
  + 次关键字：{{c1::次关键字/候选码(AlternateKeys)}}
  + 外来关键字：{{c1::是其他实体的关键字}}

### IDEF1x-两种实体的区分
+ 实体(Entity):{{c1::}} 一个“实体”表示一个现实和抽象事物的集合，这些事物必须具有相同的属性和特征。这个集合的一个元素就是该实体的一个实例}}
+ 实体被区分为:{{c1::**独立实体**和**从属实体**；在扩展E-R图中，独立实体又称**强实体**，从属实体又称**弱实体**。}}
+ **独立实体**：{{c1::一个实体的实例都被唯一的标识而不决定于它与其他实体的联系}}
  + IDEF1x独立实体描述方法图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216154857.png)}}
+ **从属实体**：{{c1::一个实体的实例的唯一标识需要依赖于该实体与其他实体的联系}}
  + IDEF1X从属实体描述方法图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216155424.png)}}
+ **独立实体/从属实体**的图示规则：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216155852.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216155906.png)}}。

### IDEF1x的标定联系与非标定联系
+ **标定联系**：{{c1::子实体的实例都是由它与父实体的联系而确定。**父实体的主关键字是子实体主关键字的一部分，一对一联系**![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217032711.png)}}
+ **非标定联系**：{{c1::子实体的实例能够被唯一标识而无需依赖与其实体的联系。**父实体的主关键字不是子实体的主关键字。一对多联系**![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217032844.png)}}
+ 关于标定联系和非标定联系的规则：工程化的要求
+ **虚直线**：{{c1::标定联系用实直线表示，非标定联系用虚直线表示}}
+ **直线**：{{c1::在子实体一侧有圆圈，联系名标注在直线旁}}

### IDEF1x的非确定联系
+ **非确定联系**：{{c1::即实体之间的**多对多**的联系，**非确定联系必须分解为若干个一对多的联系来表达**，非确定联系通过引入相交实体(Intersection Entity)或者称相关实体(Associative Entity)来分解为若干个一对多的联系来表达。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217040432.png)}}

### IDEF1x的分类联系

+ **分类联系**：{{c1::一个实体实例是由一个**一般实体实例**及多个**分类实体实例**构成的。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217044216.png)}}
+ **属性继承**：{{c1::高层实体的属性被低层实体自动继承，低层实体特有的性质仅适用于某个特定的低层实例}}
+ **完全分类联系**与**非完全分类联系**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050025.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050040.png)}}
  + 注意：{{c1::分类实体必须有特有的属性，否则分类没有意义}}
+ E-R图中的分类联系示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217044421.png)}}
+ Crow's foot表达分类联系的符号：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217044444.png)}}