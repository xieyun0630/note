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

+ **External Level**: {{c1:: **User Level** 某一用户能够看到与处理的数据,   全局数据中的某一部分}}
+ **Conceptual Level**: {{c1:: **Logic level** 从全局角度理解/管理的数据, 含相应的关联约束}}
+ **Internal Level**: {{c1:: **Physical level** 存储在介质上的数据，含存储路径、存储方式 、索引方式等}}
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

## 表的严格定义 [ ](DatabaseSystem_20210217061915381)

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

### 关系上的重要概念 [ ](DatabaseSystem_20210217061915383)

+ **Candidate Key**: {{c1::候选码(Candidate Key),关系中的一个**属性组**，其值能**唯一标识**一个元组，若从该属性组中去掉任何一个属性，它就不具有这一性质了，这样的属性组称作候选码。}}
+ **Primary Key**: {{c1::当有多个候选码时，可以选定一个作为主码.DBMS以主码为主要线索管理关系中的各个元组。}}
+ **主属性与非主属性**：{{c1::包含在任何一个候选码中的属性被称作主属性，而其他属性被称作非主属性}}
  + 最简单的，{{c1::候选码只包含一个属性}}
  + 最极端的，{{c1::所有属性构成这个关系的候选码，称为全码(All-Key)。}}
+ **Foreign Key**：{{c1::外码(Foreign Key)/外键，关系R中的一个属性组，它不是R的候选码，但它与另一个关系S的候选码相对应，则称这个属性组为R的外码或外键。}}
+ 关系与表概念对应图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210211041941.png)}}

### 关系模型中的完整性:关系完整性 [ ](DatabaseSystem_20210217061915385)

+ **实体完整性**: {{c1::关系的主码中的属性值不能为空值；若主码为空，则出现不可标识的个体，这是不容许的；}}
+ **参照完整性**: {{c1::如果关系R1的外码**Fk**与关系**R2**的主码**Pk**相对应，则**R1**中的每一个元组的**Fk**值或者等于**R2**中某个元组的**Pk值**，**或者**为**空值**}}
  + 意义：{{c1::如果关系**R1**的某个元组**t1**参照了关系**R2**的某个元组**t2**，则**t2**必须存在}}
+ **用户自定义完整性**: {{c1::用户针对具体的应用环境定义的完整性约束条件}}
+ **DBMS对关系完整性的支持**: {{c1::实体完整性和参照完整性由DBMS系统**自动支持**,它使用户可以自行定义有关的完整性约束条件,当有更新操作发生时，DBMS将自动按照完整性约束条件检验更新操作的正确性，即是否符合用户自定义的完整性}}

## 关系代数 [ ](DatabaseSystem_20210217061915389)

### 关系代数操作：集合操作和纯关系操作 [ ](DatabaseSystem_20210217061915391)

+ 问：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214022227.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214022148.png)}}

### 关系代数概念：并相容性 [ ](DatabaseSystem_20210217061915393)

+ 定义：关系R与关系S存在相容性，当且仅当：
  1. {{c1::关系R和关系S的**属性数目**必须相同；}}
  2. {{c1::对于任意i，关系R的第i个属性的域必须和关系S的第i个属性的**域相同**}}
+ 例：
  + 假设：`R(A1, A2, … , An)` , `S(B1, B2, … ,Bm)`R和S满足并相容性：
  + 那么：{{c1:: `n = m` 并且 `Domain(Ai) = Domain(Bi)` }}

### 关系代数基本操作：“并”操作 [ ](DatabaseSystem_20210217061915396)

+ 定义：{{c1::假设关系R和关系S是并相容的，则关系R与关系S的并运算结果也是一个关系，记作：R ∪S, 它由或者出现在关系R中，或者出现在S中的元组构成。在合并时去掉重复的元组。}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214023344.png)}}
+ 对应汉语：{{c1::汉语中的“或者…或者…”通常意义是并运算的要求。}}

### 关系代数基本操作：“差”操作 [ ](DatabaseSystem_20210217061915398)

+ 定义：{{c1::假设关系R和关系S是并相容的，则关系R与关系S的差运算结果也是一个关系，记作：R-S,它由**出现在**关系R中**但不出现在**关系S中的元组构成。}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214024051.png)}}
+ 对应汉语：{{c1::是…但不含…}}

### 关系代数基本操作：“笛卡尔积”操作 [ ](DatabaseSystem_20210217061915400)

+ 定义：{{c1::关系`R(<a1,a2,…,an>)`与关系`S(<b1,b2,…,bm>)`的广义笛卡尔积(简称广义积,或积或笛卡尔积)运算结果也是一个关系，记作：`RxS`,它由关系R中的元组与关系S的元组进行所有可能的拼接(或串接)构成。}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214024254.png)}}
+ 关系R的元组数目是3，度数是3; 关系S的元组数目是4, 度数是3;
  + 则RxS的元组：{{c1::数目是12, 度数是6 ?}}

### 关系代数基本操作：“选择”操作 [ ](DatabaseSystem_20210217061915403)

+ 定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214024950.png)}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214025002.png)}}
+ 运算符的优先次序:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214025414.png)}}

### 关系代数基本操作：“投影”操作 [ ](DatabaseSystem_20210217061915405)

+ 定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214034546.png)}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214034703.png)}}

### 关系代数拓展操作：“交”操作 [ ](DatabaseSystem_20210217061915408)

+ 定义：{{c1::假设关系R和关系S是并相容的，则关系R与关系S的交运算结果也是一个关系，记作：**R∩S**, 它由**同时出现在**关系R和关系S中的元组构成。}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214035424.png)}}
+ 交运算可以通过差运算来实现：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214035449.png)}}
+ 对应汉语例：{{c1::“既…又…”，“…, 并且…”}}

### 关系代数拓展操作：“theta-连接”操作 [ ](DatabaseSystem_20210217061915411)

+ 定义:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214040002.png)}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214040013.png)}}
+ **等值连接**数学描述:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214040539.png)}}
+ DBMS对**theta-连接**操作的处理：{{c1::当引入连接操作后，DBMS可直接进行连接操作，而不必先形成笛卡尔积。}}

### 关系代数拓展操作：“自然连接”操作 [ ](DatabaseSystem_20210217061915414)

+ 定义:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214040636.png)}}
+ 数学描述:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214040928.png)}}
+ 特点：
  1. **相同属性组**：{{c1::要求关系R和关系S必须有相同的属性组B(如R,S共有一个属性B1,则B是B1 , 如R, S共有一组属性`B1, B2, …, Bn`，则B是这些共有的所有属性)}}
  2. **值相等**:{{c1::R, S属性相同，值必须相等才能连接，即`R.B1 = S.B1 and R.B2 = S.B2 … and R.Bn = S.Bn`才能连接}}
  3. **去掉重复列**:{{c1::要在结果中去掉重复的属性列}}

### 关系代数的基本书写思路： [ ](DatabaseSystem_20210217061915418)

1. {{c1::选出将用到的关系/表}}
2. {{c1::做“积”运算(可用连接运算替换)}}
3. {{c1::做选择运算保留所需的行/元组}}
4. {{c1::做投影运算保留所需的列/属性}}

### 关系代数练习 [ ](DatabaseSystem_20210217061915420)

+ 问：![image-20210214063757529](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210214063757529.png)![image-20210214063839810](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210214063839810.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214064715.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214064054.png)}}

### 关系代数扩展操作:除(Division） [ ](DatabaseSystem_20210217061915423)

+ 常用于求解:{{c1::**“查询… 全部的/所有的…”**问题}}
+ 前提条件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214065239.png)}}
+ 数学描述：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214070714.png)}}
+ 定义
  + R除S结果的属性应有哪些：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214065804.png)}}
  + R除S结果的元组怎样形成：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214070514.png)}}

### 关系代数扩展操作:除(Division）练习 [ ](DatabaseSystem_20210217061915425)

+ 表结构：![image-20210214071621781](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210214071621781.png)
+ 题：![image-20210214071751337](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210214071751337.png)
+ 答：{{c1::![image-20210214071735115](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210214071735115.png)}}

### 关系代数扩展操作:“外连接”操作 [ ](DatabaseSystem_20210217061915428)

+  外连接的形式：{{c1::左外连接、右外连接、全外连接}}
   + 左外连接 = {{c1::自然连接(或theta连接) + 左侧表中**失配的元组**}}
   + 右外连接 = {{c1::自然连接(或theta连接) + 右侧表中**失配的元组**}}
   + 全外连接 = {{c1::自然连接(或theta连接) + 两侧表中**失配的元组**}}
+  左外连接(Left Outer Join)记为：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214072559.png)}}
+  右外连接(Right Outer Join)记为：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214072611.png)}}
+  全外连接(Full Outer Join)记为：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214072620.png)}}

## 关系元组演算 [ ](DatabaseSystem_20210217061915431)

+ 关系元组演算公式的基本形式：{{c1::`{ t | P(t) }`}}
+ 详：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214075752.png)}}

### 关系元组演算例子：全都学过 [ ](DatabaseSystem_20210217061915434)

+ 题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074234.png)
+ 答：
  + 关系代数：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074322.png)}}
  + 关系元组演算：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074330.png)}}


### 关系元组演算例子：全没学过 [ ](DatabaseSystem_20210217061915436)

+ 题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074451.png)
+ 答：
  + 关系代数：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074459.png)}}
  + 关系元组演算：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074509.png)}}


### 关系元组演算例子：至少有一学过 [ ](DatabaseSystem_20210217061915439)

+ 题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074612.png)
+ 答：
  + 关系代数：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074626.png)}}
  + 关系元组演算：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074633.png)}}

### 关系元组演算例子：至少有一没学过 [ ](DatabaseSystem_20210217061915442)

+ 题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074854.png)
+ 答：
  + 关系代数：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074909.png)}}
  + 关系元组演算：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214074918.png)}}

### 关系代数转换为元组演算 [ ](DatabaseSystem_20210217061915445)

+ 问：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214075126.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214075530.png)}}

## 关系域演算 [ ](DatabaseSystem_20210217061915447)

### 关系域演算例子 [ ](DatabaseSystem_20210217061915451)

+ 问：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214080340.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214080437.png)}}

## 关系运算总结 [ ](DatabaseSystem_20210217061915453)

### 关系运算的安全性 [ ](DatabaseSystem_20210217061915456)

+ 定义：{{c1::“不产生无限关系和无穷验证的运算被称为是安全的}}
+ 各运算的安全性：
  + 关系代数：{{c1::关系代数是一种集合运算，是安全的}}
  + 关系演算：{{c1::不一定是安全的![image-20210214081134592](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210214081134592.png)}}

### 关系运算总结 [ ](DatabaseSystem_20210217061915459)

+ 关系运算有三种：{{c1::关系代数、关系元组演算和关系域演算}}
+ 三种关系运算都是抽象的数学运算，体现了三种不同的思维
  + 关系代数：{{c1::以集合为对象的操作思维，由集合到集合的变换}}
  + 元组演算：{{c1::以元组为对象的操作思维，取出关系的每一个元组进行验证，有一个元组变量则可能需要一个循环，多个元组变量则需要多个循环}}
  + 域演算：{{c1::以域变量为对象的操作思维，取出域的每一个变量进行验证看其是否满足条件}}

+ **三种运算之间是等价的**：{{c1::关系代数 与 安全的元组演算表达式 与 安的域演算表达式 是等价的。即一种形式的表达式可以被等价地转换为另一种形式}}
+ **三种关系运算都可说是非过程性的**：{{c1::相比之下：域演算的非过程性最，元组演算次之，关系代数最差}}
+ **三种关系运算虽是抽象的，但却是衡量数据库语言完备性的基础**：{{c1::一个数据库语言如果能够等价地实现这三种关系运算的操作，则说该语言是完备的。目前多数数据库语言都能够实现这三种运算的操作，在此基础上还增加了许多其他的操作，如赋值操作、聚集操作等}}

## SQL语言 [ ](DatabaseSystem_20210217061915462)

### SQL语言的功能概述 [ ](DatabaseSystem_20210217061915465)

+ DDL语句引导词：{{c1::Create(建立),Alter(修改),Drop(撤消)}}
+ DML语句引导词：{{c1::Insert ,Delete, Update, Select}}
+ DCL语句引导词：{{c1::Grant,Revoke}}
+ 交互式SQL->嵌入式SQL->动态SQL等

### SQL语言:结果唯一性问题 [ ](DatabaseSystem_20210217061915467)

+ 问题引出：关系模型不允许出现重复元组。但现实DBMS，却允许出现重复元组，但也允许无重复元组。
+ 解决：{{c1::在**Table**中要求无重复元组是通过定义**Primary key**或**Unique**来保证的;而在检索结果中要求无重复元组, 是通过**DISTINCT**保留字的使用来实现的。}}

### `not in` `some` `all` 联系与区别 [ ](DatabaseSystem_20210217061915469)

+ 问：![image-20210217051138257](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210217051138257.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217051201.png)
+ 答：{{c1::注意`<>some`的语义,some等价于any,any由于语义问题被弃用.}}

### EXISTS 子查询 [ ](DatabaseSystem_20210217061915471)

+ 语义：{{c1::子查询结果中有无元组存在}}
+ 示例：检索选修了赵三老师主讲课程的所有同学的姓名:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210214090753.png)}}

## SQL语言实现关系代数操作 [ ](DatabaseSystem_20210217061915473)

### SQL语言:并-交-差的处理 [ ](DatabaseSystem_20210217061915477)

+ **SQL语言**：{{c1::并运算 UNION, 交运算INTERSECT, 差运算EXCEPT}}
+ **基本语法形式**：{{c1::子查询 `{ Union [ALL] | Intersect [ALL] | Except [ALL] 子查询 }` }}
+ **通常情况下自动删除重复元组**：{{c1::不带ALL。若要保留重复的元组，则要带ALL。}}
+ 注意：{{c1::有些DBMS不支持INTERSECT,EXCEPT}}

### SQL语言:现行DBMS的空值处理小结 [ ](DatabaseSystem_20210217061915479)

+  `where`中: {{c1:: 除is[not]null之外，空值不满足任何查找条件}}
+  如果null参与算术运算，{{c1::则该算术表达式的值为null}}
+  如果null参与比较运算，{{c1::则结果可视为false。在SQL-92中可看成unknown}}
+  如果null参与聚集运算，{{c1::则除count(*)之外其它聚集函数都忽略null}}

### SQL视图更新 [ ](DatabaseSystem_20210217061915481)

+ 原则：{{c1::视图更新要保证原有表的实体完整性。}}
+ 视图不更新的几种情况：
  1. 聚集函数：{{c1::如果视图的select目标列包含聚集函数，则不能更新}}
  2. unique或distinct：{{c1::如果视图的select子句使用了unique或distinct，则不能更新}}
  3. groupby：{{c1::如果视图中包括了groupby子句，则不能更新}}
  4. 算术表达式：{{c1::如果视图中包括经算术表达式计算出来的列，则不能更新}}
  5. 主键：{{c1::如果视图是由单个表的列构成，但并没有包括主键，则不能更新}}

## 数据库完整性和安全性 [ ](DatabaseSystem_20210217061915483)

### 数据库完整性 [ ](DatabaseSystem_20210217061915486)

+ 为什么会引发数据库完整性的问题: {{c1::不正当的数据库操作，如输入错误、操作失误、程序处理失误等}}
+ DBMS怎样自动保证完整性呢？
  + {{c1::DBMS允许用户定义一些完整性约束规则(用SQL-DDL来定义)}}
  + {{c1::当有DB更新操作时，DBMS自动按照完整性约束条件进行检查，以确保更新操作符合语义完整性}}
+ 完整性分类：{{c1::![image-20210215165354352](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215165354352.png)}}
+ 完整性约束条件(或称完整性约束规则)的一般形式:{{c1::![image-20210215163705366](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215163705366.png)}}

### SQL语言实现约束的方法-断言 [ ](DatabaseSystem_20210217061915489)

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

### 触发器Trigger [ ](DatabaseSystem_20210217061915491)

+ 作用：Create Table中的表约束和列约束基本上都是静态的约束，也基本上都是对单一列或单一元组的约束(尽管有参照完整性)，为实现动态约束以及多个元组之间的完整性约束，就需要触发器技术Trigger
+ 示例：设计一个触发器当进行Teacher表更新元组时, 使其工资只能升不能降：{{c1::![image-20210215165016404](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215165016404.png)}}

### 数据库安全性 [ ](DatabaseSystem_20210217061915494)

+ 作用：{{c1::数据库安全性是指DBMS应该保证的数据库的一种特性(机制或手段)：免受非法、非授权用户的使用、泄漏、更改或破坏}}
+ 数据的安全级别: {{c1::绝密(Top Secret), 机密(Secret),可信(Confidential)和无分类(Unclassified) }}
+ 数据库系统DBS的安全级别：{{c1::物理控制、网络控制、操作系统控制、DBMS控制}}

### 自主安全性 [ ](DatabaseSystem_20210217061915497)

+ 数据库自主安全性访问规则：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217051032.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217051049.png)}}
+ 自主安全性的实现方式:
  + 存储矩阵:{{c1::![image-20210215170039634](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215170039634.png)}}
  + 视图:{{c1::![image-20210215170046269](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215170046269.png)}}

### 自主安全性的授权过程及其问题 [ ](DatabaseSystem_20210217061915500)

+ 授权过程:{{c1::![image-20210215210903945](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215210903945.png)}}
+ 传播范围包括两个方面：
+ 水平传播数量: {{c1::是授权者的再授权用户数目(树的广度)}}
+ 垂直传播数量: {{c1::是授权者传播给被授权者，再被传播给另一个被授权者, …传播的深度(树的深度)}}

### 嵌入式SQL语言 [ ](DatabaseSystem_20210217061915502)

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

## 数据库建模E-R模型 [ ](DatabaseSystem_20210217061915504)

### 数据模型与概念模型 [ ](DatabaseSystem_20210217061915507)

+ 数据模型: {{c1:: 表达计算机世界的模型称数据模型； }}
+ 概念模型: {{c1:: 表达信息世界的模型称概念数据模型，简称概念模型，信息世界是对现实世界的理解与抽象 }}
+ 现实世界、概念模型、数据模型之间关系图示：{{c1::![image-20210215214823019](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210215214823019.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509132706.png)}}

### 怎样抽象—理解-区分-命名-表达? [ ](DatabaseSystem_20210217061915510)

+ 现实世界需要**理解**：{{c1::现实中的卡片、单据、表格、报表… …}}
+ 理解的标志是**区分**：{{c1::表与表的区分，表内数据项的区分，数据项之间关系的区分，表之间关系的区分？}}
+ 区分的标志是**命名**：{{c1::命名表、命名数据项、命名表之间的联系}}
+ 抽象的最终结果是正确的**表达**：{{c1::用其他人能理解的表达方法来表达(E-R图/Crow's Foot/IDEF1X)}}


### E-R模型：基本概念 [ ](DatabaseSystem_20210217061915513)

+ E-R模型：{{c1::**Entity-Relationship Model**。1976年，P.P.S.Chen提出E-R模型，用E-R图来描述概念模型。}}
+ E-R模型的基本观点：{{c1::世界是由一组称作**实体**的基本对象和这些对象之间的**联系**构成的}}
+ E-R模型4个基本概念：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210215221521.png)}}

### E-R模型：实体/属性/关键字 [ ](DatabaseSystem_20210217061915516)

+ 实体：{{c1::客观存在并可相互区分的事物}}
+ 属性：{{c1::属性，实体所具有的某一方面特性}}
+ **实体**与**实例**的差别：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210215222444.png)}}
+ 使用属性来刻画实体的两种方式：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509133919.png)}}
+ 属性的分类
  + **单一属性**与**复合属性**：{{c1::复合属性示例： 家庭住址：省份, 详细住址，**复合属性一定要转化为单一属性(关系的第1范式)**}}
  + **单值属性**和**多值属性**：{{c1::多值属性示例：电话号码，一个人可能有多个电话号码，**多值属性一定要转化为单值属性(关系的第1范式)**}}
  + **可空值属性**和**非空值属性**：{{c1::每个实例的该属性值可以是或不能是空值}}
  + **导出属性**：{{c1::由其他属性计算而得，例如由“出生年份” 可以得出“年龄}}
+ **关键字/码**：{{c1::实体中能够用其值唯一区分开每一实例的属性或属性组合}}

### E-R模型：联系 [ ](DatabaseSystem_20210217061915519)

+ **联系**：{{c1:: 指一个实体的实例和其他实体实例之间所可能发生的联系，联系是要表达的要素。无联系的实体是没有意义的}}
+ 联系的**度**或**元**：{{c1:: 参与发生联系的实体的数目，称为联系的度或元。}}
  + **一元联系**：{{c1:: ![image-20210217050615124](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210217050615124.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050642.png)}}
  + **二元联系**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210215230405.png)}}
  + **多元联系**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050429.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050455.png)}}
+ **角色(作用)**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050327.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210217050348.png)}}
+ 联系的**基数**：{{c1:: Cardinalities，实体实例之间的联系的数量，即一个实体的实例通过一个联系能与另一实体中相关联的实例的数目}}
+ 常见的映射基数如：{{c1:: 一对一的（1:1），一对多的（1:m），多对多的（m:n）几种情况}}
+ **完全参与联系**：{{c1:: 即该端实例至少有一个参与到联系中,最小基数为1(1..m)}}
+ **部分参与联系**：{{c1:: 即该端实例可以不参与联系，最小基数为0(0..m)}}

## E-R模型表达方法：Chen方法 [ ](DatabaseSystem_20210509093451657)

### E-R模型:Chen方法的基本图元 [ ](DatabaseSystem_20210217061915522)

+ 图示结构（根据以下图元填充）：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216000500.png)}}
+ 各图元解释：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509140131.png)}}

### Chen方法中联系的表达（3大联系，2种参与） [ ](DatabaseSystem_20210217061915525)

+ 图示结构（根据以下图元填充）：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216000844.png)}}
+ 图示结构（基数表示法）:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210216001008.png)}}
+ **1:1联系**：{{c1::箭头直线，由联系指向实体}}
+ **1:m联系**：{{c1::指向1端为箭头直线，指向多端为无箭头直线}}
+ **m:n联系**：{{c1::无箭头直线}}
+ **完全参与联系**：{{c1::双直线}}
+ **部分参与联系**：{{c1::单直线}}
  + 注意：{{c1::最小基数0的为部分参与联系}}

### Chen方法：图书管理的E-R Diagram [ ](DatabaseSystem_20210509093451660)

+ 注意：图书、读者、书架，三大实体联系的表达
+ 联系也需要通过命名来区分。
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509141124.png)}}

### Chen方法示例：仓储管理的E-R Diagram [ ](DatabaseSystem_20210509093451663)

+ 需求描述：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509144113.png)
+ 建模结果：{{c1::  ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509144240.png)  }}



## E-R模型表达方法:Crow’s foot方法 [ ](DatabaseSystem_20210509093451666)

### Crow’s foot方法：表达（实体/属性/关键字） [ ](DatabaseSystem_20210509093451669)

+ 注意：与Chen方法的区别

+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509142351.png)}}

### Crow’s foot方法：表达联系 [ ](DatabaseSystem_20210509093451672)

+ 联系：菱形框表示，也可以将菱形框省略而直接以联系名来替代
+ 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509143057.png) }}
+ 注意与chen方法的区别：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509143123.png) }}

### Crow’s foot方法：表达联系的基数 [ ](DatabaseSystem_20210509093451675)

+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509143455.png)}}
+ 与chen方法的区别：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509143515.png)}}
+ 使用示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509143829.png)}}

### Crow’s foot方法示例：仓储管理的E-R Diagram [ ](DatabaseSystem_20210509093451678)

+ 需求描述：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509144113.png)
+ 建模结果：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509144025.png) }}

## E-R模型表达方法:IDEF1x方法 [ ](DatabaseSystem_20210509093451681)

### IDEF1x方法：表达实体（两种实体的区分） [ ](DatabaseSystem_20210509093451684)

+ **独立实体**概念：{{c1::一个实体的实例都被唯一的标识而**不决定于**它与其他实体的**联系**}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509150838.png)}}
+ **从属实体**概念：{{c1::一个实体的实例的唯一标识需要依赖于该实体与其他实体的联系，**从属实体的关键字属性包含继承自其它实体的属性**}}
  + 图示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509150954.png)}}
+ **独立实体/从属实体的图示规则**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509151802.png)}}

### IDEF1x方法：对联系的分类 [ ](DatabaseSystem_20210509093451687)

+ 连接联系：{{c1::又称**父子联系**或**依存联系**}}
  + {{c1::标定联系}}
  + {{c1::非标定联系}}
+ {{c1::分类联系}}
+ {{c1::非确定联系}}

### IDEF1x方法：表达联系（标定联系\非标定联系） [ ](DatabaseSystem_20210509093451689)

+ 注意：具体的E-R图画法
+ 标定联系(图)：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509152519.png)}}
+ 非标定联系(图)：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509153159.png)}}
+ 注意E-R图中具体要求：
  + **实直线**:{{c1::标定联系用实直线表示}}
  + **虚直线**:{{c1::非标定联系用虚直线表示}}
  + **子实体**:{{c1::在子实体一侧有圆圈}}
  + **联系名**:{{c1::联系名标注在直线旁}}

### IDEF1x方法：表达联系（非确定联系） [ ](DatabaseSystem_20210509093451691)
+ **非确定联系**：{{c1::即实体之间的多对多的联系,**非确定联系必须分解为若干个一对多的联系来表达**}}
+ **怎样处理非确定联系**图示:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509175311.png) }}
+ **IDEF1x对联系的两种处理机制**图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509175529.png)}}

### IDEF1x方法：表达联系（分类联系概念） [ ](DatabaseSystem_20210509093451693)

+ 分类联系：{{c1:: 一个实体实例是由一个**一般实体**实例及多个**分类实体**实例构成的 }}
+ 注意：两种ER图的画法
+ **完全分类联系**与**；非完全分类联系**：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509182245.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509182319.png) }}


### IDEF1x方法：表达联系（分类联系） [ ](DatabaseSystem_20210509093451696)
+ IDEF1x方法的分类联系示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509181648.png)}}
+ E-R图中的分类联系示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509181903.png)}}
+ Crow's foot表达分类联系示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509181932.png)}}

## 数据库设计过程 [ ](DatabaseSystem_20210509093451698)

### 数据库设计的四个过程 [ ](DatabaseSystem_20210509093451701)
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509184753.png)}}

### 数据库设计过程：需求分析 [ ](DatabaseSystem_20210509093451703)
+ 需求分析过程：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509191016.png)}}
+ 需求分析成果物：{{c1::形成数据库设计的“源”清单和“属性”清单以及相关的详细描述,尤其是注意业务规则与属性处理规则}}
+ 源清单示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509191615.png)}}
+ “属性”清单示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509191744.png) }}
+ “属性”定义表:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509192343.png) }}

### 数据库设计过程：概念数据库设计过程 [ ](DatabaseSystem_20210509093451705)
+ 概念数据库设计过程：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509195156.png)}}

### 数据库设计过程：概念数据库设计可能的冲突 [ ](DatabaseSystem_20210509093451707)
+ 属性冲突：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509194702.png)}}
+ 结构冲突：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509194711.png)}}
+ 命名冲突：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509194722.png)}}
+ 全局E-R模式优化过程：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509194821.png)

### 数据库设计过程：概念数据库设计报告 [ ](DatabaseSystem_20210509093451709)
+ “实体”清单示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509194938.png)}}
+ “实体”定义表：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509195030.png)}}
+ “实体-联系”矩阵：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509195054.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210509195112.png)}}

### 数据库设计过程：逻辑数据库设计过程 [ ](DatabaseSystem_20210511102843609)
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511200956.png)}}

### E-R图/IDEF1X图向关系模式的转换：基本转换 [ ](DatabaseSystem_20210511102843613)
+ **基本转换规则**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511201440.png)}}
- **复合属性的转换**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511201540.png)}}
- **多值属性的转换**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511201618.png)}}

### E-R图/IDEF1X图向关系模式的转换：一对一，一对多，多对多 [ ](DatabaseSystem_20210511102843616)
+ 联系的转换
- **一对一联系**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511201730.png)}}
- **一对多联系**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511201911.png)}}
- **多对多联系**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511201959.png)}}


### E-R图/IDEF1X图向关系模式的转换：弱实体，泛化与具体化实体，多元联系 [ ](DatabaseSystem_20210511102843619)
+ **弱实体的转换**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511202507.png)}}
+ **泛化与具体化实体的转换**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511202633.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511202735.png)}}
+ **多元联系的转换**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511203118.png)}}

### 不正确设计数据库引发的问题 [ ](DatabaseSystem_20210511102843623)
+ **非受控冗余**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511203343.png)}}
+ **受控冗余**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511203357.png)}}
+ **插入异常/删除异常**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511203705.png![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511203755.png)}}
+ **如何避免?**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511203856.png)}}

### 数据库设计过程：物理数据库设计过程 [ ](DatabaseSystem_20210511102843626)
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210511204104.png)}}

## 数据依赖理论 [ ](DatabaseSystem_20210511102843629)

### 函数依赖 [ ](DatabaseSystem_20210514093242051)
+ 思考提炼1：{{c1:: 不满足（X的属性相等，Y的属性值不等）这个条件，而不是X的两个元组相等，Y就必须相等。}}
+ 思考提炼2：{{c1:: 对于每一个X值有唯一的Y值与之对应。}}
+ 函数依赖定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514182757.png)}}
+ 例题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514183556.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514183649.png)}}

### 函数依赖的特性 [ ](DatabaseSystem_20210514093242053)
+ **非平凡的函数依赖**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514183857.png)}}
+ **决定因素**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514183918.png)}}
+ **恒成立**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514184025.png)}}
+ 练习：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514184109.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514184124.png)}}

### 部分或完全函数依赖 [ ](DatabaseSystem_20210514093242056)
+ 思考提炼：去掉一个属性函数依赖不成立就是完全依赖
+ 部分函数依赖与完全函数依赖的定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514185712.png)}}
+ 练习：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514185742.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514185755.png)}}

### 传递函数依赖 [ ](DatabaseSystem_20210514093242059)
+ 传递函数依赖的定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514190838.png)}}
+ 练习：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514190915.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514190926.png)}}

### 函数依赖相关的几个重要概念 [ ](DatabaseSystem_20210514093242062)
+ 候选键定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514191411.png)}}
+ 外来键的定义：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514191435.png)}}
+ 逻辑蕴涵的定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514201739.png)}}
+ 闭包的定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514201814.png)}}

### 函数依赖的Armstrong Axioms A1 A2 A3公理 [ ](DatabaseSystem_20210514093242064)
+ 作用：{{c1:: 由一些给定的函数依赖，推导隐含的函数依赖 }}
+ **自反律** **增广律** **传递律**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514210830.png)}}
+ **合并律** **伪传递律** **分解律**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514210929.png)}}
+ 关于属性组合的函数依赖与单一属性的函数依赖有什么关系？：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514211048.png)}}

### 函数依赖:属性闭包 [ ](DatabaseSystem_20210514093242066)
+ 属性闭包作用（思考）: {{c1:: 求某个关系属性闭包，再求Y是否属于属性闭包。从而判断函数依赖 }}
+ 属性闭包定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514211142.png)}}

+ 求属性闭包问题:![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210617222329.png)

+ 答：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514211554.png) }}

### 函数依赖集的最小覆盖：覆盖、属性闭包的计算算法 [ ](DatabaseSystem_20210514093242068)

+ 问题：如何证明一个函数依赖被一个函数依赖集所蕴含
+ 覆盖的定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514211259.png)}}
+ 属性闭包证明函数依赖集之间的等价：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210617222728.png) ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514211142.png)}}
+ 函数依赖集的性质：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514212100.png)}}

### 函数依赖集的最小覆盖 [ ](DatabaseSystem_20210514093242070)

+ 作用：{{c1:: 用于模式分解 }}
+ 定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210514212803.png)}}

## 关系范式理论 [ ](DatabaseSystem_20210620101056160)

### 1FN [ ](DatabaseSystem_20210620101056163)
+ 全称：{{c1::First Normal Form}}
+ 定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210618183638.png)}}

### 2NF [ ](DatabaseSystem_20210620101056165)
+ 定义：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210619201701.png) }}
+ 作用：{{c1::第二范式消除了非主属性对候选键的部分依赖。}}

### 2NF练习 [ ](DatabaseSystem_20210620101056167)

+ 题目：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210619220651.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210619220715.png)}}

### 3NF [ ](DatabaseSystem_20210620101056170)

+ 定义:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210619221520.png) }}
+ 作用：{{c1:: 第3范式消除了非主属性对侯选键的**传递函数依赖** }}

### 关系模式分解成3NF [ ](DatabaseSystem_20210620101056172)
+ 模式分解简单例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210619223806.png) }}

### 3NF练习 [ ](DatabaseSystem_20210620101056174)

+ 题目：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210619221841.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210619221908.png)}}

### BCNF [ ](DatabaseSystem_20210620101056176)

+ 理解点:{{c1::要符合BCNF，关系的每个函数依赖必定包含候选键。}}
+ 定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210619224524.png)}}

### 关系模式分解成BCNF [ ](DatabaseSystem_20210620101056178)
+ 问：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210619224850.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210619224901.png)}}

### 4NF [ ](DatabaseSystem_20210620101056180)
+ 定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620093227.png)}}
+ 多值依赖定义：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620095443.png)}}
+ 与BCNF关系(定理):{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620093356.png)}}

## 模式分解理论 [ ](DatabaseSystem_20210620101056183)

### 模式分解存在的问题 [ ](DatabaseSystem_20210620101056185)
+ 模式分解的3条规则：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620105157.png)}}
+ 模式分解需要考虑的2个问题：
  1. {{c1::分解后的关系的连接与分解前关系的等价性}}
  2. {{c1::分解前的约束（函数依赖）在分解后是否仍然保持}}
  + 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620105545.png)}}

### 无损连接分解 [ ](DatabaseSystem_20210620101056188)
+ 定义：{{c1::无损联接分解是将一个关系模式分解成若干个关系模式后，通过自然联接和投影等运算仍能还原到原来的关系模式，则称这种分解为无损联接分解。}}
+ 无损连接性检验算法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620124906.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620124940.png)}}

### 无损连接分解检验算法的应用示例 [ ](DatabaseSystem_20210620101056191)
+ 示例：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620125028.png)
+ 解：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620125047.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620125057.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620125116.png)}}

### 分解成两个关系模式的无损连接检验算法 [ ](DatabaseSystem_20210620101056193)
+ 图示: {{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620151036.png) }}

### 保持依赖分解的检验算法应用示例 [ ](DatabaseSystem_20210620101056195)

+ 题：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620152127.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620152149.png)}}

### 数据库设计知识体系图 [ ](DatabaseSystem_20210620101056197)

+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620154234.png)}}

### 数据库设计理论要解决的根本问题 [ ](DatabaseSystem_20210620101056199)

+ 哪些属性被组织成一个关系? 
+ 是一个大关系模式呢，还是若干小关系模式? 
+ 大关系模式存在什么问题?
+ 答（图示)：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620154422.png)}}

## 数据库物理存储 [ ](DatabaseSystem_20210620101056201)

### 计算机系统的存储体系图 [ ](DatabaseSystem_20210620101056203)
+ 存储体系：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620164002.png)}}

### 操作系统对数据的组织：FAT-目录(文件夹)-磁盘块/簇 [ ](DatabaseSystem_20210620101056206)
+ 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620164255.png) }}

### 操作系统对内存-缓冲区的管理 [ ](DatabaseSystem_20210620101056208)
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620164414.png)}}

### 磁盘的结构与特性 [ ](DatabaseSystem_20210620101056211)
+ 磁盘及磁盘的容量：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620164547.png)
+ 磁盘数据读写时间：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210622134315.png)
+ 物理存取算法考虑的关键: 
  + {{c1::降低I/O次数}}
  + {{c1::降低排队等待时间}}
  + {{c1::降低寻道/旋转延迟时间：}}
    + {{c1::同一磁道连续块存储}}
    + {{c1::同一柱面不同磁道并行块存储}}
    + {{c1::多个磁盘并行块存储}}

### 数据存储与查询实现的基本框架 [ ](DatabaseSystem_20210620101056213)

+ 图示：{{c1::![image-20210620192058842](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210620192058842.png)}}

### 表/记录与磁盘块的映射 [ ](DatabaseSystem_20210620101056215)
+ 数据库-记录在磁盘上的存储：
  + **定长与变长**：{{c1::定长记录，还是变长记录(靠分隔符区分开始与结束}}
  + **跨块/非跨块**：{{c1::记录是非跨块存储，还是跨块存储(靠指针连接)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620201520.png)}}
+ 数据库-表所占磁盘块的分配方法：
  + **连续分配**: {{c1::数据块被分配到连续的磁盘块上(**会存在扩展困难问题**)}}
  + **链接分配**: {{c1::数据块中包含指向下一数据块的指针(**访问速度问题**)}}
  + **按簇分配**: {{c1::按簇分配，簇是若干连续的磁盘块，**簇之间靠指针连接;簇有时也称片段Segment或盘区extent**}}
  + **索引分配**: {{c1::索引块中存放指向实际数据块的指针![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620202210.png)}}

### 数据库的文件组织方法 [ ](DatabaseSystem_20210620101056218)
+ **文件组织**：{{c1::(File Organization)指的是数据组织成记录、块和访问结构的方式，包括把记录和块存储在磁盘上的方式，以及记录和块之间相互联系的方法}}
+ **存取方法**：{{c1::(Access Method)指的是对文件所采取的存取操作方法，一种文件组织可以采取多种存取方法进行访问}}
+ 总结：{{c1::文件组织相当与数据结构，存取方法相当于作用于数据结构的各种操作算法。}}

### 数据库文件组织方法总结 [ ](DatabaseSystem_20210620101056221)
+ 增删改时如何快速“存”,检索查询时如何快速“取”?
+ 图示:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620220654.png)}}

### 数据库的4种文件组织方法 [ ](DatabaseSystem_20210620101056224)
+ 注意各个组织方法的**特点**，**数据库重组**。
+ 无序文件组织：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620220137.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620220156.png)}}
+ 有序记录文件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620220221.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620220252.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620220320.png)}}
+ 散列文件：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620220407.png) }}
+ 聚簇文件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620220553.png)}}

## 数据库索引 [ ](DatabaseSystem_20210623112904953)

### 索引的概念 [ ](DatabaseSystem_20210623112904955)
+ 定义：{{c1::索引是定义在存储表(Table)基础之上，有助于无需检查所有记录而快速定位所需记录的一种辅助存储结构，由一系列存储在磁盘上的索引项(indexentries)组成。存在与否不改变存储表的物理存储结
构；在一个表上可以针对不同的**属性或属性组合**建立不同的索引文件}}
+ 索引项由两部分构成：
  + **索引字段**：{{c1::由Table中某些列(通常是一列)中的值串接而成。索引中通 常存储索引字段的每一个值(也有不是这样的)。索引字段类似于词典中的词条}}
  + **行指针**：{{c1::指向Table中包含索引字段值的记录在磁盘上的存储位置。行指针类似于词条在书籍、词典中出现的页码。}}
+ **索引文件** **主文件**：{{c1::存储索引项的文件为索引文件，相对应，存储表又称为主文件![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210620223042.png)}}
+ 索引文件组织方式有两种：
  + 排序索引文件(Orderedindices):{{c1::按索引字段值的某一种顺序组织存储}}
  + 散列索引文件(Hashindices):{{c1::依据索引字段值使用散列函数分配散列桶的方式存储}}
  + 与主文件组织相比：{{c1::主文件组织有堆文件、排序文件、散列文件、聚簇文件等多种方式}}

### 索引相关的概念含义的区分 [ ](DatabaseSystem_20210623112904957)
+ **码(Key)、主码(Primary Key)**: {{c1::又称为表键(Table Key),具有唯一性}}
和最小性
+ **排序码(OrderKey)**: {{c1::对主文件进行排序存储的那些属性或属性组}}
+ **索引码(IndexKey)**: {{c1::即索引字段，不一定具有唯一性}}
+ **搜索码(SearchKey)**: {{c1::在主文件中查找记录的属性或属性集}}

### SQL语言关于索引的基本知识 [ ](DatabaseSystem_20210623112904960)
+ 当定义Table后，{{c1::如果定义了主键，则系统将自动创建主索引，利用主索引对Table进行快速定位、检索与更新操作;}}
+ 自定义：{{c1::索引可以由用户创建，也可以由用户撤消}}
+ 自动维护：{{c1::当索引被创建后，无论是主索引，还是用户创建的索引，DBMS都将自动维护所有的索引，使其与Table保持一致，即：当一条记录被插入到Table中后，所有索引也自动的被更新}}
+ 当Table被删除后(droptable),{{c1::定义在该Table上的所有索引将自动被撤消}}

### 创建和维护索引的SQL语句 [ ](DatabaseSystem_20210623112904962)
+ 创建索引：
  ```sql
  #{{c1::
  CREATE [unique] INDEX indexname
      ON tablename ( colname [asc | desc], colname [asc | desc]... );
  #}}
  ```
+ 示例：在student表中创建一个基于Sname的索引
  ```sql
  #{{c1::
  create index idxSname on student(sname);
  #}}
  ```
+ 示例：在student表中创建一个基于Sname和Sclass的索引
  ```sql
  #{{c1::
  create index idxSnamcl on student(sname, sclass);
  #}}
  ```
+ 如某索引不再需要，则可通过撤消命令，撤消用户创建的索引
  ```sql
  #{{c1::
  DROP INDEX indexname;
  #}}
  ```

### 建立索引需要考虑的问题： [ ](DatabaseSystem_20210623112904965)
+ 是否建立和在哪些属性上建立索引需要考虑：
  + {{c1::访问时间}}
  + {{c1::插入时间}}
  + {{c1::删除}}
  + {{c1::时间与空间负载}}
+ 考虑索引的类型
  + {{c1::支持属性的限定值(是否符合单一值)，}}
  + 或者 {{c1::支持属性的限定范围的值(是否符合  一定范围)}}

### 稠密索引和稀疏索引的概念 [ ](DatabaseSystem_20210623112904968)
+ **稠密索引**：{{c1::对于主文件中每一个记录(形成的每一个索引字段值)，都有一个索引项和它对应，指明该记录所在位置。这样的索引称稠密索引(denseindex)}}
  + **候选键属性的稠密索引**：{{c1::先查索引，然后再依据索引读主文件。}}
  + **非候选键属性的稠密索引**：
    1. {{c1::索引字段无重复情况}}
    1. {{c1::索引字段有重复}}
    1. {{c1::指针桶处理非候选键索引的多记录}}
    + 3种情况比较：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210623201226.png)}}
  + 注意：{{c1::无论是候选键属性的稠密索引，还是非候选键属性的稠密索引：索引文件中不存在搜索码的值，就代表着主文件中没有对应搜索码的记录}}
+ **稀疏索引**：{{c1::对于主文件中部分记录(形成的索引字段值)，有索引项和它对应，这样的索引称非稠密索引(undense index)或稀疏索引(sparseindex)}}
  + 稀疏索引的使用要求：{{c1::主文件必须是按对应索引字段属性排序存储}}
  + 相比稠密索引：{{c1::空间占用更少，维护任务更轻，但速度更慢}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210623195819.png)}}

### 主索引与辅助索引 [ ](DatabaseSystem_20210623112904971)
+ 主索引:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210623205205.png)}}
+ 辅助索引:{{c1::是定义在主文件的**任一或多个**非排序字段上的辅助存储结构。**如该字段值不唯一**，则要采用一个**类似链表**的结构来保存包含该字段值的所有记录的位置![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210623210517.png)}}

### 聚簇索引和非聚簇索引 [ ](DatabaseSystem_20210623112904974)
+ **聚簇索引**: 是指索引中邻近的记录在主文件中也**是临近**存储的
  + **聚簇字段**：{{c1::如果主文件的某一排序字段不是主码，则该字段上每个记录取值便不唯一，此时该字段被称为**聚簇字段**；聚簇索引通常是定义在聚簇字段上。}}
+ **非聚簇索引**: 是指索引中邻近的记录在主文件中**不一定是邻近**存储的
+ 图示:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210623211916.png)}}

### 其他类型的索引 [ ](DatabaseSystem_20210623112904976)
+ **倒排索引**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210623213316.png)}}
+ **多级索引**：{{c1::当索引项比较多时，可以对索引再建立索引，依此类推，形成多级索引。如B树/B+树索引，以树型数据结构来组织索引项等}}
+ **多属性索引**：{{c1::索引字段由Table的多个属性值组合在一起形成的索引}}
+ **散列索引**：{{c1::使用散列技术组织的索引}}
    + **静态散列索引**：{{c1::桶的数目M是固定值}}
    + **动态散列索引**：{{c1::桶的数目随键值增多，动态增加}}
      + **可扩展散列索引**：{{c1::每次桶数量翻倍}}
      + **线性散列索引**：{{c1::桶数量按照条件保持线性增长}}
+ **网格索引(Gridfile)**：{{c1::使用多索引字段进行交叉联合定位与检索![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210623213601.png)}}

## 查询实现算法 [ ](DatabaseSystem_20210624110429808)

### 数据库查询实现算法概述 [ ](DatabaseSystem_20210623112904978)

+ 实现数据库查询的基本思想：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210623221736.png)}}
+ **逻辑查询优化**与**物理查询优化**关系:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210623222442.png)}}

### 数据库的三大类操作：查询实现算法总览 [ ](DatabaseSystem_20210623112904981)
+ 一次单一元组的一元操作：{{c1:: 选择，投影}} }}
+ 整个关系的一元操作：{{c1:: 去重，分组，排序 }}
+ 整个关系的二元操作：{{c1::并，交，差，积，连接}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624191102.png)}}

### 连接操作的实现算法：逻辑实现算法 [ ](DatabaseSystem_20210624110429810)
+ 连接操作的逻辑实现算法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624205258.png)}}
+ 物理算法需要考虑:
  + 问：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624205522.png)
  + 关系R X S所占磁盘块数：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624210220.png)}}
  + 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624205537.png)}}

### 连接操作的物理实现算法 [ ](DatabaseSystem_20210624110429812)
+ 基本实现算法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624210353.png)}}
+ 全主存实现算法:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624210446.png)}}
+ 半主存实现算法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624210523.png)}}
+ 大关系实现算法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624210615.png)}}

### 连接操作的各物理实现算法特点与时间复杂度 [ ](DatabaseSystem_20210624110429815)
+ 基本实现算法的**特点**与**时间复杂度**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624211414.png)}}
+ 全主存实现算法的**特点**与**时间复杂度**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624211425.png)}}
+ 半主存实现算法的**特点**与**时间复杂度**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624211434.png)}}
+ 大关系实现算法的**特点**与**时间复杂度**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624211447.png)}}

### 迭代器算法的提出 [ ](DatabaseSystem_20210624110429817)
+ **物化计算策略**与**流水线计算策略**区别:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624215950.png)}}

### 迭代器构造查询实现算法：迭代器实现`Union(R,S)` [ ](DatabaseSystem_20210624110429819)
+ 迭代器实现`Union(R,S)`  **并操作**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624220320.png)}}

### 迭代器构造查询实现算法：迭代器实现`SELECTION(R)` [ ](DatabaseSystem_20210624110429821)
+ 迭代器实现`SELECTION(R)`  **选择操作**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624222617.png)}}

### 迭代器构造查询实现算法：迭代器实现`PROJECTION(SELECTION(R))` [ ](DatabaseSystem_20210624110429823)
+ 迭代器实现`PROJECTION(SELECTION(R))` **选择与投影操作**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624222932.png)}}
+ 
### 迭代器构造查询实现算法：迭代器实现`Join(R,S)`  [ ](DatabaseSystem_20210624110429825)
+ 迭代器实现`Join(R,S)` **连接操作**：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210624223404.png)}}

### 关系/表数据的读取---完整地读取一个关系 [ ](DatabaseSystem_20210625113159439)
+ 注意：各个算法的基于I/O的时间复杂度
+ 聚簇关系—关系的元组集中存放(一个块中仅是一个关系中的元组):  
  + `TableScan(R)` ---表空间扫描算法 ：{{c1::扫描结果未排序:`B(R)`}}
  + `SortTableScan(R)` ：{{c1::扫描结果排序:`3B(R)`}}
  + `IndexScan(R)`---索引扫描算法 ：{{c1::扫描结果未排序:`B(R)`}}
  + `SortIndexScan(R)` ：{{c1::扫描结果排序:`B(R) or3B(R)`}}
+ 非聚簇关系—关系的元组不一定集中存放(一个块中不仅是一个关系中的元组): 
  + 扫描结果未排序:{{c1::`T(R)`}}
  + 扫描结果排序:{{c1::`T(R) + 2B(R)`}}
+ **一趟算法特点**：{{c1::只要有一个关系能够全部装入内存即可实施}}

### 一趟扫描算法，一元操作：`Distinct`操作实现算法 [ ](DatabaseSystem_20210625113159442)
+ 算法复杂性：{{c1::`B(R)`}}
+ 应用条件：{{c1::`B(&(R))<=M`}}
+ 实现思路图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210625214803.png) }}

### 一趟扫描算法，一元操作：分组操作 [ ](DatabaseSystem_20210625113159445)
+ 算法复杂性：{{c1::`B(R)`}}
+ 应用条件：{{c1::所有分组的数量应能在内存中完整保存}}
+ 实现思路图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210625215549.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210625215724.png) }}

### 一趟扫描算法，实现二元操作 [ ](DatabaseSystem_20210625113159448)
+ 算法复杂性：{{c1::`B(R)+B(S)`}}
+ 应用条件：{{c1::`min(B(R),B(S))<=M`}}
+ 实现思路图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210625220027.png)}}
+ 连接操作实现算法P4的改进示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210625220200.png)}}

### 基于索引的算法：索引应用分析示例 [ ](DatabaseSystem_20210625113159451)
+ 问题：考虑示例中关系**聚簇**，**非聚簇**下，是否使用**索引**各种情况下的查询代价![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210625220425.png)
+ 答：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210625220925.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210625221032.png)}}

### 基于有序索引的连接算法： Zig-Zag连接算法 [ ](DatabaseSystem_20210625113159454)
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210625221032.png)}}
