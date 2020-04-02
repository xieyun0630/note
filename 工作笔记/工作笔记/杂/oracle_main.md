# PL/SQL

## 本部分笔记的总体结构

![1567060680733](oracle_main.assets/1567060680733.png)

## pl/sql的基本的语法结构

### 使用PL/SQL查询一个表的单个记录的多个字段。

```plsql
declare
  --声明多个变量
  v_member_no f_private_inf.member_no%TYPE;
  v_login_id f_private_inf.login_id%TYPE;
  v_password f_private_inf.password%TYPE;
begin
  --通过 select ... into ... 语句为变量赋值
 select member_no, login_id, password   INTO v_member_no, v_login_id, v_password
 from f_private_inf
 where MEMBER_NO = 17;
 -- 打印多个变量的值
 dbms_output.put_line(v_member_no||'::'||v_login_id||'::'||v_password);
end;
```

## 记录类型

### 使用PL/SQL查询一个表的单个记录的多个字段,将多个字段封装成记录类型。

```plsql
DECLARE
TYPE member_type IS RECORD(
  v_member_no f_private_inf.member_no%TYPE,
  v_login_id f_private_inf.login_id%TYPE,
  v_password f_private_inf.password%TYPE
);
v_member_type member_type;
BEGIN
   --通过 select ... into ... 语句为变量赋值
 select member_no, login_id, password   INTO v_member_type
 from f_private_inf
 where MEMBER_NO = 17;
 -- 打印多个变量的值
 dbms_output.put_line(v_member_type.v_member_no||'::'||v_member_type.v_login_id||'::'||v_member_type.v_password);
END;
```

### 查询出一个表中的某个字段并使用记录类型打印到控制台

```plsql
DECLARE
v_member_type f_private_inf%ROWTYPE;
BEGIN
   --通过 select ... into ... 语句为变量赋值
 select * INTO v_member_type
 from f_private_inf
 where MEMBER_NO = 17;
 -- 打印多个变量的值
 dbms_output.put_line(v_member_type.member_no||'::'||v_member_type.login_id||'::'||v_member_type.password);
END;

```

## 流程控制

### 条件判断

```plsql
/*
if的使用
问题：查询出某个member的memberNo，
		memberNo大于200 输出 “memberNo>200”
		memberNo大于100 输出 “200>memberNo>100”
		memberNo小于100 输出 “100>memberNo”
		注意：ELSIF 不是 else if/elseif
*/
DECLARE
v_member_no f_private_inf.member_no%type;
v_temp VARCHAR2(20);
BEGIN
	SELECT f.member_no into v_member_no 
  	FROM f_private_inf f 
 	WHERE LOGIN_ID ='TESTFENG00';
	IF v_member_no >= 200 THEN v_temp:='memberNo>200';
	ELSIF v_member_no >= 100 THEN v_temp:='200>memberNo>100';
	ELSE v_temp:='memberNo<100';
 	END IF;
  	dbms_output.put_line(v_member_no||':'||v_temp);
END;
/*
case的使用
问题：查询出某个member的status_kbn，
	 打印出自然语言解释对应的几种状态。
*/
DECLARE
v_status_kbn f_private_inf.member_no%type;
v_temp VARCHAR2(20);
BEGIN
  SELECT f.status_kbn into v_status_kbn
  FROM f_private_inf f 
  WHERE LOGIN_ID ='TESTFENG00';
  
  v_temp:=CASE v_status_kbn WHEN 0 THEN 'logined'
               WHEN 1 THEN 'not loggin'
               WHEN 2 THEN  'forbid'
          END;

  dbms_output.put_line(v_temp);
END;
```

### 循环控制

```plsql
/*
问题：输出1到100的整数到控制台。
*/
--方式一
DECLARE
v_i NUMBER(5):=1;
BEGIN
  LOOP
    dbms_output.put_line(v_i);
  EXIT WHEN v_i>=100;
  v_i:= v_i + 1;
  END LOOP;
END;

--方式二
DECLARE
v_i NUMBER(5):=1;
BEGIN
	while v_i<=100 loop
	dbms_output.put_line(v_i);
	v_i:= v_i + 1;
	end loop;
END;

--方式三
BEGIN
   FOR c IN 1..100 LOOP
     dbms_output.put_line(c);
   END LOOP;
END;
```

### 流程控制综合使用

while版：![1567134776621](oracle_main.assets/1567134776621.png)

for版：![1567134868520](oracle_main.assets/1567134868520.png)

优化：![1567134957753](oracle_main.assets/1567134957753.png)

break功能：

![1567135064116](oracle_main.assets/1567135064116.png)

continure功能：

![1567135159022](oracle_main.assets/1567135159022.png)

## 游标的使用

### 简单使用游标

```plsql
/*
使用游标打印出所有的用户的loginid 与 password
*/
DECLARE
v_login_id f_private_inf.login_id%TYPE;
password f_private_inf.password%TYPE;
--1. 定义游标
CURSOR member_inf_cursor IS SELECT login_id,password FROM f_private_inf;
BEGIN
--2. 打开游标
  OPEN member_inf_cursor;
--3. 提取游标
  FETCH member_inf_cursor INTO v_login_id,password;
 --4. 对游标进行循环操作: 判断游标中是否有下一条记录
  WHILE member_inf_cursor%FOUND LOOP
    dbms_output.put_line(v_login_id||'::'||password);
    FETCH member_inf_cursor INTO v_login_id,password;
  END LOOP;
 --5. 关闭游标
  CLOSE  salary_cursor;
END;
```
### 将游标与记录类型混合使用

```plsql
/*
将游标与记录类型混合使用，打印出f_private_inf的数据。
*/
DECLARE
member_record f_private_inf%ROWTYPE;
CURSOR member_inf_cursor IS SELECT * FROM f_private_inf;
BEGIN
  OPEN member_inf_cursor;
  FETCH member_inf_cursor INTO member_record;
  WHILE member_inf_cursor%FOUND LOOP
    dbms_output.put_line(member_record.login_id||'::'||member_record.password);
    FETCH member_inf_cursor INTO member_record;
  END LOOP;
  CLOSE  member_inf_cursor;
END;


/*
方式二
*/
DECLARE
TYPE member_record IS RECORD(
     v_login_id f_private_inf.login_id%TYPE,
     v_password f_private_inf.password%TYPE
);
v_member_record member_record;
CURSOR member_cursor IS SELECT login_id,password FROM f_private_inf;
BEGIN
       OPEN member_cursor;
       FETCH member_cursor INTO v_member_record;
       WHILE member_cursor%FOUND LOOP
     dbms_output.put_line(v_member_record.v_login_id ||':'||v_member_record.v_password);
     FETCH member_cursor INTO v_member_record;
       END LOOP;
      CLOSE member_cursor;
END;
```

### 游标的4种属性

![1567146390212](oracle_main.assets/1567146390212.png)

### 游标的for循环

```plsql
DECLARE
CURSOR member_cursor IS SELECT login_id,password FROM f_private_inf;
BEGIN
/*
	可以避免显式的打开和关闭游标。
*/
  FOR c IN member_cursor LOOP
    dbms_output.put_line(c.login_id ||':'||c.password);
  END LOOP;
END;
```

### 带参数的游标

```plsql
declare
    --定义游标
    cursor emp_sal_cursor(dept_id number, sal number) is 
           select salary + 1000 sal, employee_id id 
           from employees 
           where department_id = dept_id and salary > sal;
    --定义基数变量
    temp number(4, 2);
begin
    --处理游标的循环操作
    for c in emp_sal_cursor(sal => 4000, dept_id => 80) loop
          --判断员工的工资, 执行 update 操作
          --dbms_output.put_line(c.id || ': ' || c.sal);
          if c.sal <= 5000 then
             temp := 0.05;
          elsif c.sal <= 10000 then
             temp := 0.03;   
          elsif c.sal <= 15000 then
             temp := 0.02;
          else
             temp := 0.01;
          end if;
          dbms_output.put_line(c.sal || ': ' || c.id || ', ' || temp);
          --update employees set salary = salary * (1 + temp) where employee_id = c.id;
    end loop;
end;
```

### 隐式游标

```plsql
--隐式游标: 更新指定员工 salary(涨工资 10)，如果该员工没有找到，则打印”查无此人” 信息
begin
         update employees 
         set salary = salary + 10
         where employee_id = 1005;
         
         if sql%notfound then
            dbms_output.put_line('查无此人!');
         end if;
end;
```

## 异常处理
### 预定义的异常处理例

```plsql
/*
	预定义的异常不需要在declare部分显式定义。
*/
declare
  v_sal employees.salary%type;
begin
  select salary into v_sal
  from employees
  where employee_id >100;
  dbms_output.put_line(v_sal);
exception
  when Too_many_rows then dbms_output.put_line('输出的行数太多了');
  when others then dbms_output.put_line('出现其他类型的异常');
end;
```

### 非预定义的异常处理例

```plsql
declare
  v_sal employees.salary%type;
  --声明一个异常
  delete_mgr_excep exception;
  --把自定义的异常和oracle的错误关联起来
  PRAGMA EXCEPTION_INIT(delete_mgr_excep,-2292);
begin
  delete from employees
  where employee_id = 100;
  
  select salary into v_sal
  from employees
  where employee_id >100;
  dbms_output.put_line(v_sal);
exception
  when Too_many_rows then dbms_output.put_line('输出的行数太多了');
  when delete_mgr_excep then dbms_output.put_line('Manager不能直接被删除');
end;
```

### 自定义的异常

![1567149762290](oracle_main.assets/1567149762290.png)

## 存储函数与存储过程

### 存储函数的结构

```plsql
--函数的声明(有参数的写在小括号里)
create or replace function func_name(v_param varchar2)
	--返回值类型
	return varchar2
is 
	--PL/SQL块变量、记录类型、游标的声明(类似于前面的declare的部分)
begin
	--函数体(可以实现增删改查等操作，返回值需要return)
       return 'helloworld'|| v_logo;
end;
```

```plsql
/*
要求: 定义一个函数: 获取给定部门的工资总和 和 该部门的员工总数(定义为 OUT 类型的参数).
要求: 部门号定义为参数, 工资总额定义为返回值.
*/
create or replace function sum_sal(dept_id number, total_count out number)
       return number
       is
       
       cursor sal_cursor is select salary from employees where department_id = dept_id;
       v_sum_sal number(8) := 0;   
begin
       total_count := 0;

       for c in sal_cursor loop
           v_sum_sal := v_sum_sal + c.salary;
           total_count := total_count + 1;
       end loop;       
    
       --dbms_output.put_line('sum salary: ' || v_sum_sal);
       return v_sum_sal;
end;

执行函数:

delare 
  v_total number(3) := 0;

begin
    dbms_output.put_line(sum_sal(80, v_total));
    dbms_output.put_line(v_total);
end;

```
### 存储过程的结构

```plsql
/*
定义一个存储过程: 获取给定部门的工资总和(通过 out 参数), 要求:部门号和工资总额定义为参数
*/
create or replace procedure sum_sal_procedure(dept_id number, v_sum_sal out number)
is
cursor sal_cursor is select salary from employees where department_id = dept_id;
begin
       v_sum_sal := 0;
       for c in sal_cursor loop
           --dbms_output.put_line(c.salary);
           v_sum_sal := v_sum_sal + c.salary;
       end loop;       
       dbms_output.put_line('sum salary: ' || v_sum_sal);
end;

--[执行]
declare 
     v_sum_sal number(10) := 0;
begin
     sum_sal_procedure(80,v_sum_sal);
end;
```

## oracle里的extend详解

```plsql
--oracle里的extend详解
--扩展已知的数组空间，例：

DECLARE
      TYPE   CourseList   IS   TABLE   OF   VARCHAR2(10);
      courses   CourseList;
BEGIN
      --   初始化数组元素，大小为3
      courses   :=   CourseList( 'Biol   4412 ',   'Psyc   3112 ',   'Anth   3001 ');
      --   为数组增加一个元素，数组大小为4，末尾的元素为NULL
      courses.EXTEND;     --   append   one   null   element
      --   为增加的元素赋值，如果没用EXTEND，这里会出错
      courses(4)   :=   'Engl   2005 ';
end

/*
Oracle在逻辑上是由各个表空间(tablespace)构成的,tablespace由segments(段)构成
段是由extends构成,中文叫作区或者数据区,
区是由一个一个的数据块构成,数据块的大小由操作系统决定。
**/
```

### dual表的作用

Oracle中的dual表是一个单行单列的虚拟表，Dual表主要用来选择系统变量或求一个表达式的值。

# oracle SEQUENCE解释和用法

在Oracle中sequence就是序号，每次提取完都会自动增加，步幅固定，**它与表没有直接关系**！

1，创建序列

```
--创建序列
  

 CREATE SEQUENCE  EMP_SEQUENCE

　　INCREMENT BY 1　 -- 每次加几个

　　START WITH 1　　 -- 从1开始计数

　　NOMAXVALUE　　　 -- 不设置最大值

　　NOCYCLE　　　　　-- 一直累加，不循环

　　CACHE 10;
```

解释

INCREMENT BY：指定序列增长步长。  能够为正（升序）、负整数（降序）。但不能为0。  最高精度28。

 START WITH： 指定序列起始数。默觉得序列最小值。

 MAXVALUE ：指定序列最大值。  最大28位。  必须大于等于起始值且大于等于序列最小值。

 NOMAXVALUE：  无最大值（实际为10^27或-1）。default  

MINVALUE ：指定序列最小值。

 NOMINVALUE  ：无最小值（实际为1或-10^26）。

Default  CYCLE  ：指定序列达到最大值或最小值后继续从头開始生成。

 NOCYCLE ：不循环生成。Default.

 CACHE ：指定数据库内存中预分配的序列值个数，以便高速获取。最小cache值为2。

2、删除序列

```
DROP SEQUENCE EMP_SEQUENCE;
```

3、应用

```
INSERT INTO USER_M(USER_ID,USER_NAME,PWD,EMAIL,SCHOOL,DEPART,GRADE) VALUES(EMP_SEQUENCE.NEXTVAL,'武圣',1424424,5233255,'长江大学','体育系','2018级');
```

结果

![img](oracle_main.assets/1560697-20190103112142173-348540125.png)







## Oracle的to_char()函数使用

### **（1）用作日期转换：**

**to_char(date,'格式');**

```
select to_date('2005-01-01 ','yyyy-MM-dd') from dual;
select to_char(sysdate,'yyyy-MM-dd HH24:mi:ss') from dual;
```

### **（2）处理数字：**

**to_char(number,'格式');**

```
select to_char(88877) from dual;
select to_char(1234567890,'099999999999999')  from dual;
select to_char(12345678,'999,999,999,999')  from dual;
select to_char(123456,'99.999')  from dual;
select to_char(1234567890,'999,999,999,999.9999')  from dual;
```

### **（3）to_char(salary,'$99,99');**

```
 select TO_CHAR(123,'$99,999.9') from dual;
```

### **（4）用于进制转换：将10进制转换为16进制；**

```
select to_char(4567,'xxxx') from dual;
select to_char(123,'xxx') from dual;
```

**例子：**

```
to_char 例子
```

①其9代表：如果存在数字则显示数字，不存在则显示空格

②其0代表：如果存在数字则显示数字，不存在则显示0，即占位符。

③其FM代表：删除如果是因9带来的空格，则删除之

```plsql
to_char(now(),'Day, HH12:MI:SS')    'Tuesday , 05:39:18'
to_char(now(),'FMDay, HH12:MI:SS')    'Tuesday, 05:39:18'
to_char(-0.1,'99.99')    ' -.10'
to_char(-0.1,'FM9.99')    '-.1'
to_char(0.1,'0.9')    ' 0.1'
to_char(12,'9990999.9')    ' 0012.0'
to_char(12,'FM9990999.9')    '0012'
to_char(485,'999')    ' 485'
to_char(-485,'999')    '-485'
to_char(485,'9 9 9')    ' 4 8 5'
to_char(1485,'9,999')    ' 1,485'
to_char(1485,'9G999')    ' 1 485'
to_char(148.5,'999.999')    ' 148.500'
to_char(148.5,'999D999')    ' 148,500'
to_char(3148.5,'9G999D999')    ' 3 148,500'
to_char(-485,'999S')    '485-'
to_char(-485,'999MI')    '485-'
to_char(485,'999MI')    '485'
to_char(485,'PL999')    '+485'
to_char(485,'SG999')    '+485'
to_char(-485,'SG999')    '-485'
to_char(-485,'9SG99')    '4-85'
to_char(-485,'999PR')    '<485>'
to_char(485,'L999')    'DM 485'
to_char(485,'RN')    ' CDLXXXV'
to_char(485,'FMRN')    'CDLXXXV'
to_char(5.2,'FMRN')    V
to_char(482,'999th')    ' 482nd'
to_char(485, '"Good number:"999')    'Good number: 485'
to_char(485.8,'"Pre-decimal:"999" Post-decimal:" .999')    'Pre-decimal: 485 Post-decimal: .800'
to_char(12,'99V999')    ' 12000'
to_char(12.4,'99V999')    ' 12400'
to_char(12.45, '99V9')    ' 125'
```

## 预定义的异常处理表

| 错误号   | 异常错误信息名称        | 说明                                                         |
| :------- | ----------------------- | ------------------------------------------------------------ |
| ORA-0001 | Dup_val_on_index        | 违反了唯一性限制                                             |
| ORA-0051 | Timeout-on-resource     | 在等待资源时发生超时                                         |
| ORA-0061 | Transaction-backed-out  | 由于发生死锁事务被撤消                                       |
| ORA-1001 | Invalid-CURSOR          | 试图使用一个无效的游标                                       |
| ORA-1012 | Not-logged-on           | 没有连接到ORACLE                                             |
| ORA-1017 | Login-denied            | 无效的用户名/口令                                            |
| ORA-1403 | No_data_found           | SELECT INTO没有找到数据                                      |
| ORA-1422 | Too_many_rows           | SELECT INTO 返回多行                                         |
| ORA-1476 | Zero-divide             | 试图被零除                                                   |
| ORA-1722 | Invalid-NUMBER          | 转换一个数字失败                                             |
| ORA-6500 | Storage-error           | 内存不够引发的内部错误                                       |
| ORA-6501 | Program-error           | 内部错误                                                     |
| ORA-6502 | Value-error             | 转换或截断错误                                               |
| ORA-6504 | Rowtype-mismatch        | 宿主游标变量与 PL/SQL变量有不兼容行类型                      |
| ORA-6511 | CURSOR-already-OPEN     | 试图打开一个已处于打开状态的游标                             |
| ORA-6530 | Access-INTO-null        | 试图为null 对象的属性赋值                                    |
| ORA-6531 | Collection-is-null      | 试图将Exists 以外的集合( collection)方法应用于一个null pl/sql 表上或varray上 |
| ORA-6532 | Subscript-outside-limit | 对嵌套或varray索引得引用超出声明范围以外                     |
| ORA-6533 | Subscript-beyond-count  | 对嵌套或varray 索引得引用大于集合中元素的个数.               |



## ORACLE中的各种数据类型详细的介绍

| char(n)         | n=1 to 2000字节        | 定长字符串，n字节长，如果不指定长度，缺省为1个字节长（一个汉字为2字节） |
| --------------- | ---------------------- | ------------------------------------------------------------ |
| 数据类型        | 参数                   | 描述                                                         |
| varchar2(n)     | n=1 to 4000字节        | 可变长的字符串，具体定义时指明最大长度n， 这种数据类型可以放数字、字母以及ASCII码字符集(或者EBCDIC等数据库系统接受的字符集标准)中的所有符号。 如果数据长度没有达到最大值n，Oracle 8i会根据数据大小自动调节字段长度， 如果你的数据前后有空格，Oracle 8i会自动将其删去。VARCHAR2是最常用的数据类型。 可做索引的最大长度3209。 |
| number(m,n)     | m=1 to 38 n=-84 to 127 | 可变长的数值列，允许0、正值及负值，m是所有有效数字的位数，n是小数点以后的位数。 如：number(5,2)，则这个字段的最大值是99,999，如果数值超出了位数限制就会被截取多余的位数。 如：number(5,2)，但在一行数据中的这个字段输入575.316，则真正保存到字段中的数值是575.32。 如：number(3,0)，输入575.316，真正保存的数据是575。 |
| date            | 无                     | 从公元前4712年1月1日到公元4712年12月31日的所有合法日期， Oracle 8i其实在内部是按7个字节来保存日期数据，在定义中还包括小时、分、秒。 缺省格式为DD-MON-YY，如07-11月-00 表示2000年11月7日。 |
| long            | 无                     | 可变长字符列，最大长度限制是2GB，用于不需要作字符串搜索的长串数据，如果要进行字符搜索就要用varchar2类型。 long是一种较老的数据类型，将来会逐渐被BLOB、CLOB、NCLOB等大的对象数据类型所取代。 |
| raw(n)          | n=1 to 2000            | 可变长二进制数据，在具体定义字段的时候必须指明最大长度n，Oracle 8i用这种格式来保存较小的图形文件或带格式的文本文件，如Miceosoft Word文档。 raw是一种较老的数据类型，将来会逐渐被BLOB、CLOB、NCLOB等大的对象数据类型所取代。 |
| long raw        | 无                     | 可变长二进制数据，最大长度是2GB。Oracle 8i用这种格式来保存较大的图形文件或带格式的文本文件，如Miceosoft Word文档，以及音频、视频等非文本文件。 在同一张表中不能同时有long类型和long raw类型，long raw也是一种较老的数据类型，将来会逐渐被BLOB、CLOB、NCLOB等大的对象数据类型所取代。 |
| blob clob nclob | 无                     | 三种大型对象(LOB)，用来保存较大的图形文件或带格式的文本文件，如Miceosoft Word文档，以及音频、视频等非文本文件，最大长度是4GB。 LOB有几种类型，取决于你使用的字节的类型，Oracle 8i实实在在地将这些数据存储在数据库内部保存。 可以执行读取、存储、写入等特殊操作。 |
| bfile           | 无                     | 在数据库外部保存的大型二进制对象文件，最大长度是4GB。 这种外部的LOB类型，通过数据库记录变化情况，但是数据的具体保存是在数据库外部进行的。 Oracle 8i可以读取、查询BFILE，但是不能写入。 大小由操作系统决定。‘ |

## PL/SQL变量的命名方式

![1567062326243](oracle_main.assets/1567062326243.png)

