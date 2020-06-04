### ORM简介 [	](mybatis_20200512080327616)

+ ORM的全称:{{c1:: Object/Relation Mapping，对象/关系映射。}}
+ 作用：{{c1:: 面向对象语言与关系型数据库的发展不同步的解决方案。}}

### ORM映射方式 [	](mybatis_20200512080327617)
1. {{c1:: 数据表映射类 }}
2. {{c1:: 数据表的行映射对象（即实例） }}
3. {{c1:: 数据表的列（字段）映射对象的属性 }}

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
// {{c1::
var n = sqlSession.insert("org.crazyit.app.dao.NewsMapper.saveNews", news);
var n = sqlSession.update("org.crazyit.app.dao.NewsMapper.updateNews", news);
var n = sqlSession.delete("org.crazyit.app.dao.NewsMapper.deleteNews", 2);
var news = sqlSession.selectOne("org.crazyit.app.dao.NewsMapper.getNews", 1);
var news = sqlSession.selectList("org.crazyit.app.dao.NewsMapper.getNews", 1);
var newsMapper = sqlSession.getMapper(NewsMapper.class);
// }}
```
### 创建Mapper接口建议约定 [	](mybatis_20200512080327623)

1. {{c1:: Mapper接口的接口名应该与对应XML文件同名。}}
2. {{c1:: Mapper接口的源文件应该与对应XML文档放在相同的包下。}}
3. {{c1:: Mapper接口中抽象方法的方法名与XML Mapper中SQL语句的id相同。}}

### Mybatis核心API及作用域 [	](mybatis_20200514071548547)

| 核心类及组件             | 最佳作用域                | 原因                                                         |
| ------------------------ | ------------------------- | ------------------------------------------------------------ |
| SqlSessionFactoryBuilder | {{c1::局部作用域}}        | {{c1::唯一作用就是创建SqlSessionFactory，只有单个Build()方法}} |
| SqlSessionFactory        | {{c1::整个应用运行期间}}  | {{c1::底层封装的当前应用的数据库配置环境，每个数据库对应一个SqlSessionFactory实例}}                   |
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

## Mybatis配置 [	](mybatis_20200520043218578)

### Mybatis允许3个地方配置属性 [	](mybatis_20200514071548553)
1. {{c1::  额外属性文件配置：`<properties resource="db.properties">`。}}
2. {{c1:: 直接配置`<properties>`的子元素。}}
3. {{c1:: SqlSessionFactory中build()方法传入Properties对象。}}
+ 属性优先级为：{{c1::  build()方法 > 额外属性文件 >  `<propertiy>`子元素。
+ 引用属性语法：{{c1::  `${user:defaultUser}` }}

### Mybatis设置配置：启用延时加载功能 [	](mybatis_20200520043218581)
{{c1::
```xml
<settings>
    <setting name="lazyLoadingEnabled" value="true"/>
</settings>
```
}}

### Mybatis配置别名 [	](mybatis_20200520043218583)
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

### 自定义对象工厂 [	](mybatis_20200520043218584)

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
### 4种加载Mapper的方式 [	](mybatis_20200520043218586)
1. {{c1:: `<mapper resource="top/xieyun/app/dao/NewsMapper.xml">`}}
2. {{c1:: `<mapper url="file:///G:/abc/NewsMapper.xml">`}}
3. {{c1:: `<mapper class="top.xieyun.app.dao.NewsMapper.xml">`}}
4. {{c1:: `<mapper package="top.xieyun.app.dao">`}}

### Mybatis类型转换器 [	](mybatis_20200520043218588)
+ 首先实现{{c1::`TypeHandler<T>`}}接口，或者继承{{c1::`BaseTypeHandler<T>`}}基类,实现以下方法
    1. `void setNonNullParameter(PreparedStatement ps, int i,T param, JdbcType jdbcType)`
    2. `T getNullableResult(ResultSet rs, String columnIndex)`
    3. `T getNullableResult(ResultSet rs, int columnIndex)`
    4. `T getNullableResult(CallableStatement cs, int columnIndex)`
+ 配置类型转换器
    {{c1::
    ```xml
        <typeHandlers>
            <typeHandler handler="com.zy.converter.BooleanAndIntConverter"/>
        </typeHandlers>
    ```
    }}
+ 指定JDBC类型与JAVA类型
    1. 核心配置指定
        {{C1::
        ```xml
        <typeHandler handler="com.zy.converter.BooleanAndIntConverter"
                    javaType="Boolean" jdbcType="INTEGER" />
        ```
        }}

    2. java注解指定
        {{C1::
        ```java
        @MappedJdbcTypes({JdbcType.VARCHAR})
        @MappedTypes({Name.class})
        public class MyTypeHandler extends BaseTypeHandler<Name> {
        ```
        }}
### Mybatis枚举的类型处理器 [	](mybatis_20200520043218590)
+ Mybatis默认的枚举处理器：{{c1:: `EnumTypeHandler` }}
+ `EnumTypeHandler`:{{c1:: 将枚举值转换成对应名称（字符串）}}
+ `EnumOrdinalTypeHandler`:{{c1:: 将枚举值转换成对应序号（整数）,使用需单独配置。}}

### 在Mybatis中为特定属性指定类型处理器的方式 [	](mybatis_20200520043218592)
+ 查询的情况
    + {{c1:: 在`<result>`元素中或者`@Result`注解中指定typeHandler属性
    ```xml
        <result column="record_season" property="recordSeason"
                typeHandler="org.apache.ibatis.type.EnumTypeHandler"/>
    ```
    ```java
        @Result(property = "recordSeason", column = "record_season",
			typeHandler = EnumTypeHandler.class)
    ​```
    ```
    
    }}
    
+ 插入的情况:
  
    + {{c1:: 在#{}中指定typeHandler属性:
    ```sql
	    insert into news_inf values
		(null, #{title}, #{content}, #{happenSeason}, #{recordSeason,
    	typeHandler=org.apache.ibatis.type.EnumTypeHandler})
    ```
    
    ​		 }}
    

### 事务管理器 [	](mybatis_20200521095802607)

`<transactionManager type="JDBC"/>`:{{c1:: 使用JDBC自带的事务提交与回滚，对应类为`JdbcTransactionFactory`。}}
`<transactionManager type="MANAGED"/>`:{{c1:: 使用容器来管理事务的生命周期}}

### 自定义Mybatis事务管理器 [	](mybatis_20200521095802608)

1. 实现TransactionFactory接口
```java
void setProperties(Properties props);
Transaction newTransaction(Connection conn);
Transaction newTransaction(DataSource ds,TransactionIsolationLevel level, boolean autoCommit);
```
    + props:{{c1:: `传入<transactionManager />`中的配置属性 }}
    + conn:{{c1:: 传入指定Connection}}
    + ds:{{c1:: 传入指定的数据源}}
    + level:{{c1:: 事务隔离级别}}
    + autoCommit:{{c1:: 是否自动提交事务}}
2. 实现Transaction接口
```java
Connection getConnection() throws SQLException;
void commit() throws SQLException;
void rollback() throws SQLException;
void close() throws SQLException;
Integer getTimeout() throws SQLException;
```
+ 注意：{{c1:: 从数据源获得connection与直接传入connection的区别 }}

### MyBatis内置了三种数据源实现 [	](mybatis_20200521095802609)

1. UNPOOLED:{{c1:: 不使用连接池，每次都会重新打开连接。}}
2. POOLED：{{c1:: 使用Mybatis内置的连接池。}}
3. JNDI：{{c1:: 使用容器管理的连接池。}}
4. 以上连接池对应的实现类为：{{c1:: `UnpooledDataSourceFactory` `PooledDataSourceFactory` `JndiDataSourceFactory`}}

### MyBatis自定义C3P0数据源 [	](mybatis_20200521095802611)

1. 实现{{c1::`DataSourceFactory`}}接口或继承{{c1::`UnpooledDataSourceFactory`}}类
    ```java
        public class C3P0DataSourceFactory extends UnpooledDataSourceFactory
        {
            //{{c1::
            public C3P0DataSourceFactory()
            {
                this.dataSource = new ComboPooledDataSource();
            }
            //}}
        }
    ```
2. 配置数据源
    + 配置自定义数据源别名：{{c1::`<typeAlias type="top.xieyun.dao.C3P0DataSourceFactory" alias="C3P0"/>`}}
    + 配置数据源：
        ```xml
            <!-- {{c1:: -->
            <dataSource type="C3P0">
            <!-- 下面这些属性是直接注入C3P0数据源（ComboPooledDataSource对象）的
            因此这些属性名必须是ComboPooledDataSource类的各setter方法对应
            -->
            <property name="driverClass" value="com.mysql.cj.jdbc.Driver"/>
            <property name="jdbcUrl" value="jdbc:mysql://127.0.0.1:3306/mybatis?serverTimezone=UTC"/>
            <property name="user" value="root"/>
            <property name="password" value="32147"/>
            <property name="maxPoolSize" value="40"/>
            <property name="minPoolSize" value="2"/>
            <property name="initialPoolSize" value="2"/>
            <property name="maxIdleTime" value="200"/>
			</dataSource>
            <!-- }} -->
        ```