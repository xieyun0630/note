### ORM简介 [	](mybatis_20200512080327616)
+ ORM的全称:{{c1:: Object/Relation Mapping，对象/关系映射。}}
+ 作用：{{c1:: 面向对象语言与关系型数据库的发展不同步的解决方案。}}

### ORM映射方式 [	](mybatis_20200512080327617)
1. 数据表映射类
2. 数据表的行映射对象（即实例）
3. 数据表的列（字段）映射对象的属性

### MyBatis如何将ResultSet的每一行转换成Java对象呢？ [	](mybatis_20200512080327618)
1. 自动转换:{{c1:: 表列名（或列别名）和对象属性名相同 }}
2. 显式指定:{{c1:: 使用`<result>`元素或`@Result`来指定列名与属性之间的关系。 }}

### mybatis-config.xml文件 [	](mybatis_20200512080327619)
+ `<environments>`的配置
{{c1::
    ```xml
        <environments default="mysql">
            <environment id="mysql">
                <transactionManager type="JDBC"/>
                <dataSource type="POOLED">
                    <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                    <property name="url" value="jdbc:mysql://127.0.0.1:3306/mybatis?serverTimezone=UTC"/>
                    <property name="username" value="root"/>
                    <property name="password" value="32147"/>
                </dataSource>
            </environment>
        </environments>
    ```
}}
+ `<mappers>`元素的配置
{{c1::
    ```xml
        <mappers>
            <mapper resource="org/crazyit/app/dao/NewsMapper.xml"/>
        </mappers>
    ```
}}

### MyBatis手动创建session对象 [	](mybatis_20200512080327621)
```java
    //{{c1::
    var inputStream = Resources.getResourceAsStream("mybatis-config.xml");
    var sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    var sqlSession = sqlSessionFactory.openSession();
    //}}
```

### 使用SqLSession执行Mapper中定义的SQL语句 [	](mybatis_20200512080327622)

```java
{{c1::
var n = sqlSession.insert("org.crazyit.app.dao.NewsMapper.saveNews", news);
var n = sqlSession.update("org.crazyit.app.dao.NewsMapper.updateNews", news);
var n = sqlSession.delete("org.crazyit.app.dao.NewsMapper.deleteNews", 2);
var news = sqlSession.selectOne("org.crazyit.app.dao.NewsMapper.getNews", 1);
var news = sqlSession.selectList("org.crazyit.app.dao.NewsMapper.getNews", 1);
var newsMapper = sqlSession.getMapper(NewsMapper.class);
}}
```
### 创建Mapper接口建议约定 [	](mybatis_20200512080327623)

1. {{c1:: Mapper接口的接口名应该与对应XML文件同名。}}
2. {{c1:: Mapper接口的源文件应该与对应XML文档放在相同的包下。}}
3. {{c1:: Mapper接口中抽象方法的方法名与XML Mapper中SQL语句的id相同。}}

### Mybatis核心API及作用域 [	](mybatis_20200514071548547)

| 核心类及组件             | 最佳作用域                | 原因                                                         |
| ------------------------ | ------------------------- | ------------------------------------------------------------ |
| SqlSessionFactoryBuilder | {{c1::局部作用域}}        | {{c1::唯一作用就是创建SqlSessionFactory，只有单个Build()方法}} |
| SqlSessionFactory        | {{c1::整个应用运行期间}}  | {{c1::底层封装的当前应用的数据库配置环境}}                   |
| SqlSession               | {{c1::方法或单个Request}} | {{c1::线程不安全，无法多线程访问}}                           |
| Mapper组件               | {{c1::局部作用域}}        | {{c1::因为是由SqlSession创建，作用域应该不大于SqlSession。}} |

### SqlSessionFactoryBuilder主要方法 [	](mybatis_20200514071548549)
```java
public SqlSessionFactory build(Reader|InputStream reader, String environment, Properties properties) 
```
- reader参数：{{c1:: 当前mybatis-config.xml配置文件 }}
- environment参数:{{c1:: 指定environment id值，不指定默认使用environments中default属性的值。}}
- Properties参数:{{c1:: 加载Mybatis属性配置。}}

### SqlSessionFactory [	](mybatis_20200514071548550)
```java
  SqlSession openSession();
  SqlSession openSession(boolean autoCommit);
  SqlSession openSession(Connection connection);
  SqlSession openSession(TransactionIsolationLevel level);
  SqlSession openSession(ExecutorType execType);
  SqlSession openSession(ExecutorType execType, boolean autoCommit);
  SqlSession openSession(ExecutorType execType, TransactionIsolationLevel level);
  SqlSession openSession(ExecutorType execType, Connection connection);
```
**参数:**
- autoCommit: {{c1:: 是否自动提交事务 }}
- connection：{{c1:: 设置指定的JDBC连接对象 }}
- level：{{c1:: 设置事务隔离级别 }}
- execType：{{c1:: 执行语句的类型 }}
  1. ExecutorType.SIMPLE: {{c1:: 每次执行SQL都创建新的PreparedStatement对象 }}
  2. ExecutorType.REUSE: {{c1:: 重复使用PreparedStatement对象 }}
  3. ExecutorType.BATCH: {{c1:: 启用批量更新，当需要批量插入，更新多条数据时，启用批量更新较好。}}

### SqlSession执行SQL语句的主要方法 [	](mybatis_20200514071548551)

```java
<T> T selectOne(String statement, Object parameter);
<E> List<E> selectList(String statement, Object parameter);
int insert(String statement, Object parameter);
int update(String statement, Object parameter);
int delete(String statement, Object parameter);
```
 + statement:{{c1:: SQL语句在mapper.xml文件中的位置 }}
 + parameter:{{c1:: 传入SQL语句中的参数 }}

### SqlSession控制事务主要方法 [	](mybatis_20200514071548552)

```java
  void commit();
  void commit(boolean force);
  void rollback();
  void rollback(boolean force);
  List<BatchResult> flushStatements();
```
flushStatements():{{c1:: 执行批量更新。}}
force:{{c1:: 是否强制提交或回滚。}}

## Mybatis配置

### Mybatis允许3个地方配置属性 [	](mybatis_20200514071548553)
1. {{c1::  额外属性文件配置：`<properties resource="db.properties">`。}}
2. {{c1:: 直接配置`<properties>`的子元素。}}
3. {{c1:: SqlSessionFactory中build()方法传入Properties对象。}}
属性优先级为：{{c1::  build()方法 > 额外属性文件 >  `<propertiy>`子元素。
引用属性语法：{{c1::  `${user:defaultUser}` }}

### Mybatis设置配置：启用延时加载功能
{{c1::
```xml
<settings>
    <setting name="lazyLoadingEnabled" value="true"/>
</settings>
```
}}

### Mybatis配置别名
1. 为单个类指定别名
    {{c1::
    ```xml
        <typeAlias alias="news" type="top.xieyun.domain.News" />
    ```
    }}
2. 为指定包下的所有类指定别名
    {{c1::
    ```xml
        <package name= "top.xieyun.domain" />
    ```
    }}
3. 使用注解指定别名
    {{c1::
    ```java
        @Alias("fkNews")
        public class News{
            //...
        }
    ```
    }}
4. 使用别名
    {{c1::
    ```
        <select id="getNews" resultType="fkNews">
    ```
    }}

### 自定义对象工厂

+ 首先实现{{c1::`ObjectFactory`}}接口，或者继承{{c1::`DefaultObjectFactory`}}基类,实现以下方法
    1. `T create(Class<T> type)`
    2. `T create​(Class<T> type,List<Class<T>> constructorArgTypes, List<Object> constructorArgs)`
    3. `T setProperties(Properties properties)`
    4. `<T> boolean isCollection(Class<T> type)`
    + type：{{c1:: 要创建对象的类型。}}
    + constructorArgTypes：{{c1:: 要创建对象的构造器参数列表}}
    + constructorArgs：{{c1:: 多个构造器参数的值}}
    + properties:{{c1:: 核心配置文件中对象工厂配置的属性}}
+ 配置自定义工厂类
{{c1::
    ```xml
        <objectFactory type="top.xieyun.mybatis.myObjectFactory">
            <property name="author" value="crazyit" />
        </objectFactory>
    ```
}}
### 4种加载Mapper的方式
1. {{c1:: `<mapper resource="top/xieyun/app/dao/NewsMapper.xml">`}}
2. {{c1:: `<mapper url="file:///G:/abc/NewsMapper.xml">`}}
3. {{c1:: `<mapper class="top.xieyun.app.dao.NewsMapper.xml">`}}
4. {{c1:: `<mapper package="top.xieyun.app.dao">`}}

### Mybatis类型转换器
+ 首先实现{{c1::`TypeHandler<T>`}}接口，或者继承{{c1::`BaseTypeHandler<T>`}}基类,实现以下方法
    1. `void setNonNullParameter(PreparedStatement ps, int i,T param, JdbcType jdbcType)`
    2. `T getNullableResult(ResultSet rs, String columnIndex)`
    3. `T getNullableResult(ResultSet rs, int columnIndex)`
    4. `T getNullableResult(CallableStatement cs, int columnIndex)`