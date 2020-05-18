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