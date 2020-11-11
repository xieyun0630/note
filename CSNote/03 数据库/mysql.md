## mysql基本概念 [ ](mysql_20200824100448996)

### 数据库的概念 [ ](mysql_20200824100448999)

+ 数据库的作用：{{c1:: 高效的存储和管理数据，为编程语言提供数据支撑 }}
+ 数据库的目的:{{c1::就是能够存储（写）和提供（读）数据 }}

### 数据库分类 [ ](mysql_20200824100449001)
数据库分类：根据数据库的架构和数据组织原理进行分类
1. 早期根据数据库的组织数据的存储模型分类
   + 层次数据库：{{c1:: 基于层次的数据结构（数据分层） }}
   + 网状数据库：{{c1:: 基于网状的数据结构（数据网络） }}
   + 关系数据库：{{c1:: 基于关系模型的数据结构（二维表） }}
2. 现在较多根据实际数据管理模型分类（存储介质）
   + 关系型数据库：{{c1:: 基于关系模型的数据结构（二维表）通常存储在磁盘 }}
   + 非关系型数据库：{{c1:: 没有具体模型的数据结构（键值对）通常存储在内存 }}

### 关系型数据库系统（DBS）模型有四层结构 [ ](mysql_20200824100449003)

1. {{c1:: 数据库管理系统（DBMS）：管理系统运行（DataBase Management System） }}
2. {{c1:: 数据库（DB）：数据存储的管理者（小管理，受DBMS管理） }}
3. {{c1:: 数据表（Table）：数据关系管理者 }}
4. {{c1:: 数据字段（Field）：依赖于数据表，实际数据存储者 }}

### 非关系型数据库特点 [ ](mysql_20200824100449005)

1. 非关系型数据库：{{c1:: NoSQL（Not only SQL），不仅仅是关系型数据库 }}
2. 数据存储模型：{{c1:: 键值对（key->value） }}
3. 存储的位置：{{c1:: 是内存（效率高） }}
4. 不能永久性存储：{{c1:: 需要定时存到关系型数据库中 }}

### 常见的非关系型数据库产品 [ ](mysql_20200824100449008)

1. {{c1:: MongoDB }}
2. {{c1:: Redis }}
3. {{c1:: Memcached }}

### NoSQL数据库与关系型数据库比较 [ ](mysql_20200824100449010)

+ 联系：{{c1:: NoSQL通常是与关系型数据库配合使用的，他们彼此是一种互补关系 }}
+ NoSQL运行在内存，解决{{c1::效率}}问题 
  + {{c1:: I/O问题 }}
  + {{c1:: 效率问题 }}
+ MySQL运行在磁盘，解决{{c1::稳定}}问题 
  + {{c1:: 安全问题（永久存储） }}
  + {{c1:: 稳定 }}

### SQL根据操作不同，分为几类 [ ](mysql_20200824100449013)

1. DQL：{{c1:: Data Query Language，数据查询语言，用于查询和检索数据}}
2. DML：{{c1:: Data Manipulation Language，数据操作语言，用于数据的写操作（增删改） }}
3. DDL：{{c1:: Data Definition Language，数据定义语言，用于创建数据结构}}
4. DCL：{{c1:: Data Control Language，数据控制语言，用于用户权限管理}}
5. TPL：{{c1:: Transaction Process Language，事务处理语言，辅助DML进行事务操作（因此也归属于DML） }}

### 客户端需要连接认证 [ ](mysql_20200824100449016)

+ 命令：{{c1::  `mysql -uroot -p123456` }}
+  -h：{{c1:: 主机地址（本机localhost可以省略） }}
+  -P：{{c1:: 端口号（默认3306可以省略） }}
+  -u：{{c1:: 用户名 }}
+  -p：{{c1:: 用户密码 }}

### 客户端退出服务端命令 [ ](mysql_20200824100449018)

1. {{c1::`\q`}}
2. {{c1::`quit`}}
3. {{c1::`exit`}}

## MYSQL的基本操作 [ ](mysql_20200824100449021)

### SQL指令语句结束符： [ ](mysql_20200824100449024)

+ 默认是英文分号：{{c1:: `;`、`\g`、`\G` }}
+ \G：{{c1:: 主要用于查询数据，立体展示结果}}

### 基本操作 [ ](mysql_20200824100449026)

+ 结构创建:{{c1::`create 结构类型 结构名 结构描述;`}}
+ 显示结构：{{c1::`show 结构类型（复数）;`}}
+ 显示结构创建详情：{{c1::`show create 结构类型 结构名;`}}
+ 新增数据:{{c1::`insert into 表名 values`}}
+ 查看数据:{{c1::`select from 表名`}}　　
+ 更新数据:{{c1::`update 表名 set `}}
+ 删除数据:{{c1::`delete from 表名`}}

## SQL库操作 [ ](mysql_20200824100449029)

### 创建数据库 [ ](mysql_20200824100449031)

1. 创建一个指定名字的数据库:{{c1:: `create database db_1;` }}
2. 创建一个指定字符集的数据库:{{c1:: `create database db_2 charset utf8MB4;` }}
3. 创建一个指定校对集的数据库:{{c1:: `create database db_3 charset utf8MB4 collate utf8mb4_general_ci;` }}
4. 数据库文件夹位置：TODO

### 显示数据库 [ ](mysql_20200824100449034)
+ 显示所有数据库:{{c1::`show databases;` }}
+ 显示数据库创建指令:{{c1::`show create database db_1;` }}

### 使用数据库 [ ](mysql_20200824100449037)

1. 使用数据库的指令是：{{c1:: `use 数据库名字;` }}
2. 使用数据库的目标
   + {{c1:: 让系统知道后续SQL指令都是针对当前选择的数据库 }}
   + {{c1:: 简化后续SQL指令的复杂度（如果不指定数据库，那么所有的SQL操作都必须强制指定数据库名字） }}

### 修改数据库 [ ](mysql_20200824100449040)

+ 数据库名字不可修改（老版本可以）解决方法：
  +  {{c1:: 先新增 }}
  +  {{c1:: 后迁移 }}
  +  {{c1:: 最后删除 }}
+ 修改数据库字符集：{{c1:: `alter database db_2 charset gbk;` }}
+ 修改数据库校对集（校对集必须对应字符集）:{{c1:: `alter database db_3 charset gbk collate gbk_chinese_ci;` }}
+ 一般我们都不会使用数据库修改（一般要改也是删除后新增）

### 删除数据库 [ ](mysql_20200824100449042)

+ 语法: {{c1:: `drop database db_1;` }}
+ 注意：{{c1:: 数据库的删除不可逆，千万要谨慎，删除之前得备份  }}
吗
## SQL表（字段）操作 [ ](mysql_20200824100449045)

### 创建数据表 [ ](mysql_20200824100449047)
+ 表创建语法
    {{c1::
    ```sql
        create table [数据库名.]表名(
            字段名 字段类型,
            ...
            字段名 字段类型
        )表选项;
        
    ```
    }}
+ 表可以指定表选项（都有默认值）
  +  存储引擎：{{c1:: engine [=] 具体存储引擎 }}
  +  字符集：{{c1:: [default] charset 具体字符集（继承数据库） }}
  +  校对集：{{c1:: collate（继承数据库） }}
  +  创建数据表——表选项
    {{c1::
    ```sql
        create table t_3(
            name varchar(50)
        )engine Innodb charset utf8MB4;
    ```
    }}
+ 如果想创建一个与已有表一样的数据表，MySQL提供了一种便捷的复制模式:
  
  + {{c1:: `create table 表名 like 数据库名字.表名` }}

### 数据引擎：`MyISAM` 和 `InnoDB` 的区别 [ ](mysql_20200824100449049)
+  `InnoDB`
  +  {{c1:: 默认存储引擎 }}
  +  {{c1:: 支持事务处理和外键 }}
+  `MyIsam`
  +  {{c1:: 不支持事务和外键 }}
  +  {{c1:: 数据、表结构、索引独立管理 }}
  +  {{c1:: MySQL5.6以后不再维护 }}

### 显示数据表 [ ](mysql_20200824100449052)

1. 显示所有数据表——当前数据库下:{{c1::`show tables;`}}
2. 显示所有数据表——指定数据库:{{c1::`show tables from db_3;`}}
3. 显示部分关联数据表——匹配:{{c1::`show tables like '%like'; # _表示匹配一个字符（固定位置），%表示匹配N个字符`}}
4. 显示数据表的创建指令:{{c1::`show create table t_1; # 看到的结果未必一定是真实创建的指令（系统会加工）`}}

### 查看数据表 [ ](mysql_20200824100449054)
+ 目的：指查看数据表中的具体结构
+ 查看语法有三种（效果一样）:
  + {{c1:: `desc 表名；` }}
  + {{c1:: `describe 表名;` }}
  + {{c1:: `show columns from 表名;` }}

### 更改数据表 [ ](mysql_20200824100449056)

1. 修改表名:{{c1:: `rename table t_1 to t1;` }}
    + 跨库修改：{{c1:: 需要使用`数据库名.表名` }}
2. 修改表选项:{{c1:: `alter table t1 charset utf8;` }}

### 更改字段 [ ](mysql_20200911094545374)

+ 新增字段:{{c1:: `alter table 表名 add [column] 字段名 字段类型 [字段属性] [字段位置]`}}
  + 字段位置分为两种：
      +  为t_3表增加一个id字段，放到最前面:{{c1:: `alter table t_3 add id int first;`}}
      +  在t_3表name字段后增加一个身份证字段card:{{c1:: `alter table t_3 add card varchar(18) after name;`}}
+ 更改字段名:{{c1:: `alter table 表名 change 原字段名 新字段名 字段类型 [字段属性] [字段位置]`}}
  + 修改身份证的类型为char(18)并且位置放到id后面:{{c1:: `alter table t_3 modify sfz char(18) after id;`}}
+ 删除字段:{{c1:: `alter table 表名 drop 字段名;`}}
  + 注意：{{c1:: 同时会删除字段对应的数据，而且不可逆}}

### SQL数据操作 [ ](mysql_20200911094545377)

+ 新增数据：数据插入分两种方式
  +  全字段插入：{{c1:: `insert into 表名 values(字段列表顺序对应的所有值);` }}
  +  部分字段插入：{{c1:: `insert into 表名 (字段列表) values(字段列表对应的值顺序列表);` }}
+ 更新数据：
  + 语法： {{c1:: `update 表名 set 字段 = 新值[,字段 = 新值] [where条件筛选];` }}
+ 删除数据：
  + 语法： {{c1:: `delete from 表名 [where条件];` }}

+ MySQL内部对象存在字符集继承：{{c1:: `字段 -> 表 -> 数据库 -> DBMS`}}
+ 客户端与服务器进行交互时，需要明确告知服务器客户端自己的字符集（数据格式）:{{c1:: `set names 客户端字符集;`}}

### `set names 字符集`是一种快捷方式，本质有三个变量被修改: [ ](mysql_20200911094545379)

1. {{c1::`character_set_client`： 服务端接收客户端数据 }}
2. {{c1::`character_set_connection`： 服务端内部连接使用 }}
3. {{c1::`character_set_results`： 服务端提供数据给客户端 }}

### 校对集概念 [ ](mysql_20200911094545381)

**校对集**：{{c1:: collate/collation，即数据比较时对应的规则 }}
+  校对集依赖字符集,每个字符集有多种校对规则
+  校对集的校对方式分为三种
  +  大小写不敏感：{{c1:: `_ci，case insensitive（不区分大小写）` }}
  +  大小写敏感：{{c1:: `_cs，case sensitive（区分大小写）` }}
  +  二进制比较：{{c1:: `_bin，binary（区分大小写）` }}
+  校对集是在进行数据比较的时候触发
+ 校对规则可以在MySQL四种内部对象中设置:{{c1:: `DBMS->DB->Table->Field` }}
+ 校对集对应的数据一旦产生，那么就不可以修改数据表的校对规则

### 校对集设置语法 [ ](mysql_20200911094545384)

1. 查看MySQL支持的所有校对集：{{c1::`show collation;`}}
2. 在数据**库**层设计校对集（常见）：{{c1::`create database db_4 charset utf8mb4 collate utf8mb4_bin;`}}
3. 在数据**表**层设计校对集:
  ```sql
    #{{c1::
    create table t_4(
      id int,
      name varchar(10)
    )charset utf8mb4 collate utf8mb4_bin;
    #}}
  ```
4. 在**字段**层设计校对集（一般不常用）:
  ```sql
    #{{c1::
    create table t_5(
      id int,
      name varchar(10) collate utf8mb4_bin
    )charset utf8mb4;
    #}}
  ```
## Mysql数据库字段详解 [ ](mysql_20200911094545386)

### mysql的数据类型 [ ](mysql_20200911094545389)

+ 作用：{{c1:: 强制规范录入数据的格式 }}
+ MySQL中有四种数据类型规范
  +  {{c1:: 整数类型 }}
  +  {{c1:: 小数类型 }}
  +  {{c1:: 字符串类型 }}
  +  {{c1:: 时间日类类型 }}

### 整数类型 [ ](mysql_20200911094545392)

  + MySQL中为了**数据空间**的有效使用，设定了五种整数类型
  +  {{c1:: 迷你整型：`tinyint`，使用**1个字节**存储整数，最多存储256个整数（-128~127） }}
  +  {{c1:: 短整型：`smallint`，使用**2个字节**存储整数 }}
  +  {{c1:: 中整型：`mediumint`，使用**3个字节**存储整数 }}
  +  {{c1:: 标准整型：`int`，使用**4个字节**存储整数 }}
  +  {{c1:: 大整型：`bigint`，使用**8个字节**存储 }}
+ 有符号与无符号：{{c1:: 默认是有符号的，无符号需要使用unsigned修饰整型}}
  例：{{c1:: `sales mediumint unsigned,` }}

### 显示宽度 [ ](mysql_20200911094545396)

+ 语法:{{c1:: `alter table t_9 add d tinyint(2) zerofill; # 0填充只能针对正数` }}
1. {{c1:: 显示宽度是显示整型能表示的最多符号数量 }}
2. {{c1:: 显示宽度能主动设置，但是绝对不会改变类型本身能表示的数据大小 }}

### `zerofill`关键字 [ ](mysql_20200911094545399)
1. 作用：{{c1:: 强制让不够宽度的数据补充前置0来达到显示宽度 }}
2. 使用类型限制:{{c1:: 无符号整型 }}

### 小数类型（浮点型） [ ](mysql_20200911094545404)

**浮点数**：{{c1:: `float/double`，存储不是特别精确的数值数据 }}
* 浮点数又称之为精度数据，分为两种
  * 单精度：`float`:{{c1:: 使用4个字节存储，精度范围为6-7位有效数字 }}
  * 双精度：`double`:{{c1:: 使用8个字节存储，精度范围为14-15位有效数字 }}
* 浮点数超过精度范围会自动进行{{c1:: **四舍五入** }}
* 精度可以指定整数和小数部分
  * 默认不指定：{{c1:: 整数部分不超过最大值，小数部分保留2位 }}
  * 指定：{{c1:: `float/double(总长度,小数部分长度)` }}
* 可以使用科学计数法插入数据：{{c1:: `AeB` }}

### 小数类型（定点型） [ ](mysql_20200911094545406)

**定点型**：{{c1:: `decimal` }}
* 不固定存储空间存储
* 每9个数字使用4个字节存储
* 定点型可以指定整数部分长度和小数部分长度
  * 默认不指定：{{c1:: 10位有效整数，0位小数 }}
  * 可以指定：{{c1:: decimal(有效数位,小数部分数位) }}
  * 有效数位最大：{{c1:: 不超过65个 }}
* 数据规范
  * 整数部分超出：{{c1:: 报错 }}
  * 小数部分超出：{{c1:: 四舍五入 }}


### 字符串类型`char(L)`（定长型） [ ](mysql_20200911094545408)

**定长型**：{{c1:: `char(L)` }}
* 定长是指定存储长度
* 定长的长度是字符而不是字节
  * L的最大值是：{{c1:: 255 }}
  * 实际存储空间：{{c1:: L字符数 * 字符集对应字节数 }}
* 注意定长型存储的数据：{{c1:: 不能超过指定长度，但是可以小于指定长度 }}
* 字符串数据使用{{c1:: 单引号或者双引号包裹 }}
+ 特点：{{c1:: 访问效率较高，但是空间利用率不高  }}

### 字符串类型`varchar(L)`（变长型） [ ](mysql_20200911094545410)

**变长型**：{{c1:: `varchar(L)` }}
* 变长型的存储空间是由实际存储数据决定的
  * L指定的是最{{c1:: 大存储的数据长度 }}
  * L最大值理论是{{c1:: `65535` }}
  * 变长需要额外产生1-2个字节，用来记录实际数据的长度
    * 数据长度小于256个:{{c1:: 多1个字节 }}
    * 数据长度大于256个:{{c1:: 多2个字节 }}
  * 实际存储空间：{{c1:: 实际字符数 * 字符集对应字节数 + 长度记录 }}
* 变长数据不能超过定义的最大长度
+ 特点：{{c1:: `在读取时需要进行长度计算，所以效率没有char(L)字符串高` }}

### 字符串类型（文本字符串） [ ](mysql_20200911094545413)

1. 作用:{{c1:: 文本类型是专门用来存储长文本的 }}
  * `text`：{{c1:: 普通文本字符 }}
  * `blob`：{{c1:: 二进制文本字符 }}
2. 一般文本长度超过255的（较长）都使用:{{c1:: `text` }}
3. text/blob根据数据存储长度有很多种，但是一般使用`text/blob`，因为文本会根据数据长度自适应选择

### 字符串类型（枚举） [ ](mysql_20200911094545415)

+ 语法：{{c1:: `type enum('小朋友','少年','青年','中年','老年')` }}
* 实际存储格式：{{c1:: 数值，从`1`开始映射对应的元素数据 }}
+ 存储大小：{{c1:: `1-2`字节 }}
+ 最大选项数：{{c1:: `65535` }}


### 字符串类型（集合） [ ](mysql_20200911094545418)

* 集合类似{{c1:: 一种多选框 }}
* 集合使用{{c1:: 1-8 }}个字节存储数据，最多可以设计{{c1:: 64 }}个元素
* 集合实际存储是{{c1:: 使用数值（二进制位），映射对应的元素数据，每个元素对应一个比特位 }}
* 集合语法：{{c1:: `set(元素1,元素2,...元素N)` }}
+ 集合定义原理
  | 集合数据        | 映射位            |
  | --------------- | ----------------- |
  | {{c1:: 元素1 }} | {{c1:: 00000001}} |
  | {{c1:: 元素2 }} | {{c1:: 00000010}} |
  | {{c1:: ...   }} | {{c1:: ...     }} |
  | {{c1:: 元素8 }} | {{c1:: 10000000}} |

### 时间日期类型（年） [ ](mysql_20200911094545420)

+ MySQL中使用{{c1:: 1 }}个字节存储年份
+ year的特殊值是：{{c1:: 0000 }}
+ year类型允许使用2位数来插入，系统会自动匹配对应的年份
* 69以前：{{c1:: 系统加上2000 }}
* 69以后：{{c1:: 系统加上1900 }}

### 时间日期类型（时间戳） [ ](mysql_20200911094545423)

**时间戳**作用：{{c1:: timestamp，基于格林威治时间的时间记录 }}
* MySQL中时间戳表现形式不是秒数，而是年月日时分秒格式
  * {{c1:: YYYY-MM-DD HH:II::SS }}
  * {{c1:: YYYYMMDDHHIISS }}
* timestamp使用4个字节存储
* timestamp的特点:{{c1:: 所对应的记录不论哪个字段被更新，该字段都会更新到当前时间 }}
+ 在MySQL8以后，取消了timestamp的默认自动更新，如果需要使用，需要额外使用属性： `alter table t_19 add c_time timestamp on update current_timestamp;`

### 时间日期类型（日期） [ ](mysql_20200911094545426)

**日期**作用：{{c1:: `date`，用来记录年月日信息 }}
* 使用3个字节存储数据
* 存储日期的格式为：{{c1:: `YYYY-MM-DD` }}
* 存储的范围是：{{c1:: `1001-01-01~9999-12-31` }}
+ 可以使用纯数字插入：`insert into t_21 values('Tom','10011212');`

### 时间日期类型（日期时间） [ ](mysql_20200911094545428)

**日期时间**作用：{{c1:: datetime，用来综合存储日期和时间 }}
* 使用8个字节存储数据
* 存储格式为：{{c1:: YYYY-MM-DD HH:II:SS }}
* 存储区间为：{{c1:: 1000-01-01 00:00:00 到9999-12-31 23:59:59 }}
+ 可以使用纯数字插入：{{c1:: `insert into t_21 values('Tom','10011212182323');` }}

### 时间日期类型（时间） [ ](mysql_20200911094545430)
**时间**作用：{{c1:: time，用来记录时间或者时间段 }}
* 使用3个字节存储数据
* 数据范围是 `-838:59:59` - `838:59:59`
* 数据插入的格式分为两种
  * 时间格式：{{c1:: [H]HH:II:SS（[]表示可以没有） }}
  * 时间段格式：{{c1:: D HH:II:SS（D表示天） }}
+ 通常被用来:{{c1:: 做时间段计算：如多少天后的什么时间点（可以理解为过期检查）}}


### MySQL4种数据类型概况 [ ](mysql_20200911094545433)

1. {{c1:: 整数类型,常用类型：`tinyint、int`}}
2. {{c1:: 小数类型,常用类型：`decimal、float`}}
3. {{c1:: 字符串类型,常用类型：`char、varchar、text`}}
4. {{c1:: 时间日期类型（不常用：通常使用真正时间戳存储数据，然后编程进行灵活解读） }}

## 字段属性 [ ](mysql_20200911094545437)

### `Null/Not Null`属性是用来限定数据是否为Null值的 [ ](mysql_20200911094545439)

  + 默认:{{c1:: 是允许为Null值 }}
  + 不允许为空：{{c1:: Not Null }}

### Default属性 [ ](mysql_20200911094545441)

+ 语法：`money decimal(16,2) default 0.00 not null`
+ 触发默认值
  * 自动触发：{{c1:: 数据插入时不给字段赋值 }}
  * 手动触发：{{c1:: 数据插入时主动使用default关键字 }}

### 主键 [ ](mysql_20200911094545444)

**主键**：{{c1:: `primary key`，用来保证整张表中对应的字段永远不会出现重复数据}}
* 唯一性：{{c1:: 主键在一张表中只能有一个 }}
* 索引：{{c1:: 主键的字段会自动创建索引 }}
* 主键不能为空：{{c1:: Not Null（默认） }}
* **逻辑主键**：{{c1:: 数据没有具体业务意义，纯粹是一种数值数据 }}
  * 逻辑主键通常是整数：{{c1:: int }}
  * 逻辑主键目的：{{c1:: 是方便检索和数据安全（不暴露数据真实信息）}}
* **复合主键**：{{c1:: 多个字段共同组成不能重复的数据 }}
  * 语法：{{c1:: `primary key(字段1,字段2,...字段N)` }}
  * 注意点：{{c1:: 联合主键使用不多，一般也不会超过2个字段 }}

### 主键管理 [ ](mysql_20200911094545446)

+ 删除主键语法：{{c1:: `alter table t_26 drop primary key;` }}
+ 后期新增主键语法：{{c1:: `alter table t_26 add primary key(account,name);` }}
  + 注意：{{c1:: 如果是针对业务主键需要保证字段数据没有Null数据且没有数据重复 }}

### 自增长属性 [ ](mysql_20200911094545448)
**自增长**：{{c1:: `auto_increment`}}
+ 语法：{{c1:: `id int primary key auto_increment` }}
+ 必要条件：{{c1:: 自增长只能是整数类型，而且对应的字段必须是一个索引（通常逻辑主键） }}
+ 唯一性：{{c1:: 一张表只能有一个自动增长类型 }}
+ 自增长的触发:{{c1:: 通过不给值（默认值）实现自动计算 }}
+ 自增长属性由两个变量控制
* 初始值：{{c1:: `auto_increment_offset`，默认是1 }}
* 步长：{{c1:: `auto_increment_increment`，默认值也是1 }}
* 查看自增长控制：{{c1:: `show variables like 'auto_increment%';` }}

### 自增长管理 [ ](mysql_20200911094545450)

+ 修改表中自增长的值，跳过一些值，直接从下次开始按照新的目标值出现
  ```sql
    #{{c1::
    alter table t_28 auto_increment = 50;
    #}}
  ```
+ 修改自增长控制：步长和起始值
  ```sql
    #{{c1::
    set auto_increment_increment = 2; # 当前用户当前连接有效（局部）
    set @@auto_increment_increment = 2; # 所有用户一直有效（全局）
    #}}
  ```

### 唯一键 [ ](mysql_20200911094545453)

**唯一键**：{{c1:: unique key，用来维护数据的唯一性 }}
+ 语法：{{c1:: `username varchar(50) unique, `}}
* 多个：{{c1:: 一个表中可以有多个唯一键 }}
* 唯一键与主键的区别:{{c1:: 在于唯一键允许数据为Null（而且Null的数量不限） }}
* 索引：{{c1:: 唯一键的字段会自动创建索引 }}
* 复合唯一键语法：{{c1:: `unique key(字段1,字段2,...字段N)` }}

### 唯一键管理 [ ](mysql_20200911094545456)

* 删除唯一键：一张表中不止一个唯一键，必须指定唯一键名字：{{c1:: `alter table 表名 drop index 唯一键名字；` }}
* 新增唯一键：{{c1:: `alter table 表名 add unique key(字段列表)；` }}

### 数据库记录长度 [ ](mysql_20200911094545460)

**数据库记录长度**：{{c1:: MySQL中规定一条记录所占用的存储长度最长不超过65535个**字节**}}
* 记录长度为：{{c1:: 表中所有字段预计占用的长度之和}}
* 所有字段只有允许Null存在：{{c1:: 系统就会预留一个字节存储Null（多个Null也只要一个就好）}}
* 因为MySQL记录长度的存在，varchar永远达不到理论长度
  * GBK存储：{{c1:: 65535（字符） * 2 + 2 = 131072（字节）}}
  * UTF8存储：{{c1:: 65535（字符） * 3 + 2 = 196607（字节）}}
* 一般数据长度超过255个字符都会{{c1:: 使用text/blob进行存储（数据存储不占用记录长度） }}

### 范式 [ ](mysql_20200911094545464)

## 范式 [ ](mysql_20200911094545467)
+ **范式**：{{c1:: `Normal Format`，表示一个关系内部各属性之间的联系的合理化程度 }}
* 范式目标:{{c1:: 在满足组织和存储的前提下使数据结构冗余最小化  }}
* 目前数据库应用到的范式有以下几层
  * {{c1:: 第一范式：1NF }}
  * {{c1:: 第二范式：2NF }}
  * {{c1:: 第三范式：3NF }}
  * {{c1:: 逆规范化 }}

### 第一范式 [ ](mysql_20200911094545470)

  + **第一范式**：{{c1:: 1NF，数据字段设计时必须满足**原子性**}}
  + **原子性**:{{c1:: 要求字段数据是不需要拆分就可以直接应用}}
  + 目的：{{c1:: 1NF就是要字段数据颗粒度最小，保证数据取出来使用的时候不用再拆分}}

### 第二范式 [ ](mysql_20200911094545472)

+ **第二范式**：{{c1:: 2NF，字段设计不能存在部分依赖 }}
+ 部分依赖：{{c1:: 首先表存在复合主键，其次有的字段不是依赖整个主键，而只是依赖主键中的一部分 }}
+ 正确方式：{{c1:: 将部分依赖关系独立成表 }}

### 第三范式 [ ](mysql_20200911094545474)

+ **第三范式**：{{c1:: 3NF，字段设计不能存在传递依赖}}
* 传递依赖：{{c1:: 字段某个非主属性不直接依赖主属性，而是通过依赖某个其他非主属性而传递到主属性之上}}
* 传递依赖解决：{{c1:: 让依赖非主属性的字段与依赖字段独立成表}}

### 一对一关系 [ ](mysql_20200914055152984)

**一对一关系**：{{c1:: 一张表中的一条记录与另外一张表中有且仅有一条记录有关系 }}
* 一对一关系通常是用来将一张原本就是一体的表拆分成两张表
  * {{c1:: 频繁使用部分：常用字段 }}
  * {{c1:: 不常使用部分：生僻字段 }}
  * {{c1:: 使用相同的主键对应 }}
* 一对一关系设计较多使用在优化方面

## mysql高级操作 [ ](mysql_20200914055152987)

### 批量插入 [ ](mysql_20200914055152989)

+ 全字段批量插入：{{c1:: `insert into 表名 values(值列表1),(值列表2),...(值列表N);`}}
+ 部分字段批量插入（注意字段默认值）：{{c1:: `insert into 表名 (字段列表) values (值列表1),(值列表2),...(值列表N);`}}

### 蠕虫复制 [ ](mysql_20200914055152991)

+ 蠕虫复制语法:{{c1:: `insert into 表名 [(字段列表)] select 字段列表 from 表名;` }}

### 主键冲突 [ ](mysql_20200914055152993)

+ **主键冲突**：{{c1:: 在数据进行插入时包含主键指定，而主键在数据表已经存在 }}
+ 解决方案
  * 忽略新数据：{{c1:: `insert ignore` }}
  * 更新部分数据：{{c1:: `insert ... on duplicate key update` }}
  * 全部替换：{{c1:: `replace into` }}

### 查询选项 [ ](mysql_20200914055152994)

+ `select`选项:{{c1:: select关键字之后，有两个互斥值 }}
  * {{c1:: `all`：默认，保留全部（关键字可以没有） }}
  * {{c1:: `distinct`：手动选择，去重（针对所选字段构成的记录，而不是某个字段） }}

### 字段别名 [ ](mysql_20200914055152996)

**字段别名**：给字段取的临时名字
* 字段别名语法
  * {{c1:: 字段名 as 别名 }}
  * {{c1:: 字段名 别名 }}
* 字段别名的目的通常为了保护数据
  * 字段冲突：{{c1:: 多张表同时操作有同名字段（系统默认覆盖），想保留全部 }}
  * 数据安全：{{c1:: 对外提供数据不使用真实字段名字 }}
+ 字段别名不能在where中使用

### 数据源 [ ](mysql_20200914055152997)

**数据源**：{{c1:: from关键字之后，数据的来源。只要最终结果是一个二维表，都可以当做数据}}源 
* 单表数据源：{{c1:: 数据源就是一张表  `from 表名`}}
* 多表数据源：{{c1:: 数据来源是多张表（逗号分隔） `from  表名1,表名2,...表名N`}}
* 子查询数据源：{{c1:: 数据来源是一个查询结果 `from (select 字段列表 from 表名) as 别名}}`
  * 数据源要求必须是{{c1:: 一个`表`}}
  * 如果是查询结果必须{{c1:: 给起一个表别名}}

### 回溯统计 [ ](mysql_20200914055152999)

**回溯统计**：{{c1:: 在进行分组时（通常是多分组），每一次结果的回溯都进行一次汇总统计}}
* 回溯统计语法：{{c1:: 在统计之后使用 `with rollup`}}
  + 例：{{c1:: `select count(*),class_name,gender,group_concat(name) from t_40 group by class_name,gender with rollup;`}}


### 分组排序 [ ](mysql_20200914055153001)

**分组排序**：{{c1:: 在分组后统计结果时可以根据分组字段进行升序或者降序显示数据 }}
* 默认:{{c1:: 升序排序 }}
* 可以设定分组结果的排序方式
  * {{c1:: group by 字段名 [ASC]：升序排序（默认） }}
  * {{c1:: group by 字段名 DESC：降序排序 }}


### limit子句 [ ](mysql_20200914055153002)

+ limit限制数量的方式有两种
  * {{c1:: `limit 数量`：限制获取的数量（不保证一定能获取到指定数量） }}
  * {{c1:: `limit 起始位置,数量`：限制数据获取的位置以及数量（分页） }}
+ 例：{{c1:: `select * from t_40 limit 3;` }}

### 限制更新/删除 [ ](mysql_20200914055153004)
+ 限制更新语法：{{c1:: update t_41 set account = account + 10 limit 3; }}
+ 限制删除语法：{{c1:: delete from t_41 where account = 0 limit 1; }}

### 清空数据 [ ](mysql_20200914055153005)

+ 本质是:{{c1:: 先删除表，后创建表,自增长重新回到初始值 }}
* 语法：{{c1:: `truncate 表名`}}

### 联合查询 [ ](mysql_20200914055153007)
**联合查询**：{{c1:: union，是指将多个查询结果合并成一个结果显示 }}
* 联合查询语法:
  ```sql
    #{{c1::
    select 查询【决定字段名字】
      union 查询选项
    select 查询
    #}}
  ```
* 联合查询要求：
  * {{c1:: 联合查询不要求字段类型一致，只对数量要求一致 }}
  * {{c1:: 联合查询的字段来源于第一个查询语句的字段 }}
* 查询选项：
  * {{c1:: all：保留所有记录 }}
  * {{c1:: distinct：保留去重记录（默认） }}

### 联合查询排序 [ ](mysql_20200914055153009)
1. 将t_40和t_42表的结果使用年龄降序排序
  ```sql
    #{{c1::
    select * from t_40
    union all
    select * from t_42
    order by age desc; #针对的是整个union之后的结果
    #}}
  ```
2. t_40表按年龄降序排序，t_42表按年龄升序排序
  ```sql
    #{{c1::
    (select * from t_40 order by age desc limit 99999)
    union 
    (select * from t_42 order by age desc limit 99999);
    #}}
  ```

### 连接查询 [ ](mysql_20200914055153010)
* 交叉连接:{{c1:: `cross join`，不需要连接条件的连接 }}
* 内连接:{{c1:: `[inner] join`，将两张表根据指定的条件连接起来，严格连接 }}
* 外连接:{{c1:: `outer join`，外连接是将主表的记录去匹配从表的记录,匹配失败（全表）：保留记录，只是从表字段置空 }}
  * 左外连接:{{c1:: `left join` }}
  * 右外连接:{{c1:: `right join` }}
* 自然连接:{{c1:: `natural join` }}
  * 自然连接不是一种特殊的连接方式，而是一种自动匹配条件的连接
  * 自然连接包含自然内连接和自然外连接
    * 自然内连接：{{c1:: `natural join`}}
    * 自然外连接：{{c1:: `natural left/right join`}}
* `using`关键字:{{c1:: 连接查询时如果是同名字段作为连接条件，using可以代替on出现（比on更好） }}
  * using是针对同名字段（using(id) === A.id = B.id）
  * using关键字使用后会自动合并对应字段为一个
  * using可以同时使用多个字段作为条件

### 子查询 [ ](mysql_20200914055153012)

**子查询**：`sub query`，将一条select查询结果当做另外一条select查询的**条件**或者**数据源**
* 位置分类
  * from子查询：{{c1:: 子查询出现在from后做数据源 }}
  * where子查询：{{c1:: 子查询出现在where后做数据条件 }}
* 按子查询得到的结果分类
  * 标量子查询：{{c1:: 子查询返回的结果是一行一列（一个数据） }}
    + 例:`select * from t_45 where c_id = (select c_id from t_46 where c_name = 'Computer');`
  * 列子查询：{{c1:: 子查询返回的结果是一列多行（一列数据） }}
    + 例:`select * from t_46 where c_id in (select distinct c_id from t_45 where c_id is not null);`
  * 行子查询：{{c1:: 子查询返回的结果是一行多列 }}
    + 例:`select * from t_40 where (gender,age) = (select gender,age from t_42 where name = '弥勒');`
  * 表子查询：{{c1:: 子查询返回的结果是一个二维表,表子查询通常解决的问题是提供数据源 }}
  * exists子查询：{{c1:: 子查询返回的结果是布尔结果（验证型） }}
    + 例:`select * from t_46 c where exists(select c_id from t_45 where c.c_id = c_id);`

### 比较方式 [ ](mysql_20200914055153013)

* 特定的比较方式都是基于比较符号一起使用
  * `all`：{{c1:: 满足后面全部条件  }}
  * `any`：{{c1:: 数据只要与结果集中的任何一个元素相等  }}
  * `some`：{{c1:: 满足任意条件（与any完全一样）  }}
+ 例：{{c1:: `select * from t_40 where age = some(select age from t_42);` }}


## 安全管理 [ ](mysql_20200914055153015)

### 外键 [ ](mysql_20200914055153017)

**外键**：{{c1:: foreign key，表中指**向外部表主键**的字段定义成外键 }}
* 语法:{{c1:: `[constraint 外键名] foreign key(当前表字段名) references 外部表(主键字段)` }}
* 外键构成条件
  * {{c1:: 外键字段必须与对应表的主键字段类型一致 }}
  * {{c1:: 外键字段本身要求是一个索引（创建外键会自动生成一个索引） }}

### 外键约束 [ ](mysql_20200914055153018)

**外键约束**：{{c1:: 当表建立外键关系后，外键就会对主表（外键指向的表）和子表（外键所在的表）里的数据产生约束效果 }}
* 外键约束控制：外键可以在定义时控制外键的约束作用
  * 控制类型
    * {{c1:: `on update`：父表更新时子表的表现 }}
    * {{c1:: `on delete`：父表删除时子表的表现 }}
  * 控制方式
    * {{c1:: `cascade`：级联操作，父表操作后子表跟随操作 }}
    * {{c1:: `set null`：置空操作，父表操作后，子表关联的外键字段置空 }}
    * {{c1:: `restrict`：严格模式，不允许父表操作（默认的） }}
    * {{c1:: `no action`：子表不管 }}
  + 约束语法：{{c1:: `foreign key(c_id) references t_50(id) on update cascade on delete set null` }}

### 外键管理 [ ](mysql_20200914055153020)

* 新增外键：{{c1:: `alter table 表名 add [constraint 外键名] foreign key(外键字段) references 表名(主键) [on 外键约束]` }}
  + 注意：{{c1:: 追加外键需要保证外键字段里的值要么为Null，要么在父表中都能找到 }}
* 删除外键：{{c1:: `alter table 表名 drop foreign key 外键名;` }}
* 更新外键：{{c1:: 先删除后新增 }}

### 事务处理 [ ](mysql_20200914055153021)

**事务处理**：{{c1:: 利用自动或者手动方式实现事务管理 }}
* 自动事务处理：{{c1:: 系统默认，操作结束直接同步到数据表（事务关闭状态） }}
  * 系统控制：{{c1:: 变量 autocommit（值为ON，自动提交） }}
* 手动事务处理
  * 开启事务： {{c1:: `start transaction` }}
  * 关闭事务
    * 提交事务：{{c1:: `commit`（同步到数据表同时清空日志数据） }}
    * 回滚事务：{{c1:: `rollback`（清空日志数据） }}
* 事务回滚：在长事务执行中，可以在某个已经成功的节点处设置回滚点，后续回滚的话可以回到某个成功点
  * 设置回滚点：{{c1:: `savepoint 回滚点名字` }}
  * 回滚到回滚点：{{c1:: `rollback to 回滚点名字` }}

### 事务特点 [ ](mysql_20200914055153023)

**事务特点**：事务处理具有ACID四大特性
* **原子性**：{{c1:: （Atomicity ）一个事务操作是一个整体，不可拆分，要么都成功，要么都失败}}
* **一致性**：{{c1:: （Consistency）事务执行之前和执行之后都必须处于一致性状态，数据的完整性没有被破坏（事务逻辑的准确性）}}
* **隔离性**：{{c1:: （Isolation ）事务操作过程中，其他事务不可见}}
* **持久性**：{{c1:: （Durability ）事务一旦提交，结果不可改变}}
* **事务锁**：{{c1:: 当一个事务开启时，另外一个事务是不能对当前事务锁占用的数据进行操作的}}
  * 行锁：{{c1:: 当前事务只占用了一行（id精确检索数据），那么其他事务可以操作其他行数据 }}
  * 表锁：{{c1:: 当前事务占用了整张表（like扫码整个表），那么其他事务对整张表都不能操作 }}
* **脏读**：{{c1:: 一个事务在对某个数据进行操作但尚未提交，而另外一个事务读到了这个“历史”数据其实已经被修改}}

### 预处理 [ ](mysql_20200914055153025)

+ 预处理属于**会话级别**：{{c1:: 即当前用户当次连接有效（断开会被服务器清理掉） }}
+ 预处理的作用:
  * 效率优化：{{c1:: 同样的SQL不用每次都进行编译（编译耗时） }}
  * 网络传输优化：{{c1:: 复杂的SQL指令只需要传输一次 }}
  * 安全：{{c1:: 有效防止SQL注入（外部通过数据的特殊使用使得SQL的执行方式改变） }}
+ 如果预处理的指令不是在一次连接中重复使用，那么预处理反而会降低效率。所以预处理的执行如果不是考虑到安全因素，那么一定是SQL需要重复执行

### 使用预处理向表中插入数据 [ ](mysql_20200914055153026)

```SQL
  # 准备预处理：涉及参数
  #{{c1::
  prepare t_40_insert from 'insert into t_40 values(null,?,?,?,?)';
  #}}

  # 设置变量并传入参数
  #{{c1::
  set @name = '药师兜';
  set @gender = '男';
  set @age = 23;
  set @class_name = '木叶1班';
  #}}

  # 执行预处理
  #{{c1::
  execute t_40_insert using @name,@gender,@age,@class_name;
  #}}
```
### 视图 [ ](mysql_20200914055153028)

+ 视图的目的
  * 方便提供全面数据：{{c1:: 可以根据需求组织数据，而实际上不会在数据库产生数据冗余 }}
  * 数据安全：{{c1:: 视图本质是来源于数据基表，但是对外可以保护基本的数据结构 }}
+ 创建视图语法：{{c1:: `create view 视图名字 as select指令;` }}

### 视图管理 [ ](mysql_20200914055153029)

**视图管理**：{{c1:: 对视图结构的管理 }}
* 视图查看：{{c1:: 显示视图结构和具体视图信息 }}
  + 查看全部视图:{{c1:: `show tables; `  }}
  + 查看视图创建指令:{{c1:: `show create table/view 视图名字; `  }}
  + 查看视图结构:{{c1:: `desc 视图名字;  `  }}
* 视图修改：更改视图逻辑
  + 更改视图:{{c1:: `alter view 视图名 as 新的查询指令;`  }}
  + 创建新的或者替换新的:{{c1:: `create or replace view 视图名 as 新的查询指令;`  }}
* 视图删除:{{c1:: `drop view 视图名; `  }}

### 视图数据操作 [ ](mysql_20200914055153031)

**视图数据操作**：直接对视图进行写操作（增删改）然后实现基表数据的变化
* 视图操作条件
  * **多基表视图**：{{c1:: 不允许操作（增删改都不行）}}
  * **单基表视图**：{{c1:: 允许增删改}}
    * **新增条件**：{{c1:: 视图的字段必须包含基表中所有不允许为空的字段}}
  * `with check option`：{{c1:: 操作检查规则}}
    * 默认不需要这个规则（创建视图时指定）：{{c1:: 视图操作只要满足前面上述条件即可}}
    * 增加此规则：{{c1:: 视图的数据操作后，必须要保证该视图还能把通过视图操作的数据查出来（否则失败）}}

### 视图算法 [ ](mysql_20200914055153033)

**视图算法**：{{c1:: 指视图在执行过程中对于内部的select指令的处理方式}}
* 指定语法：{{c1:: `create ALGORITHM = 算法 view 视图名字 as select指令;`}}
* 视图算法一共有三种
  * `undefined`：{{c1:: 默认的，未定义算法，即系统自动选择算法}}
  * `merge`：{{c1:: 合并算法，就是将视图外部查询语句跟视图内部select语句合并后执行，效率高（系统优先选择）}}
  * `temptable`：{{c1:: 临时表算法，即系统将视图的select语句查出来先得出一张临时表，然后外部再查询（temptable算法视图不允许写操作）}}

## 备份与还原 [ ](mysql_20200914055153034)

### 表数据备份 [ ](mysql_20200914055153036)
+ 表数据备份语法：
  ```sql
    #{{c1::
    select 字段列表|*  into outfile 外部文件路径 
      [fields terminated by 格式 enclosed by 格式]
      [lines terminated by 格式 starting by 格式]
    from 数据表;
    #}}
  ```
+ 表数据还原语法：
  ```SQL
    #{{c1::
    load data infile '数据文件所在路径' into table 表名
    [fields terminated by 格式 enclosed by 格式]
    [lines terminated by 格式 starting by 格式]
    [(字段列表)]; # 如果是部分表字段，那么必须将字段列表放到最后
    #}}
  ```

### 文件备份 [ ](mysql_20200914055153037)

+ **文件备份**：{{c1:: 直接对数据表进行文件保留，属于物理备份 }}
1. MyIsam表的文件备份：{{c1:: 找到三个文件，复制迁移 }}
  1. {{c1:: sdi：表结构文件 }}
  2. {{c1:: MYI：索引文件 }}
  3. {{c1:: MYD：数据文件 }}
2. InnoDB表的文件备份：{{c1:: 找到两个文件，复制迁移 }}
  1. {{c1:: ibd：表结构文件 }}
  2. {{c1:: bdata：所有InnoDB数据文件 }}
+ **文件还原**：{{c1:: 直接将备份的文件放到对应的位置即可 }}


## 账号管理 [ ](mysql_20200916055246268)

* MySQL中账号的组成分为两个部分：{{c1:: 用户名 @ 主机地址（root@localhost） }}
  * 主机地址：{{c1:: 是允许账号所在客户端的访问的客户端IP（如上述root只能在服务器本机通过客户端访问）}}
* 账号管理:
  * 创建账号：{{c1:: `create user 用户名@主机地址 identified by '明文密码';` }}
  * 删除账号：{{c1:: `drop user 用户名@主机地址` }}

### 权限管理 [ ](mysql_20200916055246271)

* 赋权：{{c1:: 给账号绑定相应的权限 `grant 权限列表 on 数据库|*.数据表|* to 用户名@主机地址 `}}
* 回收：{{c1:: 将账号已有的权限回收 `revoke 权限列表 on 数据库|*.数据表|* from 用户名@主机地址 `}}
* 刷新权限：{{c1:: `flush privileges`}}
* 查看权限：{{c1:: `show grants for 用户名@主机地址`}}

### 角色管理 [ ](mysql_20200916055246273)

* 创建角色：{{c1:: `create role 角色名字1[,角色名字2,...角色名字N]`（可批量创建） }}
* 分配权限：{{c1:: `grant 权限列表 on 数据库|*.数据表|* to 角色名字` }}
* 绑定角色：{{c1:: `grant 角色名字 to 用户名@主机地址` }}
* 撤销角色：{{c1:: `revoke 角色名字 from 用户名@主机地址` }}
* 回收角色权限：{{c1:: `revoke 权限列表 on 数据库|*.数据表|* from 角色名字` }}
* 删除角色：{{c1:: `drop role 角色名字1[,角色名字2,...角色名字N]` }}

### MySQL目前提供了以下4种索引类型： [ ](mysql_20200916055246275)

- `BTREE 索引` ： {{c1:: 最常见的索引类型，大部分索引都支持 B 树索引。 }}
- `HASH 索引`：{{c1:: 只有Memory引擎支持 ， 使用场景简单 。 }}
- `R-tree 索引`：{{c1:: 空间索引是MyISAM引擎的一个特殊索引类型，主要用于地理空间数据类型，通常使用较少，不做特别介绍。 }}
- `Full-text` ：{{c1:: 全文索引也是MyISAM的一个特殊索引类型，主要用于全文索引，InnoDB从Mysql5.6版本开始支持全文索引。 }}

### 索引分类 [ ](mysql_20200916055246276)

1. 单值索引：{{c1:: 即一个索引只包含单个列，一个表可以有多个单列索引 }}
2. 唯一索引：{{c1:: 索引列的值必须唯一，但允许有空值 }}
3. 复合索引：{{c1:: 即一个索引包含多个列 }}

### 索引管理 [ ](mysql_20200916055246278)
+ 创建索引:
  ```SQL
    #{{c1::
    CREATE  [UNIQUE|FULLTEXT|SPATIAL]  INDEX index_name 
    [USING  index_type]
    ON tbl_name(index_col_name,...)
    #}}
  ```
+ 查看索引:{{c1:: `show index from table_name;` }}
+ 删除索引:{{c1:: `drop index index_name on tbl_name;` }}

### 使用ALTER命令创建索引 [ ](mysql_20200916055246280)
+ 添加一个主键，这意味着索引值必须是唯一的，且不能为NULL：{{c1:: `alter  table  tb_name  add  primary  key(column_list); `}}
+ 创建索引的值必须是唯一的（NULL可能会出现多次）：{{c1:: `alter  table  tb_name  add  unique index_name(column_list);`}}
+ 添加普通索引， 索引值可以出现多次：{{c1:: `alter  table  tb_name  add  index index_name(column_list);`}}
+ 添加全文索引：{{c1:: `alter  table  tb_name  add  fulltext  index_name(column_list);`}}

### 索引设计原则 [ ](mysql_20200916055246282)

+ **索引创建场景**：{{c1:: 对查询频次较高，且数据量比较大的表建立索引。}}
+ **字段选择**:{{c1:: 最佳候选列应当从where子句的条件中提取，如果where子句中的组合比较多，那么应当挑选最常用、过滤效果最好的列的组合。}}
+ **唯一索引**：{{c1:: 区分度越高，使用索引的效率越高。}}
+ **性能影响**:{{c1::  注意索引对DML的性能影响}}
+ **使用短索引**:{{c1:: 假如构成索引的字段总长度比较短，那么在给定大小的存储块内可以存储更多的索引值，相应的可以有效的提升MySQL访问索引的I/O效率。}}
+ **利用最左前缀**:{{c1:: N个列组合而成的组合索引，那么相当于是创建了N个索引，如果查询时where子句中使用了组成该索引的前几个字段，那么这条查询SQL可以利用组合索引来提升查询效率。}}


### 存储过程和函数 [ ](mysql_20200916055246284)

+ 存储过程和函数的区别:{{c1:: 函数必须有返回值，而存储过程没有。 }}
+ 创建存储过程:
  ```SQL
  #{{c1::
    delimiter $
    CREATE PROCEDURE procedure_name ([proc_parameter[,...]])
    begin
      -- SQL语句
    end ;
    delimiter ;
  #}}
  ```
+ 调用存储过程:{{c1:: `call procedure_name();` }}
+ 查询db_name数据库中的所有的存储过程:{{c1:: `select name from mysql.proc where db='db_name';`}}
+ 查询存储过程的状态信息:{{c1:: `show procedure status;` }}
+ 查询某个存储过程的定义:{{c1:: `show create procedure test.pro_test1 \G;` }}
+ 删除存储过程:{{c1:: `DROP PROCEDURE  [IF EXISTS] sp_name;` }}

### 函数 [ ](mysql_20200916055246286)

+ 案例 : 定义一个存储过程, 请求满足条件的总记录数 ;
  ```SQL
    #{{c1::
      delimiter $
      create function count_city(countryId int)
      returns int
      begin
        declare cnum int ;
        select count(*) into cnum from city where country_id = countryId;
        return cnum;
      end$
      delimiter ;
    #}}
  ```
+ 调用: {{c1:: `select count_city(1);` }}

## MYSQL流程控制 [ ](mysql_20200916055246287)

### MYSQL流程控制：变量 [ ](mysql_20200916055246289)

+ 声明：{{c1:: `DECLARE var_name[,...] type [DEFAULT value]` }}
+ 赋值：{{c1:: `SET var_name = expr [, var_name = expr] ...` }}
+ `into`赋值：{{c1:: `select count(*) into countnum from city;` }}

### MYSQL流程控制：条件判断与传递参数 [ ](mysql_20200916055246291)

+ 传递参数语法格式：{{c1::`create procedure procedure_name([in/out/inout] 参数名   参数类型)`}}
+ 案例：
  ```text
    根据定义的身高变量，判定当前身高的所属的身材类型 
    180 及以上 ----------> 身材高挑
    170 - 180  ---------> 标准身材
    170 以下  ----------> 一般身材
  ```
+ 实现：
  ```SQL
  #{{c1::
    delimiter $
    create procedure pro_test5(in height int)
    begin
      declare description varchar(50) default '';
      if height >= 180 then
        set description='身材高挑';
      elseif height >= 170 and height < 180 then
        set description='标准身材';
      else
        set description='一般身材';
      end if;
      select concat('身高 ', height , '对应的身材类型为:',description);
    end$
    delimiter ;
  #}}
  ```

### MYSQL流程控制：case结构 [ ](mysql_20200916055246293)
+ 方式一 : 
  ```SQL
  #{{c1::
    CASE case_value
      WHEN when_value THEN statement_list
      [WHEN when_value THEN statement_list] ...
      [ELSE statement_list]
    END CASE;
  #}}
  ```
+ 方式二 : 
  ```SQL
  #{{c1::
    CASE
      WHEN search_condition THEN statement_list
      [WHEN search_condition THEN statement_list] ...
      [ELSE statement_list]
    END CASE;
  #}}
  ```

###  MYSQL流程控制：循环 [ ](mysql_20200916055246295)

  + 案例：计算从1加到n的值
    + while循环：
    ```SQL
      #{{c1::
        delimiter $
        create procedure pro_test8(n int)
        begin
          declare total int default 0;
          declare num int default 1;
          while num<=n do
            set total = total + num;
          set num = num + 1;
          end while;
          select total;
        end$
        delimiter ;
      #}}
    ```
    + repeat结构：
    ```SQL
      #{{c1::
        delimiter $
        create procedure pro_test10(n int)
        begin
          declare total int default 0;
          repeat 
            set total = total + n;
            set n = n - 1;
            until n=0  
          end repeat;
          select total ;
        end$
        delimiter ;
      #}}
    ```
    + loop结构：
    ```SQL
      #{{c1::
        delimiter $
        CREATE PROCEDURE pro_test11(n int)
        BEGIN
          declare total int default 0;
          ins: LOOP
            IF n <= 0 then
              leave ins;
            END IF;
            set total = total + n;
            set n = n - 1;
          END LOOP ins;
          select total;
        END$
        delimiter ;
      #}}
    ```

### 游标 [ ](mysql_20200916055246296)

+ 作用：{{c1:: 遍历**查询结果集**的数据类型 }}
+ 声明光标：{{c1:: `DECLARE cursor_name CURSOR FOR select_statement ;` }}
+ OPEN 光标：{{c1:: `OPEN cursor_name ;` }}
+ FETCH 光标：{{c1:: `FETCH cursor_name INTO var_name [, var_name] ...` }}
+ CLOSE 光标：{{c1:: `CLOSE cursor_name ;` }}
+ 获取结束flag:
  ```SQL
    #{{c1::
      DECLARE emp_result CURSOR FOR select * from emp;
      DECLARE EXIT HANDLER FOR NOT FOUND set has_data = 0;
    #}}
  ```

### 管理触发器 [ ](mysql_20200916055246298)

+ 创建触发器语法 : 
  ```SQL
    #{{c1::
    create trigger trigger_name 
    before/after insert/update/delete
    on table_name 
    [ for each row ]
    begin
      trigger_stmt ;
    end;
    #}}
  ```
+ 删除触发器语法:{{c1:: `drop trigger [schema_name.]trigger_name` }}
+ 查看触发器语法:{{c1:: `show triggers；` }}
+ oracle与mysql中`for each row`的区别：
  + {{c1:: oracle触发器中分行级触发器和语句级触发器,可不写foreachrow,无论影响多少行都只执行一次。}}
  + {{c1:: mysql不支持语句触发器,所以必须写foreachrow;}}
+ NEW 和 OLD的使用 
  | 触发器类型      | NEW 和 OLD的使用                                        |
  | --------------- | ------------------------------------------------------- |
  | INSERT 型触发器 | {{c1:: NEW 表示将要或者已经新增的数据                          }}|
  | UPDATE 型触发器 | {{c1:: OLD 表示修改之前的数据 , NEW 表示将要或已经修改后的数据 }}|
  | DELETE 型触发器 | {{c1:: OLD 表示将要或者已经删除的数据                          }}|

## SQL优化 [ ](mysql_20200916055246300)

### 整个MySQL Server由以下组成 [ ](mysql_20200916055246302)

- `Connection Pool` :{{c1:: 连接池组件}}
- `Management Services & Utilities` :{{c1:: 管理服务和工具组件}}
- `SQL Interface` :{{c1:: SQL接口组件}}
- `Parser` :{{c1:: 查询分析器组件}}
- `Optimizer` :{{c1:: 优化器组件}}
- `Caches & Buffers` :{{c1:: 缓冲池组件}}
- `Pluggable Storage Engines` :{{c1:: 存储引擎}}
- `File System` :{{c1:: 文件系统}}

### 存储引擎 [ ](mysql_20200916055246304)

+ 是什么：{{c1:: 存储引擎就是存储数据，建立索引，更新查询数据等等技术的实现方式 。 }}
+ mysql特点：{{c1:: Oracle，SqlServer等数据库只有一种存储引擎。MySQL提供了插件式的存储引擎架构。 }}
+ 查询当前数据库支持的存储引擎：{{c1:: `show engines` }}
+ 查看Mysql数据库默认的存储引擎:{{c1:: `show variables like '%storage_engine%'；` }}

### InnoDB与MyISAM特点与区别 [ ](mysql_20200916055246306)

+ InnoDB和MyISAM都是B+树的结构，实现方式差别：
  + {{c1:: InnoDB是聚簇索引（叶子节点存数据），MyISAM是非聚簇索引（叶子节点存指针） }}
  + 实现（图）：{{c1:: ![img](https://gitee.com/xieyun714/nodeimage/raw/master/img/1107494-20181127224013631-1598460643.png) }}
+ 功能差别：{{c1:: InnoDB 支持事务、行级锁, 而MyISAM都不支持 }}

### 查看MYSQL数据库中SQL执行频率 [ ](mysql_20200927095114644)

+ 查看服务器状态信息命令:{{c1::` show [session|global] status like 'Com_______';`}}
+ `Com_***      `:{{c1::  这些参数对于所有存储引擎的表操作都会进行累计。}}
+ `Innodb_*** `:{{c1::  这几个参数只是针对InnoDB 存储引擎的，累加的算法也略有不同。}}
+ 常见参数列表：
| 参数                 | 含义                                                         |
| :------------------- | ------------------------------------------------------------ |
| Com_select           | {{c1:: 执行 select 操作的次数，一次查询只累加 1。                   }}|
| Com_insert           | {{c1:: 执行 INSERT 操作的次数，对于批量插入的 INSERT 操作，只累加一次。 }}|
| Com_update           | {{c1:: 执行 UPDATE 操作的次数。                                     }}|
| Com_delete           | {{c1:: 执行 DELETE 操作的次数。                                     }}|
| Innodb_rows_read     | {{c1:: select 查询返回的行数。                                      }}|
| Innodb_rows_inserted | {{c1:: 执行 INSERT 操作插入的行数。                                 }}|
| Innodb_rows_updated  | {{c1:: 执行 UPDATE 操作更新的行数。                                 }}|
| Innodb_rows_deleted  | {{c1:: 执行 DELETE 操作删除的行数。                                 }}|
| Connections          | {{c1:: 试图连接 MySQL 服务器的次数。                                }}|
| Uptime               | {{c1:: 服务器工作时间。                                             }}|
| Slow_queries         | {{c1:: 慢查询的次数。                                               }}|

### 定位低效率执行SQL：`show processlist`命令 [ ](mysql_20200927095114646)

+ 图：![1556098544349](https://gitee.com/xieyun714/nodeimage/raw/master/img/1556098544349.png)
+ 各列含义
  + `id列`:{{c1::用户登录mysql时，系统分配的"connection_id"，可以使用函数connection_id()查看}}
  + `user列`:{{c1::显示当前用户。如果不是root，这个命令就只显示用户权限范围的sql语句}}
  + `host列`:{{c1::显示这个语句是从哪个ip的哪个端口上发的，可以用来跟踪出现问题语句的用户}}
  + `db列`:{{c1::显示这个进程目前连接的是哪个数据库}}
  + `command列`:{{c1::显示当前连接的执行的命令，一般取值为休眠（sleep），查询（query），连接（connect）等}}
  + `time列`:{{c1::显示这个状态持续的时间，单位是秒}}
  + `state列`:{{c1::以查询为例，可能需要经过`copying to tmp table`、`sorting result`、`sending data`等状态才可以完成}}
  + `info列`:{{c1::显示这个sql语句，是判断问题语句的一个重要依据}}

### explain命令 [ ](mysql_20200927095114648)
+ 语法：{{c1:: `explain  select * from tb_item where title = '阿尔卡特 (OT-979) 冰川白 联通3G手机3';` }}
+ 各字段含义：
  | 字段          | 含义                                                         |
  | ------------- | ------------------------------------------------------------ |
  | id            | {{c1:: select查询的序列号，是一组数字，表示的是查询中执行select子句或者是操作表的顺序。 }}|
  | select_type   | {{c1:: 表示 SELECT 的类型，常见的取值有 SIMPLE（简单表，即不使用表连接或者子查询）、PRIMARY（主查询，即外层的查询）、UNION（UNION 中的第二个或者后面的查询语句）、SUBQUERY（子查询中的第一个 SELECT）等 }}|
  | table         | {{c1:: 输出结果集的表                                               }}|
  | type          | {{c1:: 表示表的连接类型，性能由好到差的连接类型为( system  --->  const  ----->  eq_ref  ------>  ref  ------->  ref_or_null---->  index_merge  --->  index_subquery  ----->  range  ----->  index  ------> all ) }} |
  | possible_keys | {{c1:: 表示查询时，可能使用的索引                                   }}|
  | key           | {{c1:: 表示实际使用的索引                                          }} |
  | key_len       | {{c1:: 索引字段的长度                                              }} |
  | rows          | {{c1:: 扫描行的数量                                                }} |
  | extra         | {{c1:: 执行情况的说明和描述                                        }} |


###  explain命令：id列 [ ](mysql_20200927095114650)

+ 作用：{{c1:: 表示的是查询中执行select子句或者是操作表的**顺序** }}
+ id 情况有三种 ：
  1. {{c1:: id 相同表示加载表的顺序是从上到下。 }}
  2. {{c1:: id 不同id值越大，优先级越高，越先被执行。  }}
  3. {{c1:: 以上2种情况同时存在，id相同的可以认为是一组，从上往下顺序执行；在所有的组中，id的值越大，优先级越高，越先执行。 }}

###  explain命令：select_type列 [ ](mysql_20200927095114652)

+ 常见取值
  | select_type  | 含义                                                         |
  | ------------ | ------------------------------------------------------------ |
  | SIMPLE       | {{c1:: 简单的select查询，查询中不包含子查询或者UNION               }} |
  | PRIMARY      | {{c1:: 查询中若包含任何复杂的子查询，最外层查询标记为该标识        }} |
  | SUBQUERY     | {{c1:: 在SELECT 或 WHERE 列表中包含了子查询                         }}|
  | DERIVED      | {{c1:: 在FROM 列表中包含的子查询，被标记为 DERIVED（衍生） MYSQL会递归执行这些子查询，把结果放在临时表中 }}|
  | UNION        | {{c1:: 若第二个SELECT出现在UNION之后，则标记为UNION ； 若UNION包含在FROM子句的子查询中，外层SELECT将被标记为 ： DERIVED }}|
  | UNION RESULT | {{c1:: 从UNION(`<union1,2>`)表获取结果的SELECT                                    }}|

###  explain命令：type列 [ ](mysql_20200927095114654)

+ 作用：显示访问类型
+ 常见取值：
  | type   | 含义                                                         |
  | ------ | ------------------------------------------------------------ |
  | NULL   | {{c1:: MySQL不访问任何表，索引，直接返回结果                        }}|
  | system | {{c1:: 表只有一行记录(等于系统表)，这是const类型的特例，一般不会出现 }}|
  | const  | {{c1:: 表示通过索引一次就找到了，const 用于比较primary key 或者 unique 索引。因为只匹配一行数据，所以很快。如将主键置于where列表中，MySQL 就能将该查询转换为一个常亮。const于将 "主键" 或 "唯一" 索引的所有部分与常量值进行比较 }}|
  | eq_ref | {{c1:: 类似ref，区别在于使用的是唯一索引，使用主键的关联查询，关联查询出的记录只有一条。常见于主键或唯一索引扫描 }}|
  | ref    | {{c1:: 非唯一性索引扫描，返回匹配某个单独值的所有行。本质上也是一种索引访问，返回所有匹配某个单独值的所有行（多个） }}|
  | range  | {{c1:: 只检索给定返回的行，使用一个索引来选择行。 where 之后出现 between ， < , > , in 等操作。 }}|
  | index  | {{c1:: index 与 ALL的区别为  index 类型只是遍历了索引树， 通常比ALL 快， ALL 是遍历数据文件。 }}|
  | all    | {{c1:: 将遍历全表以找到匹配的行                                     }}|

+ 建议：{{c1:: 需要保证查询至少达到 range 级别， 最好达到ref  }}

###  explain命令：extra列 [ ](mysql_20200927095114656)

| extra            | 含义                                                         |
| ---------------- | ------------------------------------------------------------ |
| `using filesort`  | {{c1:: 说明mysql会对数据使用一个外部的索引排序，而不是按照表内的索引顺序进行读取， 称为 “文件排序”, 效率低。 }}|
| `using temporary` | {{c1:: 使用了临时表保存中间结果，MySQL在对查询结果排序时使用临时表。常见于 order by 和 group by； 效率低 }}|
| `using index`     | {{c1:: 表示相应的select操作使用了覆盖索引， 避免访问表的数据行， 效率不错。 }}|

### show profile分析SQL [ ](mysql_20200927095114658)

+ 查看当前MySQL是否支持profile:{{c1:: `select @@have_profiling`}}
+ 通过set语句在Session级别开启profiling:{{c1:: `set profiling=1；`}}

+ 查看SQL语句执行的耗时：{{c1:: `show profiles `![1552489017940](https://gitee.com/xieyun714/nodeimage/raw/master/img/1552489017940.png)}}

+ 查看具体语句中每个线程的状态和消耗的时间：{{c1:: `show  profile for  query  query_id `![1552489053763](https://gitee.com/xieyun714/nodeimage/raw/master/img/1552489053763.png)}}

+ MySQL支持进一步选择all、cpu、block io 、context switch、page faults等明细类型类查看MySQL在使用什么资源上耗费了过高的时间。
  + 例：{{c1:: `show profile for cpu query_id`}}

### trace分析优化器执行计划 [ ](mysql_20200927095114660)

+ 作用： {{c1:: 查看mysql优化器，执行了哪些步骤 }}
+ 打开trace配置：
  ```SQL
    #{{c1::
    SET optimizer_trace="enabled=on",end_markers_in_json=on;
    SET optimizer_trace_max_mem_size=1000000;
    #}}
  ```
+ 执行一般的SQL语句
+ 查询优化器执行计划：{{c1:: `select * from information_schema.optimizer_trace\G;` }}

## 索引的使用 [ ](mysql_20200927095114662)

### 避免索引失效几种情况：  [ ](mysql_20200927095114664)

1. 全值匹配：{{c1:: 该情况下索引生效，执行效率比较高 }}
2. 最左前缀法则：{{c1:: 查询必须包含复合索引的最左边的列，且不跳过索引中的列。 }}
3. 注意范围查询右边的列不会走索引：
  + 例：{{c1:: `select * from tb_seller where name='小米科技' and status > '1' and address ='北京市'`}}
  + 其中address不会走索引
4. 索引列上进行运算操作:{{c1:: 索引将失效。}}
   +  例：{{c1:: `select * from tb_seller where substring(name,3,2)='科技'`}}
5. 字符串不加单引号：{{c1:: 索引失效 }}
6. 用`or`分割开的条件：{{c1:: 如果or前的条件中的列有索引，而后面的列中没有索引，那么涉及的索引**都不会**被用到。}}
7. 以`%`开头的`Like`模糊查询：索引失效
   - 注意：{{c1:: 以%结尾，会走索引。}}
   - 解决方案：{{c1:: 通过在select中覆盖索引解决，覆盖索引代表select后面全部都要是索引字段}}
8. MySQL评估使用索引比全表更慢，则不使用索引。
   - 例：{{c1:: `select * from tb_seller where address = '北京市'` }}
   - 发生背景：{{c1:: 表中匹配的记录占很总数的很大一部分。 }}
9. `is  NULL` ，`is NOT NULL`**有时**索引失效。 
   1. 发生背景：{{c1:: 与上一条类似，单种情况的记录如果占大多数则不走索引。 }}
10. `in`与`not in` :{{c1:: in 走索引， not in 索引失效。 }}

### 单列索引与复合索引的选择 [ ](mysql_20200927095114666)

+ 创建复合索引 ：`create index idx_name_sta_address on tb_seller(name, status, address);` 
  + 就相当于创建了三个索引 ： 
    1.  {{c1:: name }}
    2.  {{c1:: name + status }}
    3.  {{c1:: name + status + address }}
+ 创建单列索引 :
  ```sql
  create index idx_seller_name on tb_seller(name);
  create index idx_seller_status on tb_seller(status);
  create index idx_seller_address on tb_seller(address);
  ```
  + {{c1:: 数据库会选择一个最优的索引（辨识度最高索引）来使用，并不会使用全部索引  }}

## SQL优化 [ ](mysql_20200927095114668)

### SQL优化:当使用load 命令导入数据的时候，适当的设置可以提高导入的效率 [ ](mysql_20200927095114670)

+ 主键顺序插入: {{c1:: 导入文件行以主键顺序排序 }}
+ 关闭唯一性校验: {{c1:: `SET UNIQUE_CHECKS=0` }}
+ 关闭自动提交事务： {{c1:: `SET AUTOCOMMIT=0` }}

### SQL优化:insert语句 [ ](mysql_20200927095114672)

+ 同时对一张表插入很多行数据时，使用多值插入:
  ```sql
    #{{c1::
    insert into tb_test values(1,'Tom'),(2,'Cat')，(3,'Jerry');
    #}}
  ```
+ 在事务中进行数据插入:
  ```sql
    #{{c1::
    start transaction;
    insert into tb_test values(1,'Tom');
    insert into tb_test values(2,'Cat');
    insert into tb_test values(3,'Jerry');
    commit;
    #}}
  ```
+ 数据有序插入:
  ```sql
    #{{c1::
    insert into tb_test values(1,'Tom');
    insert into tb_test values(2,'Cat');
    insert into tb_test values(3,'Jerry');
    insert into tb_test values(4,'Tim');
    insert into tb_test values(5,'Rose');
    #}}
  ```

### 优化order by语句 [ ](mysql_20200927095114674)

+ 两种排序方式：
  + **filesort** ：{{c1:: 所有不是通过索引直接返回排序结果的排序都叫 FileSort 排序。 }}
  +  **using index**：{{c1:: 通过有序索引顺序扫描直接返回有序数据 }}
+ 出现`filesort`主要原因：{{c1:: 本质上**覆盖索引**问题，即select后的字段需要是索引字段 }}
+ 注意点：
  + 尽量减少额外的排序: {{c1:: 通过索引直接返回有序数据。 }}
  + `Order by` 的顺序: {{c1:: 和索引顺序相同 }}
  + 多个`Order by` 的字段: {{c1:: 都是升序，或者都是降序 }}

### 优化order by语句：`Filesort`的优化 [ ](mysql_20200927095114676)

  + 两种`Filesort`排序算法：
    1. 两次扫描算法：{{c1:: 可能会导致大量随机I/O操作。 }}
    2. 一次扫描算法：{{c1:: 排序时内存开销较大，但是排序效率比两次扫描算法要高。 }}
  + `max_length_for_sort_data`,`sort_buffer_size`变量
    + {{c1:: MySQL 通过比较系统变量 max_length_for_sort_data 的大小和Query语句取出的字段总大小， 来判定是否那种排序算法。 }}

### 优化group by 语句 [ ](mysql_20200927095114678)

+ 执行`order by null`禁止排序:{{c1:: `explain select age,count(*) from emp group by age order by null;` }}
+ 索引：{{c1:: 在索引字段上`group by` }}

###  优化嵌套查询 [ ](mysql_20200927095114680)

+ 优化思路：{{c1:: 如果需要嵌套查询的任务能够被替换成连接查询，那么就使用**连接查询** }}
+ 示例: `explain select * from t_user where id in (select user_id from user_role );`
+ 优化后 :`explain select * from t_user u , user_role ur where u.id = ur.user_id;`

###  优化OR条件 [ ](mysql_20200928050450126)

+ 优化原因：{{c1:: 使用union替换or解决索引失效的问题。 }}
+ 例子：
  + 优化前：{{c1:: `explain select * from emp where id = 1 or id = 10`}}
  + 优化后：{{c1:: `explain select * from emp where id = 1 union select * from emp id =10`}}

### 优化分页（limit)查询 [ ](mysql_20200928050450129)

+ 问题： `limit 2000000,10`,此时需要MySQL**排序**前`2000010`记录，仅仅返回`2000000 - 2000010 `的记录
+ 思路一：{{c1:: 覆盖索引，在索引上完成排序分页操作，最后根据主键关联回原表查询所需要的其他列内容。 }}
  + 例：{{c1:: `explain select * from tb_item t,(select id from tb_item order by id limit 2000000,10 a) where t.id = a.id` }}
+ 思路二： {{c1:: 把Limit 查询转换成某个位置的查询 }}
  + 例：{{c1:: `explain select * from tb_item where id > 100000 limit 10` }}
  + 必要条件： {{c1:: 比思路一效率高,适用与主键自增的表，且不能出现记录断层 }}

### 使用SQL提示 [ ](mysql_20200928050450131)

+ `USE INDEX`
  + 作用：{{c1:: 提供希望MySQL去参考的索引列表，就可以让MySQL不再考虑其他可用的索引 }}
  + 语法：{{c1:: `explain select * from tb_seller use index(idx_seller_name) where name = '小米科技';`}}
+ `IGNORE INDEX`
  + 作用：{{c1:: 让MySQL忽略一个或者多个索引 }}
  + 语法：{{c1:: `explain select * from tb_seller ignore index(idx_seller_name) where name = '小米科技';`}}
+ `FORCE INDEX`
  + 作用：{{c1:: 强制MySQL使用一个特定的索引 }}
  + 语法：{{c1:: `explain select * from tb_seller force index(idx_seller_name) where name = '小米科技';`}}

### MYSQL应用层的几种优化 [ ](mysql_20200928050450132)

  + 使用数据库连接池
  + 减少对MYSQL的访问
    1. {{c1:: 能一次取出全部数据就尽量不要两次取。 }}
    2. {{c1:: 增加cache层，如（Mybatis一级缓存，redis数据库缓存）}}
  + 负载均衡 
    1. {{c1:: 通过MySQL的主从复制，实现读写分离 }}
    2. {{c1:: 采用分布式数据库架构 }}

## MYSQL查询缓存 [ ](mysql_20200928050450134)

###  MYSQL查询缓存配置 [ ](mysql_20200928050450136)

1. 查看当前的MySQL数据库是否支持查询缓存：{{c1:: `SHOW VARIABLES LIKE 'have_query_cache'; `}}
2. 查看当前MySQL是否开启了查询缓存 ：{{c1:: `SHOW VARIABLES LIKE 'query_cache_type';`}}
3. 查看查询缓存的占用大小 ：{{c1:: `SHOW VARIABLES LIKE 'query_cache_size';`}}
4. 查看查询缓存的状态变量：{{c1:: `SHOW STATUS LIKE 'Qcache%';`}}
   + 各个变量的含义如下：
   | 参数                    | 含义                                                         |
   | ----------------------- | ------------------------------------------------------------ |
   | Qcache_free_blocks      | {{c1:: 查询缓存中的可用内存块数                                     }}|
   | Qcache_free_memory      | {{c1:: 查询缓存的可用内存量                                         }}|
   | Qcache_hits             | {{c1:: 查询缓存命中数                                               }}|
   | Qcache_inserts          | {{c1:: 添加到查询缓存的查询数                                       }}|
   | Qcache_lowmen_prunes    | {{c1:: 由于内存不足而从查询缓存中删除的查询数                       }}|
   | Qcache_not_cached       | {{c1:: 非缓存查询的数量（由于 query_cache_type 设置而无法缓存或未缓存） }}|
   | Qcache_queries_in_cache | {{c1:: 查询缓存中注册的查询数                                       }}|
   | Qcache_total_blocks     | {{c1:: 查询缓存中的块总数                                           }}|

### 查询缓存 [ ](mysql_20200928050450138)

+ 打开功能参数配置：{{c1:: `query_cache_type` }}
+ 参数配置各取值含义：
  | 值          | 含义                                                         |
  | ----------- | ------------------------------------------------------------ |
  | `OFF` 或 `0`    | {{c1:: 查询缓存功能关闭                                             }}|
  | `ON` 或 `1`     | {{c1:: 查询缓存功能打开，SELECT的结果符合缓存条件即会缓存，否则，不予缓存，显式指定 SQL_NO_CACHE，不予缓存 }}|
  | `DEMAND` 或 `2` | {{c1:: **按需缓存**，显式指定 `SQL_CACHE` 的`SELECT`语句才会缓存,其它均不予缓存 }}|
+ 按需缓存例子：
  ```Sql
    #{{c1::
    SELECT SQL_CACHE id, name FROM customer;
    SELECT SQL_NO_CACHE id, name FROM customer;
    #}}
  ```


### MYSQL查询缓存失效的情况 [ ](mysql_20200928050450142)

1. SQL语句不一致的情况
  + SQL1 : {{c1:: `select count(*) from tb_item;` }}
  + SQL2 : {{c1:: `Select count(*) from tb_item;` }}
2. 当查询语句中有一些不确定的时,如 ： {{c1:: `now() , current_date() , curdate() , curtime() , rand() , uuid() , user() , database()` }}
3. 不使用任何表查询语句:{{c1:: `select 'A';` }}
4. 查询下列数据库中的表时，不会走查询缓存。
  + {{c1:: `mysql` }}
  + {{c1:: `information_schema` }}
  + {{c1:: `performance_schema`  }}
5. 在存储的{{c1:: **函数**，**触发器**或**事件的主体** }}内执行的查询。
6. 如果表更改，{{c1:: 插入一条数据，或者修改一条数据，该表对应所有的查询缓存皆失效 }}

## Mysql内存管理及优化 [ ](mysql_20200929055547636)

###  Mysql内存优化原则 [ ](mysql_20200929055547637)

1.  将尽量多的内存分配给MySQL做缓存:{{c1:: ，但要给操作系统和其他程序预留足够内存。 }}
2.  MyISAM 存储引擎的数据文件读取依赖于操作系统自身的IO缓存:{{c1:: ，因此，如果有MyISAM表，就要预留更多的内存给操作系统做IO缓存。 }}
3.  排序区、连接区等:{{c1:: 缓存是分配给每个数据库会话（session）专用的，其默认值的设置要根据最大连接数合理分配，如果设置太大，不但浪费资源，而且在并发连接较高时会导致物理内存耗尽。 }}

### MyISAM 内存优化参数配置 [ ](mysql_20200929055547639)
+ 优化背景:
  + 索引块:{{c1:: myisam存储引擎使用 key_buffer 缓存索引块，加速myisam索引的读写速度。 }}
  + 数据块:{{c1:: 对于myisam表的数据块，mysql没有特别的缓存机制，完全依赖于操作系统的IO缓存。}}
+ `/usr/my.cnf`配置
  + `key_buffer_size`
    + 作用：{{c1:: key_buffer_size决定MyISAM索引块缓存区的大小，直接影响到MyISAM表的存取效率。可以在MySQL参数文件中设置key_buffer_size的值，对于一般MyISAM数据库，建议至少将1/4可用内存分配给key_buffer_size。 }}
  + `read_buffer_size`
    + 作用：{{c1:: 如果需要经常顺序扫描myisam表，可以通过增大read_buffer_size的值来改善性能。但需要注意的是read_buffer_size是每个session独占的，如果默认值设置太大，就会造成内存浪费。 }}
  + `read_rnd_buffer_size`
    + 作用：{{c1:: 对于需要做排序的myisam表的查询，如带有order by子句的sql，适当增加 read_rnd_buffer_size 的值，可以改善此类的sql性能。但需要注意的是 read_rnd_buffer_size 是每个session独占的，如果默认值设置太大，就会造成内存浪费。 }}

### InnoDB 内存优化参数配置 [ ](mysql_20200929055547641)

+ 优化背景:{{c1:: innodb用一块内存区做IO缓存池，该缓存池不仅用来缓存innodb的索引块，而且也用来缓存innodb的数据块。 }}
+ `innodb_buffer_pool_size`:{{c1:: 该变量决定了 innodb 存储引擎表数据和索引数据的最大缓存区大小。 }}
+ `innodb_log_buffer_size`:{{c1:: 决定了innodb重做日志缓存的大小 }}

### Mysql并发参数调整 [	](mysql_20201012060626276)

+ `max_connections`:
  + 作用：{{c1:: 控制允许连接到MySQL数据库的最大数量，默认值是 151。}}
  + 使用背景：{{c1:: 如果状态变量 connection_errors_max_connections 不为零，并且一直增长，则说明不断有连接请求因数据库连接数已达到允许最大值而失败，这是可以考虑增大max_connections 的值。}}
  + 注意:{{c1:: 取决于很多因素，包括给定操作系统平台的线程库的质量、内存大小、每个连接的负荷、CPU的处理速度，期望的响应时间等。}}
+ `back_log`:
  + 作用：{{c1:: 与`max_connections`有关联,控制**积压请求栈大小**,默认值为 50,最大不超过900。}}
  + 使用背景：{{c1:: 如果需要数据库在较短的时间内处理大量连接请求， 可以考虑适当增大back_log 的值}}
+ `table_open_cache`:
  + 作用：{{c1:: 该参数用来控制所有SQL语句执行线程总共可打开表缓存的数量}}
  + 使用背景：{{c1:: 该参数的值应该根据设置的最大连接数 max_connections 以及每个连接执行关联查询中涉及的**表的最大数量**来设定`max_connections x N ；`}}
+  `thread_cache_size`
  + 作用：{{c1:: 控制 MySQL server中为客户端服务线程的数量。}}
+ `innodb_lock_wait_timeout`
  + 作用：{{c1:: 设置InnoDB 事务等待行锁的时间,默认值是50ms }}

## Mysql锁 [	](mysql_20201012060626279)

### MYSQL锁分类 [	](mysql_20201012060626281)
+ 从对数据操作的粒度分 ： 
  1. {{c1:: 表锁：操作时，会锁定整个表。}}
  2. {{c1:: 行锁：操作时，会锁定当前操作行。}}
+ 从对数据操作的类型分：
  1. {{c1:: 读锁（共享锁）：针对同一份数据，多个读操作可以同时进行而不会互相影响。}}
  2. {{c1:: 写锁（排它锁）：当前操作没有完成之前，它会阻断其他写锁和读锁。}}

###  如何加MyISAM表锁 [	](mysql_20201012060626283)
+ 应用背景：{{c1:: MyISAM 在执行查询语句（SELECT）前，会自动给涉及的所有表加读锁，在执行更新操作（UPDATE、DELETE、INSERT 等）前，会自动给涉及的表加写锁，这个过程并不需要用户干预，因此，用户一般不需要直接用 LOCK TABLE 命令给 MyISAM 表显式加锁。 }}
+ 显式加读锁：{{c1:: `lock table table_name read;` }}
+ 显式加写锁：{{c1:: `lock table table_name write；` }}

### 查看表锁的争用情况 [	](mysql_20201012060626285)
+ `show open tables`；
  + `In_user` : {{c1:: 表当前被查询使用的次数。如果该数为零，则表是打开的，但是当前没有被使用。 }}
  + `Name_locked`：{{c1:: 表名称是否被锁定。名称锁定用于取消表或对表进行重命名等操作。 }}
+ `show status like 'Table_locks%'`;
  + `Table_locks_immediate` ： {{c1:: 指的是能够立即获得表级锁的次数，每立即获取锁，值加1。 }}
  + `Table_locks_waited` ： {{c1:: 指的是不能立即获取表级锁而需要等待的次数，每等待一次，该值加1，此值高说明存在着较为严重的表级锁争用情况。 }}

  

### 并发事务处理带来的问题 [	](mysql_20201012060626287)

+ | 问题                               | 含义                                                         |
  | ---------------------------------- | ------------------------------------------------------------ |
  | 丢失更新（Lost Update）            | {{c1:: 当两个或多个事务选择同一行，最初的事务修改的值，会被后面的事务修改的值覆盖。 }}|
  | 脏读（Dirty Reads）                | {{c1:: 当一个事务正在访问数据，并且对数据进行了修改，而这种修改还没有提交到数据库中，这时，另外一个事务也访问这个数据，然后使用了这个数据。 }}|
  | 不可重复读（Non-Repeatable Reads） | {{c1:: 一个事务在读取某些数据后的某个时间，再次读取以前读过的数据，却发现和以前读出的数据不一致。 }}|
  | 幻读（Phantom Reads）              | {{c1:: 一个事务按照相同的查询条件重新读取以前查询过的数据，却发现其他事务插入了满足其查询条件的新数据。 }}|
+ 简单总结：脏读是不可容忍的，不可重复读和虚读在一定的情况下是可以的【做统计的肯定就不行】。

### 事务隔离级别 [	](mysql_20201012060626289)
+ 作用：为了解决事务并发问题
+ 4种事务隔离级别
  1. `Read Uncommitted`：{{c1::（未提交读）事务中的修改，即使没有提交，其他事务也可以看得到，会导致“脏读”、“幻读”和“不可重复读取”。 }}
  2. `Read Committed`：{{c1::（提交读）默认事务等级，保证一个事务**不会**读到另一个并行事务**已修改但未提交的数据**，避免了“脏读取”，但不能避免“幻读”和“不可重复读取”。该级别适用于大多数系统。 }}
  3. `Repeatable Read`：{{c1::（重复读）保证了一个事务**不会**修改已经由另一个事务**读取但未提交（回滚）的数据**。避免了“脏读取”和“不可重复读取”的情况，但不能避免“幻读”，但是带来了更多的性能损失。 }}
  4. `Serializable`：{{c1::（串行化）最严格的级别，事务串行执行，资源消耗最大； }}
+ 查看当前隔离级别变量：{{c1:: `show variables like 'tx_isolation';` }}

### InnoDB 的行锁模式 [	](mysql_20201012060626291)
+ 对于UPDATE、DELETE和INSERT语句：{{c1:: InnoDB会自动给涉及数据集加排他锁（X)； }}
+ 对于普通SELECT语句：{{c1:: InnoDB不会加任何锁； }}
+ 显式加锁语法：
  + 共享锁（S）：{{c1:: `SELECT * FROM table_name WHERE ... LOCK IN SHARE MODE` }}
  + 排他锁（X) ：{{c1:: `SELECT * FROM table_name WHERE ... FOR UPDATE` }}
+ 无索引行锁升级为表锁sql例:{{c1:: `update test_innodb_lock set sex='2' where name = 400` }}
+ 注意间隙锁问题：{{c1:: `update test_innodb_lock set sex='2' where id < 100` }}

### 查询InnoDB 行锁争用情况 [	](mysql_20201012060626293)

+ 命令：`show status like 'innodb_row_lock%';`
  + `Innodb_row_lock_current_waits`:{{c1:: 当前正在等待锁定的数量 }}
  + `Innodb_row_lock_time`:{{c1:: 从系统启动到现在锁定总时间长度 }}
  + `Innodb_row_lock_time_avg`:{{c1:: 每次等待所花平均时长 }}
  + `Innodb_row_lock_time_max`:{{c1:: 从系统启动到现在等待最长的一次所花的时间 }}
  + `Innodb_row_lock_waits`:{{c1:: 系统启动后到现在总共等待的次数 }}

## 常用SQL技巧 [	](mysql_20201012060626294)

### SQL编写顺序 [	](mysql_20201012060626296)

1. {{c1:: `SELECT DISTINCT <select list>` }}
1. {{c1:: `FROM <left_table> <join_type>` }}
1. {{c1:: `JOIN <right_table> ON <join_condition>` }}
1. {{c1:: `WHERE <where_condition>` }}
1. {{c1:: `GROUP BY <group_by_list>` }}
1. {{c1:: `HAVING <having_condition>` }}
1. {{c1:: `ORDER BY <order_by_condition>` }}
1. {{c1:: `LIMIT <limit_params>` }}

### SQL执行顺序 [	](mysql_20201012060626298)

1. {{c1:: `FROM <left_table>`}}
1. {{c1:: `ON   <join_condition>`}}
1. {{c1:: `<join_type>  JOIN <right_table>`}}
1. {{c1:: `WHERE  <where_condition>`}}
1. {{c1:: `GROUP BY  <group_by_list>`}}
1. {{c1:: `HAVING  <having_condition>`}}
1. {{c1:: `SELECT DISTINCT  <select list>`}}
1. {{c1:: `ORDER BY <order_by_condition>`}}
1. {{c1:: `LIMIT  <limit_params>`}}

### Use Regular Expression in SQL [	](mysql_20201012060626300)

+ 语法：{{c1:: `select * from emp where name regexp '[uvw]';` }}

## mysql常用工具 [	](mysql_20201012060626302)

### mysql的客户端工具 [	](mysql_20201012060626304)

+ 执行选项: {{c1:: `mysql -uroot -p2143 db01 -e "select * from tb_book";` }}

### mysqladmin [	](mysql_20201012060626306)

+ 作用：{{c1:: 个执行管理操作的客户端程序。可以用它来检查服务器的配置和当前状态、创建并删除数据库等。 }}
  + 查看帮助文档：{{c1:: `mysqladmin --help` }}
  + 例子:
    +  `mysqladmin -uroot -p2143 create 'test01';` 
    +  `mysqladmin -uroot -p2143 drop 'test01';` 
    +  `mysqladmin -uroot -p2143 version;` 

### mysqlbinlog [	](mysql_20201012060626308)

+ 作用：查看服务器生成的二进制日志文件
  + 语法 ：`mysqlbinlog [options]  log-files1 log-files2 ...`
  + 选项：
   + `-d, --database=name` : {{c1:: 指定数据库名称，只列出指定的数据库相关操作。 }}
   + `-o, --offset=#` : {{c1:: 忽略掉日志中的前n行命令。 }}
   + `-r,--result-file=name` : {{c1:: 将输出的文本格式日志输出到指定文件。 }}
   + `-s, --short-form` : {{c1:: 显示简单格式， 省略掉一些信息。 }}
   + `--start-datatime=date1  --stop-datetime=date2` : {{c1:: 指定日期间隔内的所有日 志。}}
   + `--start-position=pos1 --stop-position=pos2` : {{c1:: 指定位置间隔内的所有日志。 }}

### mysqldump [ ](mysql_20200914055153039)

+ 作用：{{c1:: 导出数据库的.sql文件备份 }}
+ 备份语法：{{c1:: `mysqldump.exe -h -P -u -p [备份选项] 数据库名字 [数据表列表] > SQL文件路径` }}
+ 备份选项:
  + 全库备份：{{c1:: `--all-databases` 所有数据库的所有表，也不需要指定数据库名字 }}
  + 单库备份：{{c1:: `[--databases] 数据库` 指定数据库里的所有表（后面不要给表名） }}
  + 部分表（单表）备份：{{c1:: `数据库名字 表1[ 表2...表N]` }}
+ 输出内容选项:
 + `--add-drop-database`:{{c1:: 在每个数据库创建语句前加上 Drop database 语句}}
 + `--add-drop-table`:{{c1:: 在每个表创建语句前加上 Drop table 语句 , 默认开启 ; 不开启(--skip-add-drop-table)}}
 + `-n, --no-create-db`:{{c1:: 不包含数据库的创建语句}}
 + `-t, --no-create-info`:{{c1:: 不包含数据表的创建语句}}
 + `-d --no-data`:{{c1:: 不包含数据}}
 + `-T, --tab=name`:{{c1:: 自动生成两个文件,.sql定义文件与.txt数据文件}}
  + 例：{{c1:: `mysqldump -uroot -p2143 -T /tmp test city` }}
+ 备份数据导入
  + 导入txt备份文件语法:{{c1:: `mysqlimport -uroot -p2143 dbname /tmp/city.txt` }}
  + 导入sql备份文件语法:{{c1:: `source /root/tb_book.sql` }}

### mysqlshow [	](mysql_20201012060626310)
+ 作用：{{c1:: 可以让我们在不连接到MySQL客户端的情况下查看MySQL的一些参数、数据库、表、列、索引等信息 }}
+ 选项
  + `--count`:{{c1:: 显示数据库及表的统计信息（数据库，表 均可以不指定） }}
  + `-i`:{{c1:: 显示指定数据库或者指定表的状态信息 }}
+ 例子:
  + 查询每个数据库的表的数量及表中记录的数量:{{c1::`mysqlshow -uroot -p2143 --count` }}
  + 查询test库中每个表中的字段书，及行数:{{c1::`mysqlshow -uroot -p2143 test --count` }}
  + 查询test库中book表的详细情况:{{c1::`mysqlshow -uroot -p2143 test book --count` }}

## MYSQL中4 种不同的日志 [	](mysql_20201012060626312)

### mysql错误日志 [	](mysql_20201012060626314)
+ 作用：{{c1:: 它记录了当 mysqld 启动和停止时，以及服务器在运行过程中发生任何严重错误时的相关信息。当数据库出现任何故障导致无法正常使用时，可以首先查看此日志。 }}
+ 查看错误日志位置：{{c1:: `show variables like 'log_error%';` }}

### 二进制日志（BINLOG 日志） [	](mysql_20201012060626316)
+ 作用：记录了所有的 DDL（数据定义语言）语句和 DML（数据操纵语言）语句，但是不包括**数据查询语句**，主从复制，就是通过该binlog实现，默认情况下是没有开启的
+ 配置文件位置 : /usr/my.cnf
  + 开启日志：`log_bin=mysqlbin`
  + 配置日志格式：`binlog_format=STATEMENT`
+ 日志格式
  + **STATEMENT**:{{c1:: 记录的都是SQL语句 }}
  + **ROW**:{{c1:: 记录的是每一行的数据变更 }}
  + **MIXED**:{{c1:: 混合了STATEMENT 和 ROW两种格式,默认情况下采用STATEMENT，但是在一些特殊情况下采用ROW来进行记录。 }}
+ 查看日志:`mysqlbinlog log-file；`
+ 查看ROW格式日志:`mysqlbinlog -vv mysqlbin.000002`

###  二进制日志的删除 [	](mysql_20201012060626318)
+ 整体删除:{{c1:: `Reset Master` }}
+ 删除指定序号前的日志:{{c1:: `purge  master logs to 'mysqlbin.******` }}
+ 删除指定日期前的日志:{{c1:: `purge master logs before 'yyyy-mm-dd hh24:mi:ss'` }}
+ 指定日志过期天数:{{c1:: 设置参数`expire_logs_days=#`  }}

### 查询日志 [	](mysql_20201012060626320)
+ 作用：{{c1:: 记录了客户端的所有操作语句，而二进制日志不包含查询数据的SQL语句。 }}
+ 开启查询日志配置参数
  + 开启查询日志:{{c1:: `general_log=1` }}
  + 设置日志的文件名:{{c1:: `general_log_file=file_name` }}

### 慢查询日志 [	](mysql_20201012060626322)

+ 慢查询日志配置参数
  + 该参数用来控制慢查询日志是否开启:{{c1:: `slow_query_log=1` }}
  + 该参数用来指定慢查询日志的文件名:{{c1:: `slow_query_log_file=slow_query.log` }}
  + 该选项用来配置查询的时间限制,默认10s:{{c1:: `long_query_time=10` }}
+ 查看日志：
  + `cat slow_query.log`
  + `mysqldumpslow slow_query.log` :{{c1:: 对慢查询日志进行分类汇总。 }}

## Mysql复制 [	](mysql_20201014033126191)

### MYSQL主从复制:master数据库搭建 [	](mysql_20201014033126193)

1. 在master 的配置文件（/usr/my.cnf）中，配置如下内容：
  + `server-id=1`:{{c1:: mysql 服务ID,保证整个集群环境中唯一 }}
  + `log-bin=/var/lib/mysql/mysqlbin`:{{c1:: mysql binlog 日志的存储路径和文件名 }}
  + `read-only=0`:{{c1:: 是否只读,1 代表只读, 0 代表读写 }}
  + `binlog-ignore-db=mysql`:{{c1:: 忽略的数据, 指不需要同步的数据库 }}
2. `service mysql restart;`:{{c1:: 执行完毕之后，需要重启Mysql }}
3. 创建同步数据的账户，并且进行授权操作:
  + `grant replication slave on *.* to 'itcast'@'192.168.192.131' identified by 'itcast';`
  + `flush privileges;`
4. 查看master状态:`show master status;`
  + 字段含义：
    + `File` :{{c1:: 从哪个日志文件开始推送日志文件  }}
    + `Position` ：{{c1:: 从哪个位置开始推送日志 }}
    + `Binlog_Ignore_DB` :{{c1:: 指定不需要同步的数据库 }}

### MYSQL主从复制:slave数据库搭建 [	](mysql_20201014033126195)

1. 在 slave 端配置文件中，配置如下内容
  + `server-id=2`:{{c1:: mysql服务端ID,唯一 }}
  + `log-bin=/var/lib/mysql/mysqlbin`:{{c1:: 指定binlog日志 }}
2. 重启Mysql:`service mysql rest;`
3. 指定主数据库：
    + `change master to master_host= '192.168.192.130', master_user='itcast', master_password='itcast', master_log_file='mysqlbin.000001', master_log_pos=413;`
4. 开启同步操作
  + `start slave;`
  + `show slave status;`
