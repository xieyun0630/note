## 概论
### 数据库核心划分
+ 7大部分图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209201627.png)}}

### 数据库系统课程与其他课程之间的关系
+ 图示：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209201925.png)

### Table的构成暨关于Table的常用术语
+ 列/字段/属性/数据项
+ 行/元组/记录
+ (关系)模式
+ 表/关系
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209203109.png)}}

### 什么是数据库系统?
+ **DB**：{{c1::数据库(DB): Database}}
+ **DBMS**：{{c1::数据库管理系统(DBMS): Database Management System}}
+ **DBAP**：{{c1::数据库应用(DBAP): DataBase Application}}
+ **DBA**：{{c1::数据库管理员(DBA): DataBase Administrator}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209203645.png)}}

## 数据库系统的结构抽象

### 数据库系统的标准结构：DBMS管理数据的三个层次
**External Level**: {{c1:: **User Level** 某一用户能够看到与处理的数据,   全局数据中的某一部分}}
**Conceptual Level**: {{c1:: **Logic level** 从全局角度理解/管理的数据, 含相应的关联约束}}
**Internal Level**: {{c1:: **Physical level** 存储在介质上的数据，含存储路径、存储方式 、索引方式等}}
+ 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209211746.png)}}

### 数据库系统的标准结构：数据与数据的结构（模式）
+ **Schema**：{{c1::模式(Schema)对数据库中数据所进行的一种结构性的描述，所观察到数据的结构信息}}
+ **View/Data**：{{c1::视图(View)/数据(Data)某一种表现形式下表现出来的数据，库中的数据}}
+ 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209212118.png)}}

### 数据库系统的标准结构：三级模式两层映像
+ 三级模式:
  + **External Schema**:{{c1::(External) View,某一用户能够看到与处理的数据的结构描述}}
  + **(Conceptual) Schema**:{{c1::Conceptual View,从全局角度理解/管理的数据的结构描述, 含相应的关联约束,体现在数据之间的内在本质联系}}
  + **Internal Schema**:{{c1::Internal  View,存储在介质上的数据的结构描述，含存储路径、存储方式 、索引方式等}}
+ 两层映像:
  + **E-C Mapping**：{{c1::**External Schema-Conceptual Schema Mapping**,将外模式映射为概念模式，从而支持实现数据概念视图向外部视图的转换,便于用户观察和使用}}
  + **C-I Mapping**：{{c1::**Conceptual Schema-Internal Schema Mapping**，将概念模式映射为内模式，从而支持实现数据概念视图向内部视图的转换,便于计算机进行存储和处理}}
+ 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209213434.png)}}

### 数据库系统的标准结构：三级模式两层映像
+ 两个独立性
  + 逻辑数据独立性：{{c1::当概念模式变化时，可以不改变外部模式(只需改变E-C Mapping)，从而无需改变应用程序}}
  + 物理数据独立性：{{c1::当内部模式变化时，可以不改变概念模式(只需改变C-I Mapping) ，从而不改变外部模式}}
+ 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209220736.png)}}

### 数据模型
+ 数据模型：{{c1::数据模型是对模式本身结构的抽象，模式是对数据本身结构形式的抽象}}
+ 三大经典数据模型
  + 关系模型：{{c1::表的形式组织数据}}
  + 层次模型：{{c1::树的形式组织数据}}
  + 网状模型：{{c1::图的形式组织数据}}
+ 图例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209235136.png)}}

### 数据库系统的演变与发展
+ 由文件系统到数据库：{{c1::主要不足为数据的组织及语义紧密依赖于处理该文件的应用程序**高度耦合**}}
+ 由层次/网状模型数据库到关系数据库：{{c1::主要不足为数据之间的关联关系由复杂的指针系统来维系，**结构描述复杂**}}
+ 由关系数据库到对象关系数据库、面向对象数据库：
  + 对象-关系数据库：{{c1::可有效支持不满足关系第
1范式的数据项，![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210209234714.png)}}
  + 面向对象数据库：{{c1::面向对象技术(O-O)与集合/聚集操作技术(SQL)的结合}}
+ 由普通数据库到与各种先进技术结合所形成的新型数据库：
  + {{c1::**Statistical Database**： DB + 统计学。}}
  + {{c1::**Internet Database**： DB + Internet/WWW(网页/HTML文档)。...}}

### “表”的严格定义：关系
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

### 关系的特性
+ 列是同质：{{c1::即每一列中的分量来自同一域，是同一类型的数据}}
+ 不同的列可来自同一个域：{{c1::称其中的每一列为一个属性，不同的属性要给予不同的属性名。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210210022142.png)}}
+ 列位置互换性：{{c1::区分哪一列是靠列名}}
+ 行位置互换性：{{c1::区分哪一行是靠**某一**或**某几**列的值(关键字/键字/码字)}}
+ 注意元组的重复：{{c1::理论上，关系的任意两个元组不能完全相同。(集合的要求：集合内不能有相同的两个元素)；现实应用中，**表(Table)**可能并不完全遵守此特性。}}

### 关系的第一范式
+ 第一范式：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210210022538.png)}}

