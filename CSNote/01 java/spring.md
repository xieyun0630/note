
### EJB对比Spring [	](spring_20200713102713839)

- EJB({{c1:: Enterprise Java Bean }})特点：
    1. {{c1:: 运行环境苛刻 }}
    2. {{c1:: 代码移植性差 }}
    3. {{c1:: 重量级的框架 }}
- Spring:{{c1:: 轻量级的JavaEE解决方案，整合众多优秀的设计模式 }}
  - 轻量级：{{c1:: 对于运行环境是没有额外要求的 }}
    - 开源运行环境：{{c1:: tomcat resion jetty }}
    - 收费运行环境：{{c1:: weblogic websphere }}
  - 代码移植性高,{{c1:: 不需要实现额外接口 }}
  - 整合设计模式
    1.  {{c1:: 工厂 }}
    2.  {{c1:: 代理 }}
    3.  {{c1:: 模板 }}
    4.  {{c1:: 策略 }}

### 静态类实现通用工厂 [	](spring_20200713102713842)
- 简单工厂会存在大量的代码冗余
  
  - ![image-20200411181701143](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200411181701143.png)
- 通用工厂的代码
  ```java
  //{{c1::
  public class BeanFactory{
      public static Object getBean(String key){
          Object ret = null;
          try {
              Class clazz = Class.forName(env.getProperty(key));
              ret = clazz.newInstance();
          } catch (Exception e) {
              e.printStackTrace();
          }
          return ret;
      }
  }
  //}}
  ```

##  Spring的核心API [	](spring_20200713102713844)

### BeanFactory [	](spring_20200824063336925)

+ 作用：{{c1:: spring最核心的接口，是`ApplicationContext`的父接口。 }}

+ 常用实现类：{{c1:: `DefaultListableBeanFactory` }}





### ApplicationContext [	](spring_20200713102713846)

+ 作用：工厂接口
- 主要实现类
  - 非web环境:(main junit)：{{c1::  `ClassPathXmlApplicationContext` }}
  - web环境 ：{{c1::   `XmlWebApplicationContext` }}
- 重量级资源含义：{{c1:: ApplicationContext工厂的对象占用大量内存，一个应用只会创建一个工厂对象，一定是线程安全的。 }}

### ApplicationContext的国际化:概念 [	](spring_20200824063336928)

- ApplicationContext继承了MessageSource接口，该接口具有以下方法：
  1. {{c1:: `String getMessage(String code,Object[] args,Locale loc)` }}
  2. {{c1:: `String getMessage(String code,Object[] args,String default,Locale loc)` }}
- ApplicationContext在创建时，为了实现国际化：
  - {{c1:: 会自动在其容器中寻找`messageSource bean` }}
  - {{c1:: 如果没有找到，会自动创建一个`staticMessageSrouce bean`接收getMessage方法的调用 }}

### ApplicationContext的国际化:使用 [	](spring_20200824063336931)

- 给出文件名为`message_en_US.properties`与`message_zh_CN.properties`两个资源文件
- 配置`messageSource`:
  ```xml
   <!-- {{c1:: -->
    <bean id="messageSource" class="xxx.ResourceBundleMessageSource">
      <property name="defaultEncoding" value="utf-8"/>
      <property name="basenames">
        <list>
          <value>message</value>
        </list>
      </property>
    </bean>
    <!-- }} -->
  ```
- 使用：
  ```java
    //{{c1::
    ctx.getMessage("hello", new String[]{"孙悟空"},Locale.getDefault(Locale.Category.FORMAT));
    ctx.getMessage("now", new Object[]{new Date()},Locale.getDefault(Locale.Category.FORMAT));  
    //}}
  ```

### ApplicationContext的事件机制 [	](spring_20200824063336933)

+ 简单使用例子：
  ```java
    //{{c1::
    var ctx = new ClassPathXmlApplicationContext("beans.xml");
    // 创建一个ApplicationEvent对象
    var ele = new EmailEvent("test", "spring_test@163.com", "this is a test");
    // 发布容器事件
    ctx.publishEvent(ele);
    //}}
  ```
+ 使用事件机制的配置步骤：
   1. {{c1:: 自定义实现了`ApplicationEvent`的事件类 }}
   2. {{c1:: 自定义实现了`ApplicationListener`的监听器 }}
   3. {{c1:: 配置监听器：`<bean class="xx.xxApplicationListener" />` }}
   
### spring内置的xxxAware接口 [	](spring_20200824063336936)

+ 作用：{{c1:: 让容器调用setter将**特定的对象**注入到实现了`xxxAware接口`的`bean`中 }}
+ 常见的`xxxAware接口`：
  + `BeanNameAware`：{{c1:: 容器会注入bean本身的id值 }}
  + `ResourceLoaderAware`：{{c1:: 容器会注入资源访问器，如果没有自定义`ResourceLoader`,默认注入的实际上是`ResourceLoader`类型的`ctx`对象 }}
  + `ApplicationContextAware`：{{c1:: 容器会注入ctx对象 }}

### spring程序开发流程 [	](spring_20200713102713847)

1. 创建java类:{{c1:: `public class Person{...}` }}
2. 在配置文件中配置Bean :{{c1:: `<bean id="person" class="com.baizhiedu.basic.Person"/>` }}
3. 通过工厂（容器）类，获得对象
   ```java
   //{{c1::
   ApplicationContext ctx = new ClassPathXmlApplicationContext("/applicationContext.xml");
   Person person = (Person)ctx.getBean("person");
   //}}
   ```
- 注意：Spring工厂创建的对象，叫做{{c1:: bean或者组件(componet) }}

### Spring工厂的相关的方法 [	](spring_20200713102713849)

+ 通过这种方式获得对象，就不需要强制类型转换:{{c1:: `Person person = ctx.getBean("person", Person.class);`}}
+ 当前Spring的配置文件中 只能有一个`<bean class ..>`是Person类型:{{c1:: `Person person = ctx.getBean(Person.class);`}}
+ 获取的是 Spring工厂配置文件中所有bean标签的id值:{{c1:: `String[] beanDefinitionNames = ctx.getBeanDefinitionNames();`}}
+ 根据类型获得Spring配置文件中对应的id值:{{c1:: `String[] beanNamesForType = ctx.getBeanNamesForType(Person.class);`}}
+ 用于判断是否存在指定id值得bean:{{c1:: `ctx.containsBeanDefinition("a")`}}
+ 用于判断是否存在指定id值得bean:{{c1:: `ctx.containsBean("person")`}}

### spring配置文件细节 [	](spring_20200713102713850)

+ `<bean  class="com.baizhiedu.basic.Person"/>`自动分配的id值为:{{c1:: com.baizhiedu.basic.Person#0 }}
+ name属性与id属性的区别
  1. 多个别名：{{c1:: 别名可以定义多个,但是id属性只能有一个值}}
  2. 命名要求：{{c1:: XML的id属性的值有命名要求：必须以字母开头，字母 数字 下划线 连字符 不能以特殊字符开头 /person，但现在这个限制已经没有了。name属性的值没有命名要求。}}
  3. ctx.containsBean("p"):{{c1:: 也可以判断name值}}
  4. ctx.containsBeanDefinition("person"):{{c1:: 不可以判断name值}}

### Spring5.x与日志框架的整合 [	](spring_20200715110208921)

+ 默认日志框架
  + spring 1/2/3 早起都是基于：{{c1:: commons-logging.jar}}
  + spring 5.x默认使用：{{c1:: logback log4j2}}
+ 整合log4j
  1. 引入依赖：{{c1:: `slf4j-log4j12` `log4j`}}
  2. 配置文件：{{c1:: 将`log4j.properties`放在`resources`文件夹根目录下}}

## 依赖注入 [	](spring_20200715110208922)
### 什么是注入 [	](spring_20200715110208923)
  + 注入：{{c1:: Injection,通过Spring工厂及配置文件，为所创建对象的成员变量赋值 }}
  + 为什么需要注入：{{c1:: **通过编码的方式，为成员变量进行赋值，存在耦合** }}
  + 如何进行注入[开发步骤]
    - {{c1:: 类的成员变量提供set get方法 }}
    - {{c1:: 配置spring的配置文件 }}
      ```xml
        <!-- {{c1:: -->
        <bean id="person" class="com.baizhiedu.basic.Person">
          <property name="id">
            <value>10</value>
          </property>
          <property name="name">
            <value>xiaojr</value>
          </property>
        </bean>
        <!-- }} -->
      ```
### Spring注入的原理分析(简易版) [	](spring_20200715110208924)

+ `<bean id="account" class="xxx.Accout">`等效于：{{c1:: `Account account = new Account();`}}
+ `<property name="name">`等效于：{{c1:: `account.setName("suns");`}}

### JDK内置类型注入 [	](spring_20200715110208925)

+ String + 8种基本类型：
  ```xml
  <!-- {{c1:: -->
  <value>suns</value>
  <!-- }} -->
  ```
+ 数组
  ```xml
  <!-- {{c1:: -->
  <list>
    <value>suns@zparkhr.com.cn</value>
    <value>liucy@zparkhr.com.cn</value>
    <value>chenyn@zparkhr.com.cn</value>
  </list>
  <!-- }} -->
  ```
+ Set集合
  ```xml
  <!-- {{c1:: -->
  <set>
    <value>11111</value>
    <value>112222</value>
    <ref bean="account">
    <set>...
  </set>
  <!-- }} -->
  ```
+ List集合
  ```xml
  <!-- {{c1:: -->
  <list>
    <value>11111</value>
    <value>2222</value>
    <ref bean>
    <set>...
  </list>
  <!-- }} -->
  ```
+ Map集合
  ```xml
  <!-- {{c1:: -->
  <map>
    <entry>
      <key><value>suns</value></key>
      <value>3434334343</value>
    </entry>
    <entry>
      <key><value>chenyn</value></key>
      <ref bean="account">
    </entry>
  </map>
  <!-- }} -->
  ```
+ Properites
  ```xml
  <!-- {{c1:: -->
  <!-- Properties类型 特殊的Map key=String value=String  -->
  <props>
    <prop key="key1">value1</prop>
    <prop key="key2">value2</prop>
  </props>
  <!-- }} -->
  ```

### 用户自定义类型注入 [	](spring_20200715110208926)

- 新建bean注入(赋值)
  ```xml
  <!-- {{c1:: -->
  <bean id="userService" class="xxxx.UserServiceImpl">
     <property name="userDAO">
         <bean class="xxx.UserDAOImpl"/>
    </property>
  </bean>
  <!-- }} -->
  ```
  + 存在问题
    1. {{c1:: 配置文件代码冗余}}
    2. {{c1:: 被注入的对象(UserDAO),多次创建，浪费（JVM)内存资源}}
+ bean引用注入
  ```xml
  <!-- {{c1:: -->
  <bean id="userDAO" class="xxx.UserDAOImpl"/>
  <bean id="userService" class="xxx.UserServiceImpl">
     <property name="userDAO">
          <ref bean="userDAO"/>
    </property>
  </bean>
  <!-- }} -->
  ```

### 依赖注入:Set注入的简化写法 [	](spring_20200715110208927)

- 基于属性的简化写法
  - spring + 8种基本类型:{{c1:: `<property name="name" value="suns"/>`}}
  - 用户自定义类型：{{c1:: `<property name="userDAO" ref="userDAO"/>`}}
- 基于p命名空间的简化写法
  - spring + 8种基本类型:{{c1:: `<bean id="person" class="xxx.Person" p:name="suns"/>`}}
  - 用户自定义类型：{{c1:: `<bean id="userService" class="xxx.UserServiceImpl" p:userDAO-ref="userDAO"/>`}}

### 依赖注入:构造注入 [	](spring_20200715110208928)

- 基于以下代码进行构造注入
    ```java
    public class Customer implements Serializable {
        private String name;
        private int age;
        public Customer(String name, int age) {
            this.name = name;
            this.age = age;
        }
    }
    ```
+ 配置文件
    ```xml
    <!-- {{c1:: -->
    <bean id="customer" class="com.baizhiedu.basic.constructer.Customer">
      <constructor-arg>
        <value>suns</value>
      </constructor-arg>
      <constructor-arg>
        <value>102</value>
      </constructor-arg>
    </bean>
    <!-- }} -->
    ```

+ 当构造方法有多个重载方法时的2种情况的类型冲突解决
  1. 参数个数不同时：{{c1:: 通过控制`<constructor-arg>`标签的数量进行区分  }}
  2. 构造参数个数相同时：{{c1:: `用type属性进行类型的区分 <constructor-arg type="">` }}

### spring注入的总结图 [	](spring_20200715110208929)

{{c1::![image-20200416155620897](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200416155620897.png)}}

### 反转控制与依赖注入 [	](spring_20200715110208930)

- 反转控制：
  - IOC：{{c1:: inverse of Control }}
  - 控制:{{c1:: 对于成员变量赋值的控制权 }}
  - 反转控制:{{c1:: 把对于成员变量赋值的控制权，从代码中反转(转移)到Spring工厂和配置文件中完成,达到解耦合的目的 }}
- 依赖注入：
  - DI：{{c1:: Dependency Injection }}
  - 注入：{{c1:: 通过Spring的工厂及配置文件，为对象（bean，组件）的成员变量赋值 }}
  - 依赖注入：{{c1:: 当一个类需要另一个类时，就意味着依赖，一旦出现依赖，就可以把另一个类作为本类的成员变量，最终通过Spring配置文件进行注入(赋值),达到解耦合的目的 }}

## spring工程高级特性 [	](spring_20200717061050980)

### Spring工厂创建复杂对象的3种方式 [	](spring_20200715110208931)

- 实例工厂与静态工厂
  - 作用：{{c1:: 避免Spring框架的侵入，整合遗留系统  }}
  - 实例工厂:
    ```xml
      <!-- {{c1:: -->
     <bean id="connFactory" class="com.baizhiedu.factorybean.ConnectionFactory"></bean>
     <bean id="conn"  factory-bean="connFactory" factory-method="getConnection"/>
     <!-- }} -->
    ```
  - 静态工厂：
      ```xml
      <!-- {{c1:: -->
      <bean id="conn" class="com.baizhiedu.factorybean.StaticConnectionFactory" factory-method="getConnection"/>
      <!-- }} -->
      ```

- 实现FactoryBean接口
  - 实现内部3个方法:
    1. {{c1:: T getObject() throws Exception;：返回要创建的对象 }}
    2. {{c1:: Class<?> getObjectType();：反对对象类型 }}
    3. {{c1:: boolean isSingleton();：是否使用单例模式 }}
  
  - 配置：{{c1:: `<bean id="conn" class="com.baizhiedu.factorybean.ConnectionFactoryBean"/>` }}
  
  - 细节:
    - 获得FactoryBean对象本身 :{{c1:: `ctx.getBean("&conn")`获得就是ConnectionFactoryBean对象 }}
    - mysql高版本连接创建时，需要制定SSL证书，解决问题的方式
      
      - {{c1:: `url = "jdbc:mysql://localhost:3306/suns?useSSL=false"` }}
  
- 注意：以上3种方法创建的Bean同样可以使用`<property>`进行set依赖注入

### Spring工厂创建对象与依赖注入的流程图 [	](spring_20200715110208932)

{{c1::![image-20200417152030222](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200417152030222.png)}}

### Spring工厂创建对象的次数 [	](spring_20200715110208933)

- 创建对象的次数的类型：
  - singleton:{{c1:: 只会创建一次简单对象 默认值}}
  - prototype:{{c1:: 每一次都会创建新的对象}}
- 控制简单对象的创建次数:{{c1:: `<bean id="account" scope="singleton|prototype" class="xxxx.Account"/>`}}
- 控制复杂对象的创建次数:{{c1:: 实现FactoryBean接口中`boolean isSingleton()`方法返回值}}
- 什么样的对象只创建一次？
  1. {{c1:: `SqlSessionFactory` }}
  2. {{c1:: `DAO` }}
  3. {{c1:: `Service` }}
- 什么样的对象 每一次都要创建新的？
  1. {{c1:: `Connection` }}
  2. {{c1:: `SqlSession | Session` }}
  3. {{c1:: `Struts2 Action` }}


### spring中Bean的生命周期执行步骤： [	](spring_20200715110208935)

1. 创建实例
2. 注入依赖关系
3. 初始化：{{c1:: 调用`InitializingBean`接口中的`afterPropertiesSet`方法 }}
4. 初始化：{{c1:: 调用`<bean>`元素`init-mehotd`指定的方法 }}
5. 对外提供服务
6. 销毁：{{c1:: 调用`DisposableBean`接口中的`destroy()`方法 }}
7. 销毁：{{c1:: 调用`<bean>`元素`destroy-mehotd`指定的方法 }}
8. Bean实例被销毁
+ 注意：
  1. {{c1:: 销毁方法的操作只适用于 scope="singleton" }}
  2. {{c1:: 注入一定发生在初始化操作的前面 }}

### spring配置文件参数化的开发步骤 [	](spring_20200715110208936)

- 提供一个小的配置文件(.properities)
  ```properties
  <!-- {{c1:: -->
  jdbc.driverClassName = com.mysql.jdbc.Driver
  jdbc.url = jdbc:mysql://localhost:3306/suns?useSSL=false
  jdbc.username = root
  jdbc.password = 123456
  <!-- }} -->
  ```
- applicationContext.xml中配置
  ```xml
  <!-- {{c1:: -->
  <context:property-placeholder location="classpath:/db.properties"/>
  <!-- }} -->
  ```
- 在Spring配置文件中通过${key}获取小配置文件中对应的值
  ```xml
  <!-- {{c1:: -->
  <bean id="conn" class="com.baizhiedu.factorybean.ConnectionFactoryBean">
    <property name="driverClassName" value="${jdbc.driverClassName}"/>
    <property name="url" value="${jdbc.url}"/>
    <property name="username" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
  </bean>
  <!-- }} -->
  ```

### 自定义spring类型转换器 [	](spring_20200715110208937)

+ 自定义Converter接口:
  ```java
  //{{c1::
  public class MyDateConverter implements Converter<String, Date> {
    @Override
    public Date convert(String source) {
      Date date = null;
      try {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        date = sdf.parse(source);
      } catch (ParseException e) {
        e.printStackTrace();
      }
      return date;
    }
  }
  //}}
  ```
+ applicationContext.xml中配置:
  + 创建转换器对象：
  ```xml
    <!-- {{c1:: -->
    <bean id="myDateConverter" class="com.baizhiedu.converter.MyDateConverter">
      <property name="pattern" value="yyyy-MM-dd"/>
    </bean>
    <!-- }} -->
  ```
  + 类型转换器的注册
  ```xml
    <!-- {{c1:: -->
    <!-- ConversionSeviceFactoryBean 定义 id属性 值必须 conversionService  -->
    <bean id="conversionService" class="....ConversionServiceFactoryBean">
      <property name="converters">
        <set>
          <ref bean="myDateConverter"/>
        </set>
      </property>
    </bean>
    <!-- }} -->
  ```

### Bean后置处理器 [	](spring_20200715110208938)

1. {{c1:: 实现 BeanPostProcessor接口 }}
2. {{c1:: Spring的配置文件中进行配置`<bean id="myBeanPostProcessor" class="xxx.MyBeanPostProcessor"/>` }}
   +  注意：{{c1:: BeanPostProcessor会对Spring工厂中所有创建的对象进行加工。 }}
+ 运行流程图
  + {{c1::![image-20200420155053027](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200420155053027.png)}}

### 容器后置处理器 [	](spring_20200911094545271)
+ 容器后置处理器必须实现：{{c1:: `BeanFactoryPostProcessor`接口 }}
+ 作用：{{c1:: 通常用于容器初始化后对容器的整体操作 }}


### spring内置**属性占位符**容器后置处理器 [	](spring_20200911094545273)
+ 接口：{{c1:: `PropertyPlaceholderConfigurer`}}
+ 作用：{{c1:: 使用`properties`文件简化`beans.xml`的配置}}
+ 命名空间简化配置：{{c1:: `<context:property-placeholder location="classpath:db.properties" />`}}
+ 实际配置：
  ```xml
    <!-- {{c1:: -->
    <bean class=
      "org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
      <property name="locations">
        <list>
          <value>dbconn.properties</value>
        </list>
      </property>
    </bean>
    <!-- 定义数据源Bean，使用C3P0数据源实现 -->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource"
      destroy-method="close"
      p:driverClass="${jdbc.driverClassName}"
      p:jdbcUrl="${jdbc.url}"
      p:user="${jdbc.username}"
      p:password="${jdbc.password}"/>
    </beans>
    <!-- }} -->
  ```
### spring内置**重写占位符**容器后置处理器 [	](spring_20200911094545275)

+ 接口：{{c1:: `PropertyOverrideConfigurer`}}
+ 作用：{{c1:: 使用`properties`文件覆盖`<bean ..>`的`property`}}
+ 命名空间简化配置：{{c1:: `<context:property-placeholder location="classpath:db.properties" />`}}
+ 实际配置：
  + properties配置
  ```yaml
    dataSource.driverClass=com.mysql.cj.jdbc.Driver
    dataSource.jdbcUrl=jdbc:mysql://localhost:3306/spring?serverTimezone=UTC
    dataSource.user=root
    dataSource.password=32147
  ```
  + xml配置
  ```xml
    <!-- {{c1:: -->
    <bean class=
    "org.springframework.beans.factory.config.PropertyOverrideConfigurer">
      <property name="locations">
        <list>
          <value>dbconn.properties</value>
        </list>
      </property>
    </bean>
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource" 
      destroy-method="close"/>  
      <!-- }} -->
  ```

### singleton Bean的初始化 [	](spring_20200824063336938)

+ `BeanFactory`:{{c1:: 以BeanFactory创建容器不会初始化容器中的Bean }}
+ `ApplicationContext`:{{c1:: singleton Bean 在ApplicationContext创建时会一起创建并初始化 }}
+ 阻止`singletonBean`初始化:{{c1:: 阻止singletonBean初始化:为 `<bean>` 加上` lazy-init="true"` }}

## spring容器中的bean [	](spring_20200824063336941)

### `<beans>根元素` [	](spring_20200824063336943)
+ 作用：配置文件的根元素，该元素下的所有属性，单个`<bean>`也能指定
+ 属性：
  1. `default-lazy-init`:{{c1:: 是否延时初始化，也就是第一次调用`ctx.getBean()`才初始化 }}
  2. `default-merge`:TODO
  3. `default-autowire`:{{c1:: 进行自动装配 }}
  4. `default-autowire-candidates`:{{c1:: 将指定`<bean>`设置为不进行自动装配 }}
  5. `default-init-method`:{{c1:: 指定初始化方法 }}
  6. `default-destroy-method`:{{c1:: 指定销毁方法 }}


### 为`<bean>`指定别名 [	](spring_20200824063336945)

+ 指定单个别名:{{c1:: `<bean id="" class="..." alias="singleAlias">` }}
+ 指定多个个别名:{{c1:: `<bean id="" class="..." name="#aaa,@bbb">` }}

### 容器中Bean的作用域 [	](spring_20200824063336947)
+ 基本作用域：
  1. {{c1:: `singleton` }}
  2. {{c1:: `prototype` }}
+ web作用域：
  1. {{c1:: `request` }}
  2. {{c1:: `session` }}
  3. {{c1:: `application` }}
  4. {{c1:: `websocket` }}
+ 注意在非springMVC应用使用web作用域需配置`web.xml`
  ```xml
    <!-- {{c1:: -->
    <listener>
      <listener-class>xxx.RequestContextListener</listenner-class>
    </listener>
    <!-- }} -->
  ```

### 自动装配：`default-autowire`与`autowire`属性的值： [	](spring_20200824063336949)

1. `no`：{{c1:: 不使用自动装配 }}
2. `byName`：{{c1:: 根据setter方法查找匹配的id的`bean` }}
3. `byType`：{{c1:: 根据setter方法型参类型查找`bean` }}
4. `constructor`：{{c1:: 根据构造方法型参类型查找`bean` }}
5. `autodetect`：{{c1:: 根据当前bean的结构，自动选择byType或者constructor }}

### 组合属性 [	](spring_20200824063336951)

+ 驱动Spring调用`exampleBean的getPerson().setName()`方法
  ```xml
    <!-- 以"孙悟空"作为参数 -->
    <!-- {{c1:: -->
    <property name="person.name" value="孙悟空"/>
    <!-- }} -->
  ```
### spring的java配置管理 [	](spring_20200824063336955)

+ 使用java类配置spring时的常用注解：
  + `@Configuration`:{{c1:: 修饰**java配置类** }}
  + `@Bean`:{{c1:: 修饰**方法**，代表一个Bean }}
  + `@Value`:{{c1:: 修饰**成员变量**，相当于配置了一个变量 }}
  + `@Import`:{{c1:: 修饰**java配置类**，向当前配置类导入其他java配置类 }}
  + `@Scope`:{{c1:: 修饰**方法**，指定bean生命周期 }}
  + `@Lazy`:{{c1:: 修饰**方法**，开启bean延时初始化 }}
  + `@DependsOn`:{{c1:: 修饰**方法**，在指定bean之后初始化当前bean }}
  + `@EnableAspectJAutoProxy`：{{c1:: 修饰类，启用aop增强处理 }}
  + `@EnableTransactionManagement`: {{c1:: 修饰类，开启声明式事务 }}
+ 以配置文件为主，加入java配置类，配置spring
  ```xml
  <!-- {{c1:: -->
    <bean class="top.xieyun.app.config.AppConfig">
  <!-- }} -->
  ```
+ 以java类文件为主，加入xml配置文件，配置spring
  ```java
    //{{c1::
    @Configuration
    @importResource("classpath:/beans.xml")
    pbulic class MyConfig{
      ....
    }
    //}}
  ```

### 抽象Bean与子Bean [	](spring_20200824063336958)

  + 重要的2个属性：`abstract` `parent`
  + 例子：
    ```xml
    <!-- {{c1:: -->
    <!-- 指定abstract="true"定义抽象Bean -->
    <bean id="personTemplate" abstract="true">
      <property name="name" value="crazyit"/>
      <property name="axe" ref="steelAxe"/>
    </bean>
    <!-- 通过指定parent属性指定下面Bean配置可从父Bean继承得到配置信息 -->
    <bean id="chinese" class="Chinese" parent="personTemplate"/>
    <bean id="american" class="American" parent="personTemplate"/>
    <!-- }} -->
    ```

### `<lookup-method>`注入 [	](spring_20200824063336960)

+ 使用原因：{{c1:: 当`singleton Bean` 依赖 `prototype Bean`时，`prototype bean`变成`singleton bean`问题 }}
+ 作用：{{c1:: 自定义抽象方法，然后交给spring容器实现 }}
+ 使用步骤：
  1. {{c1:: 将`singletonBean`定义为抽象类,以及定义抽象方法 }}
  2. 定义Bean的子元素：{{c1:: `<lookup-method name="" bean="">` }}
     1. `name`:{{c1:: 抽象方法名（注意是全名） }}
     2. `bean`:{{c1:: 需要注入的bean id }}

## 使用spring配置文件调用getter方法，普通方法，访问类或对象的Field [	](spring_20200824063336962)

### 使用spring配置文件，调用getter方法 [	](spring_20200824063336964)
  + 工厂类：{{c1:: `PropertyPathFactoryBean` }}
  + 普通配置：{{c1:: `<bean class="PropertyPathFactoryBean" p:targetBeanName="person" p:peropertyPath="son.age" />` }}
  + id简化例配置：{{c1:: `<bean id="person.son.age" class="PropertyPathFactoryBean" />` }}
  + 命名空间简化配置：{{c1:: `<util:property-path id="theAge" path="person.son.age" />` }}

### 使用spring配置文件，访问类或对象的静态Field [	](spring_20200824063336967)
  + 工厂类：{{c1:: `FieldRetrievingFactoryBean` }}
  + 普通配置：{{c1:: `<bean class="FieldRetrievingFactoryBean" p:targetClass="java.sql.Connection" p:targetField="TRANSACTION_SERIALIZABLE" />` }}
  + 简化配置：{{c1:: `<bean class="FieldRetrievingFactoryBean" p:staticField="java.sql.Connection.TRANSACTION_SERIALIZABLE" />` }}
  + id简化配置：{{c1:: `<bean id="java.sql.Connection.TRANSACTION_SERIALIZABLE" class="FieldRetrievingFactoryBean"/>` }}
  + 命名空间简化配置：{{c1:: `<util:constant id="theAge1" static-field="java.sql.Connection.TRANSACTION_SERIALIZABLE" />` }}

### 使用spring配置文件调用，静态或者实例方法：MethodInvokingFactoryBean [	](spring_20200824063336969)
  + 常用4个property调用
    1. {{c1:: `setTargetClass(String targetClass)`:调用哪个类 }}
    2. {{c1:: `setTargetObject(Object targetObject)`:调用哪个对象 }}
    3. {{c1:: `setTargetMethod(Method targetMethod)`:调用哪个方法 }}
    4. {{c1:: `setArguments(Object[] arguments)`:调用方法的参数 }}


## 基于XML Schema的简化配置方式 [	](spring_20200911094545277)

### 使用p:命名空间简化配置 [	](spring_20200911094545281)
```xml
<!-- {{c1:: -->
<bean id="chinese" class="top.xieyun.service.impl.Chinese"
    p:age="29" p:axe-ref="stoneAxe"/>
<!-- }} -->
```

### 使用c:命名空间简化配置 [	](spring_20200911094545284)
+ 需配置代码：
```java
public class Person
{
  private String name;
  private int age;
  @ConstructorProperties({"personName", "age"})
  public Person(String name, int age)
  {
    this.name = name;
    this.age = age;
  }
}
```
+ c:命名空间简化配置:
```xml
<!-- {{c1:: -->
  <bean id="person" class="top.xieyun.service.Person"
  c:age="500" c:personName="孙悟空"/>
<!-- }} -->
```
### 使用util:命名空间简化配置 [	](spring_20200911094545287)
  + `constant`：{{c1:: `<util:constant id="chin.age" static-field="java.sql.Connection.`TRANSACTION_SERIALIZABLE"/>}}
  + `property-path`:{{c1::`获取指定bean的getter方法，peropertyPathFacrotyBean的简化配置`}}
  + `list`：{{c1:: `<util:list id="chin.schools" list-class="java.util.LinkedList">`}}
  + `set`：{{c1:: `<util:set id="chin.axes" set-class="java.util.HashSet">`}}
  + `map`：{{c1:: `<util:map id="chin.scores" map-class="java.util.TreeMap">`}}
  + `properties`：{{c1:: `<util:properties id="confTest" location="classpath:test_zh_CN.properties"/>`}}
  + 注意：以上简化配置都有:{{c1:: `scope`属性 }}

## 使用注解配置spring [	](spring_20200911094545289)

### 标注`bean`的注解 [	](spring_20200911094545293)

+ 标注`bean`的注解
  1. {{c1::`@Component`：标注普通bean**类**}}
  2. {{c1::`@Controller`：标注控制器组件**类**}}
  3. {{c1::`@Service`：标注业务逻辑组件**类**}}
  4. {{c1::`@Repository`：标注DAO组件**类**}}
  + 注意以上都可以指定bean名称：{{c1::`@Component("person")`}}
+ 指定`bean`的作用域：{{c1:: `@Scope`,标注使用注解的组件**类** }}
+ 设置`bean`初始化顺序**注解**：{{c1:: `@DependsOn`,修饰**类** }}
+ 取消`singleton bean`预初始化**注解**:{{c1:: `@Lazy`,修饰**类** }}

### 代替`<lookup-method ../>`的注解 [	](spring_20200911094545295)

+ {{c1:: `@Lookup(value="beanId")`:标注执行lookup方法注入的**方法** }}

### 自动扫描Bean类注解配置 [	](spring_20200911094545298)

+ 自动扫描指定包及其子包下的所有Bean类 ：{{c1::`<context:component-scan base-package="top.xieyun.service"/>`}}
+ 2个过滤器子元素:
  1. {{c1:: `<context:include-filter type="regex" expression=".*Chinese"/>` }}
  2. {{c1:: `<context:exclude-filter type="regex" expression=".*Axe"/>` }}
+ 过滤器类型：
  1. {{c1:: anotation }}
  2. {{c1:: assignable }}
  3. {{c1:: regex }}
  4. {{c1:: aspectj }}

### 使用注解配置依赖注入 [	](spring_20200911094545301)

+ 相当于`<property .../>`元素的value属性
  + 注解：{{c1:: `@Value`,可修饰setter,实例变量 }}
+ 相当于`<property .../>`元素的ref属性
  + 注解：{{c1:: `@Resource`,可修饰setter,实例变量 }}

### 使用注解定制生命周期行为 [	](spring_20200911094545303)

+ 相当于`<bean>`元素的`init-method`属性
  + 注解：{{c1:: `@PostConstruct`,修饰方法 }}
+ 相当于`<bean>`元素的`destroy-method`属性
  + 注解：{{c1:: `@PreDestroy`,修饰方法 }}

### 自动装配与精准装配 [	](spring_20200911094545306)

+ 自动装配注解：{{c1:: `@Autowaired`, 可修饰方法，构造方法，成员实例变量，数组，集合,泛型变量 }}
+ 默认使用`byType`策略，出现多个相同类型的`<bean>`时
  
  + 指定主候选`<bean>`：{{c1::`@Primary 指定类`}}
+ 精准装配(意义不大，等价于使用`@Resource`):
  ```java
    //{{c1::
    @Autowired
    @Qualifier("steelAxe")
    private Axe axe;
    //}}
  ```

### 使用@Autowaired自动装配时找不到`bean`时的解决方案： [	](spring_20200911094545309)
1. 指定@Autowired属性：{{c1:: `@Autowired(required = false)` }}
2. 使用注解：{{c1:: `@Nullable`,指定方法形参，成员实例变量 }}

### @NonNull,@Nullable，@NonNullFields，@NonNullApi [	](spring_20200911094545312)

+ `@NonNull`:{{c1:: 使用在**字段**，**方法参数**或**方法的返回值**。表示不能为空 }}
+ `@Nullable`:{{c1:: 使用在**字段**，**方法参数**或**方法的返回值**。表示可以为空。 }}
+ `@NonNullFields`:{{c1:: 使用在**包级别**，并且是该包下类的**字段**不能为空。 }}
  
  + 使用条件：{{c1:: 必须先定义一个名为`package-info.java` }}
+ `@NonNullApi`:{{c1:: 使用在**包级别**，该包下的类的**方法参数**和**返回值**不能为空 }}
  
  + 使用条件：{{c1:: 必须先定义一个名为`package-info.java` }}
+ `package-info.java`文件：
  ```java
  //{{c1::
    @NonNullApi
    @NonNullFields
    package org.springframework.mail;
    import org.springframework.lang.NonNullApi;
    import org.springframework.lang.NonNullFields;
  //}}
  ```

## 资源访问 [	](spring_20200911094545315)

### Resouce的常用实现类 [	](spring_20200911094545317)
+ 常用的资源访问前缀：
  1. {{c1:: `http:` }}
  2. {{c1:: `ftp:` }}
  3. {{c1:: `file:` }}
  4. {{c1:: `classpath:` }}
    + 注意：{{c1:: `classpath*:bean*.xml`可以搜索指定路径下的符合文件名的所有文件 }}
| 实现类                 | 说明                           |
| ---------------------- | ------------------------------ |
| `ClassPathResource`      | {{c1:: 过类路径获取资源文件         }}|
| `FileSystemResource`     | {{c1:: 过文件系统获取资源           }}|
| `UrlResource`            | {{c1:: 过URL地址获取资源            }}|
| `ByteArrayResource`      | {{c1:: 取字节数组封装的资源         }}|
| `ServletContextResource` | {{c1:: 取ServletContext环境下的资源 }}|
| `InputStreamResource`    | {{c1:: 取输入流封装的资源           }}|
+ 通常建议使用`ByteArrayResource`代替`ServletContextResource`

### Resource接口 [	](spring_20200911094545321)

+ 常用方法
  | 方法             | 说明                                                         |
  | ---------------- | ------------------------------------------------------------ |
  | `exists()`         | {{c1:: 判断资源是否存在，true表示存在。                             }}|
  | `isReadable()`     | {{c1:: 判断资源的内容是否可读。需要注意的是当其结果为true的时候，其内容未必真的可读，但如果返回false，则其内容必定不可读。 }}|
  | `isOpen()`         | {{c1:: 判断当前Resource代表的底层资源是否已经打开，如果返回true，则只能被读取一次然后关闭以避免资源泄露；该方法主要针对于InputStreamResource，实现类中只有它的返回结果为true，其他都为false。 }}|
  | `getURL()`         | {{c1:: 返回当前资源对应的URL。如果当前资源不能解析为一个URL则会抛出异常。如ByteArrayResource就不能解析为一个URL。 }}|
  | `getURI()`         | {{c1:: 返回当前资源对应的URI。如果当前资源不能解析为一个URI则会抛出异常。 }}|
  | `getFile()`        | {{c1:: 返回当前资源对应的File。                                     }}|
  | `contentLength()`  | {{c1:: 返回当前资源内容的长度。                                     }}|
  | `getFilename()`    | {{c1:: 获取资源的文件名。                                           }}|
  | `getDescription()` | {{c1:: 返回当前资源底层资源的描述符，通常就是资源的全路径（实际文件名或实际URL地址）。 }}|
  | `getInputStream()` | {{c1:: 获取当前资源代表的输入流。除了InputStreamResource实现类以外，其它Resource实现类每次调用getInputStream()方法都将返回一个全新的InputStream。 }}|

### `ctx.getResource(String location)`方法 [	](spring_20200911094545324)

+ 作用：{{c1:: 可以使用前缀直接访问资源 }}
+ 传给普通Bean：{{c1:: 可以使用`ResourceLoaderAware`间接将`ctx`作为`ResourceLoader`传给`Bean` }}

### 使用Resource作用属性 [	](spring_20200911094545327)
+ 使用Resource作为普通Bean属性后可以通过资源访问前缀使用如下配置获取资源
  ```xml
    <!-- {{c1:: -->
    <bean id="test" class="TestBean" p:resource="classpath:book.xml" />
    <!-- }} -->
  ```

### AOP的基本概念 [	](spring_20200911094545329)

+ `Aspect`:{{c1:: 切面，用于组织多个`Advice,Advice`在切面中定义 }}
+ `Joinpoint`:{{c1:: 程序执行中明确的点，在`spring AOP`中总是**方法的调用** }}
+ `Advice`:{{c1:: 增强处理，有`around,before,after`等类型 }}
+ `Pointcut`:{{c1:: 切入点，可以插入增强处理的连接点。 }}
+ 引入：{{c1:: 将方法或字段添加到被处理的类中 }}
+ 目标对象：{{c1:: 被增强处理的对象。 }}


### 开启spring中AspectJ支持 [	](spring_20200911094545332)

+ 需要使用xml配置方式
```xml
  <!-- 启动@AspectJ支持 -->
<!-- {{c1:: }} -->
  <aop:aspectj-autoproxy/>
<!-- }} -->
```
+ 不需要xml配置方式
```xml
<!-- {{c1:: -->
  <bean class= 'xxx.AnnotationAwareAspectJAutoProxyCreator' />
<!-- }} -->
```


### AOP配置声明  [	](spring_20201115084450644)
```xml
<!-- {{c1:: -->
  <aop:config>
    <!--切入点-->
    <aop:pointcut id="p" expression="* top.xieyun.service.impl.*.*(..))"/>
    <!--配置切面-->
    <aop:aspect ref="proxyBean">
      <!--增强作用在具体的方法上-->
      <aop:before method="before" pointcut-ref="p"/>
    </aop:aspect>
  </aop:config>
<!-- }} -->
```
### 基于注解的AOP配置 [	](spring_20200911094545336)
+ 定义切面:{{c1:: `@Aspect` }}
+ 5种advice:{{c1:: `Before,AfterReturning(成功),AfterThrowing(失败),After(无论),around` }}
+ 5种advice使用例子:
  ```java
    //{{c1::
    @Before("execution(* top.xieyun.service.impl.*.*(..))")
    public void authority()
    {}

    @AfterReturning(returning = "rvt",
      pointcut = "execution(* top.xieyun.service.impl.*.*(..))")
    public void log(Object rvt)
    {}

    @AfterThrowing(throwing = "ex",
      pointcut = "execution(* top.xieyun.service.impl.*.*(..))")
    public void doRecoveryActions(Throwable ex)
    {}

    @After("execution(* top.xieyun.service.*.*(..))")
    public void release()
    {}

    @Around("execution(* top.xieyun.service.impl.*.*(..))")
    public Object processTx(ProceedingJoinPoint jp)
      throws java.lang.Throwable
    {}
    //}}
  ```

### 访问目标方法方式 [	](spring_20200911094545339)

+ 定义增强处理方法时:{{c1:: 将第一个参数定义为`JoinPoint`类型 }}
  
  + 注意:{{c1:: `Around`只能定义为`proceedingJoinPoint`类型 }}
+ 使用args表达式
  ```java
    //{{c1::
    // 下面的args(arg0, arg1)会限制目标方法必须有2个形参
    @AfterReturning(returning = "rvt", pointcut =
      "execution(* top.xieyun.service.impl.*.*(..)) && args(arg0, arg1)")
    // 此处指定arg0、arg1为String类型
    // 则args(arg0, arg1)还要求目标方法的两个形参都是String类型
    public void access(Object rvt, String arg0, String arg1)
    {
      System.out.println("调用目标方法第1个参数为:" + arg0);
      System.out.println("调用目标方法第2个参数为:" + arg1);
      System.out.println("获取目标方法返回值:" + rvt);
      System.out.println("模拟记录日志功能...");
    }
    //}}
  ```

### JoinPoint对象API [	](spring_20200911094545342)

| 方法名                    | 功能                                                         |
| ------------------------- | ------------------------------------------------------------ |
|  `Signature getSignature(); `| {{c1:: 获取封装了署名信息的对象,在该对象中可以获取到目标方法名,所属类的Class等信息 }}|
|  `Object[] getArgs();`| {{c1:: 获取传入目标方法的参数对象                                   }}|
|  `Object getTarget();`| {{c1:: 获取被代理的对象                                             }}|
|  `Object getThis();`| {{c1:: 获取代理对象                                                 }}|


### 指定切面类的优先级（执行顺序）2种方法： [	](spring_20200911094545346)

+ {{c1:: 让切面类实现Ordered接口,该接口具有一个返回整数的方法 }}
+ {{c1:: 使用@Order注解修饰一个切面类 }}

### 定义切入点 [	](spring_20201017075500728)
+ 定义切入点：
```java
  //{{c1::
  @Pointcut("execution(* transfer(..)))
  private void myPontcut(){}
  //}}
```
+ 引用已有切入点
```java
    //{{c1::
    //引用本类
    @AfterReturning(pointcut = "myPontcut()",returning = "rvt")
    //引用其他类
    @AfterReturning(pointcut = "SystemArchitecture.myPointcut()",returning = "rvt")
    public void writelog(Object rvt){...}
    //}}
```

### 切入点指示符：execution [	](spring_20201017075500732)

+ 表达式：`execution(* com.test.method.des..*.*(..))`
+ 解释如下：
  1. {{c1:: `execution()`表达式的主体 }}
  2. {{c1:: 第一个`*`符号表示返回值的类型任意 }}
  3. {{c1:: `com.test.method.des`AOP所切的服务的包名，即，需要进行横切的业务类 }}
  4. {{c1:: 包名后面的“..”表示当前包及子包 }}
  5. {{c1:: 第二个`*`表示类名，`*`即所有类 }}
  6. {{c1:: `.*(..)`表示任何方法名，括号表示参数，两个点表示任何参数类型 }}
+ 通配符的使用：
  + `*`:{{c1:: 匹配单个任意参数 }}
  + `..`:{{c1:: 匹配多个任意参数 }}
  + 例:{{c1:: `(*,String)` }}

### 切入点指示符：within [	](spring_20201017075500734)

+ 作用：{{c1:: 用于匹配特定类型的连接点,spring中为方法的执行 }}
+ 例：
  + 匹配指定包中任意连接点：{{c1:: `within(top.xieyun.service.*)` }}
  + 匹配指定**包及其子包**中任意连接点：{{c1:: `within(top.xieyun.service..*)` }}

### 切入点指示符：this target args bean @annotation [	](spring_20201017075500736)

+ 匹配实现指定类型的目标对象所有连接点：{{c1:: `target(top.xieyun.myService)` }}
+ 匹配实现指定类型的代理对象所有连接点：{{c1:: `this(top.xieyun.myService)` }}
+ 对方法参数类型以及个数进行限制：{{c1:: `args(java.io.Serializable)` }}
+ 匹配所有名字以Service bean的连接点：{{c1:: `bean("*Service")` }}
+ 匹配标注了指定注解的连接点：{{c1:: `@annotation(operateLog)` }}
+ 逻辑运算符：{{c1:: `&& || !` }}


## spring缓存机制 [	](spring_20201017075500740)

### 启用spring缓存 [	](spring_20201017075500742)

+ 使用注解：{{c1::`<cache:annotation-driven cache-manager="缓存管理器ID"/>` }}
  +  cache-manager属性默认值为:{{c1:: cacheManager }}


### 配置spring内置缓存实现的配置 [	](spring_20201017075500744)
+ 概况：
  + spring内置缓存管理器类:{{c1:: `SimpleCacheManager` }}
  + 作为缓存区的类:{{c1:: `ConcurrentMapCacheFactoryBean` }}
+ 配置如下：
  ```xml
  <!-- {{c1:: -->
  <bean id="cacheManager" class=
    "org.springframework.cache.support.SimpleCacheManager">
    <property name="caches">
      <set>
        <bean class=
        "org.springframework.cache.concurrent.ConcurrentMapCacheFactoryBean"
        p:name="default"/>
        <bean class=
        "org.springframework.cache.concurrent.ConcurrentMapCacheFactoryBean"
        p:name="users"/>
      </set>
    </property>
  </bean>
  <!-- }} -->
  ```

### spring内置EhCache缓存实现的配置 [	](spring_20201017075500746)

+ 概况：{{c1:: `EhCacheCacheManager`缓存管理器包装`EhCacheManagerFactoryBean`生成的对象 }}
```xml
  //{{c1::
  <bean id="ehCacheManager"
    class="org.springframework.cache.ehcache.EhCacheManagerFactoryBean"
    p:configLocation="classpath:ehcache.xml"
    p:shared="false" />
  <bean id="cacheManager"
    class="org.springframework.cache.ehcache.EhCacheCacheManager"
    p:cacheManager-ref="ehCacheManager" > 
  //}}
```

### `@Cacheable` 与 `@Cacheput` [	](spring_20201017075500748)

+ 作用：{{c1:: 修饰类与方法，以方法参数为key，将方法返回值放入缓存。 }}
+ 可指定属性：
  + `value`:{{c1:: 必须属性，指定缓冲区的名字 }}
    + 例：{{c1:: `@Cacheable("user")` }}
  + `key`:{{c1:: 指定缓存的key }}
    + 例：{{c1:: `@Cacheable(value="user",key="#name")` }}
  + `conditon`:{{c1:: 指定一个SpEl表达式，表达式为true时，缓存方法返回值 }}
    + 例：{{c1:: `@Cacheable("user",conditon="#age>100")` }}
  + `unless`:{{c1:: 指定一个SpEl表达式，表达式为false时，缓存方法返回值 }}
    + 例：{{c1:: `@Cacheable("user",unless="#age<100")` }}
+ `@Cacheable`与`@Cacheput`的区别：{{c1:: @Cacheput不会读取缓存，每次都会将方法返回值重新放到缓存区 }}

### @CacheEvict [	](spring_20201017075500750)
+ 作用：{{c1:: 修饰方法，可用于清除所有的缓存数据 }}
+ 可指定属性：
  + `value`:{{c1:: 必须属性，指定缓冲区的名字 }}
  + `allEntries`:{{c1::是否清空整个缓存区}}
  + `beforeInvocation`:{{c1::是否在执行方法之前清除缓存数据}}
  + `condition`:{{c1::指定一个SpEl表达式，表达式为true时，清除缓存}}
  + `key`:{{c1::清除指定key的缓存数据}}
+ 例：
  ```java
    //{{c1::
    @CacheEvict(value = "users", allEntries = true)
    public void evictAll()
    {
      System.out.println("--正在清空整个缓存--");
    }
    //}}
  ```
## spring jdbcTemplate [	](spring_20201017075500751)

### 配置JDBCTemplate对象 [	](spring_20201017075500753)
```xml
<!-- {{c1:: -->
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
  <!--注入 dataSource-->
  <property name="dataSource" ref="dataSource"></property>
</bean>
<!-- }} -->
```

### jdbcTemplate操作数据库：DML操作 [	](spring_20201017075500755)

+ `update(String sql,Object... args)`: {{c1:: {{c1:: DML操作方法签名 }} }}
+ `batchUpdate(String sql,List<Object[]> batchArgs)`: {{c1:: {{c1:: 批量DML操作方法签名 }} }}
+ 例：
```java
// {{c1::
  String sql = "insert into t_book values(?,?,?)";
  Object[] args = {book.getUserId(), book.getUsername(), book.getUstatus()};
  int update = jdbcTemplate.update(sql,args);

  String sql = "update t_book set username=?,ustatus=? where user_id=?";
  Object[] args = {book.getUsername(), book.getUstatus(),book.getUserId()};
  int update = jdbcTemplate.update(sql, args);

  String sql = "delete from t_book where user_id=?";
  int update = jdbcTemplate.update(sql, id);

  public void batchAddBook(List<Object[]> batchArgs) {
  String sql = "insert into t_book values(?,?,?)";
  int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
  System.out.println(Arrays.toString(ints));
}
//}}
```

### jdbcTemplate操作数据库：DQL操作 [	](spring_20201017075500757)

+ `queryForObject(String sql,Class<T> requiredType)`：{{c1:: 返回单个值方法签名 }}
+ `queryForObject(String sql,RowMapper<T> rowMapper,Object... args)`：{{c1:: 返回对象方法签名 }}
+ `query(String sql,RowMapper<T> rowMapper,Object... args)`：{{c1:: 返回集合方法签名 }}
+ `RowMapper`常用实例：{{c1:: `BeanPropertyRowMapper` }}
+ 例：
  ```java
      //{{c1::
      //返回单个值
      String sql = "select count(*) from t_book";
      Integer count = jdbcTemplate.queryForObject(sql, Integer.class);
      //返回对象
      String sql = "select * from t_book where user_id=?";
      Book book = jdbcTemplate.queryForObject(sql, new BeanPropertyRowMapper<Book>(Book.class), id);
      //返回集合
      String sql = "select * from t_book";
      List<Book> bookList = jdbcTemplate.query(sql, new 
      BeanPropertyRowMapper<Book>(Book.class));

      //自定义rowMapper
      String sql = "select name, gender from test_student where name = ?";
      Student student = this.jdbcTemplate.queryForObject(sql, new Object[]{name}, new RowMapper<Student>() {
          @Override
          public Student mapRow(ResultSet rs, int i) throws SQLException {
              Student s = new Student();
              s.setName(rs.getString("name"));
              s.setGender(rs.getString("gender"));
              return s;
          }
      });
      //}}
  ```

## spring的事务 [	](spring_20201017075500759)

### PlatformTransactionManager [	](spring_20201017075500761)
+ 作用：{{c1:: 提供一个接口，代表事务管理器，这个接口针对不同的框架提供不同的实现类 }}
+ 继承关系图：![image-20201017163325206](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201017163325206.png)

### spring注解声明式事务配置 [	](spring_20201017075500764)

1. 创建事务管理器
  ```xml
  <!-- {{c1:: -->
  <bean id="transactionManager" 
  class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
   <property name="dataSource" ref="dataSource"></property>
  </bean>
  <!-- }} -->
  ```
2. 引入{{c1::`tx`}}命名空间
3. 开始事务注解：{{c1:: `<tx:annotation-driven transactionManager="transactionManager"></tx:annotation-driven>` }}
4. 使用{{c1:: `@Transactional` }}声明事务

### spring XML声明式事务管理 [	](spring_20201017075500766)

+ 第一步 配置事务管理器
+ 第二步 配置通知
+ 第三步 配置切入点和切面
+ 代码：
  ```xml
  <!-- {{c1:: -->
  <!--1 创建事务管理器--> 
  <bean id="transactionManager" 
  class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <!--注入数据源-->
    <property name="dataSource" ref="dataSource"></property>
  </bean>

  <!--2 配置通知--> 
  <tx:advice id="txadvice">
    <!--配置事务参数-->
    <tx:attributes>
    <!--指定哪种规则的方法上面添加事务-->
    <tx:method name="accountMoney" propagation="REQUIRED"/>
    <!--<tx:method name="account*"/>-->
    </tx:attributes>
  </tx:advice>

  <!--3 配置切入点和切面--> 
  <aop:config>
    <!--配置切入点-->
    <aop:pointcut id="pt" expression="execution(* 
    com.atguigu.spring5.service.UserService.*(..))"/>
    <!--配置切面-->
    <aop:advisor advice-ref="txadvice" pointcut-ref="pt"/>
  </aop:config>
  <!-- }} -->
  ```

### @Transactional注解 [	](spring_20201017075500769)

+ 作用：
  + 修饰类:{{c1:: 如果把这个注解添加类上面，这个类里面所有的方法都添加事务 }}
  + 修饰方法:{{c1:: 如果把这个注解添加方法上面，为这个方法添加事务 }}
+ 属性：
  + `isolation`:{{c1:: 设置隔离级别}}
  + `noRollbackFor`:{{c1:: 遇到指定的异常时不回滚事务}}
  + `noRollbackForClassName`:{{c1:: 遇到指定的多个异常时不回滚事务}}
  + `propagation`:{{c1:: 指定事务的传播行为}}
  + `readOnly`:{{c1:: 是否只读}}
  + `rollbackFor`:{{c1:: 设置出现哪些异常进行回滚}}
  + `rollbackForClassName`:{{c1:: 设置出现哪些异常进行回滚，该属性可以指定多个}}
  + `timeout`:{{c1:: 事务超时时间}}

### spring事务管理：7种事务传播行为 [	](spring_20201017075500772)
+ 作用：{{c1:: 处理service层，事务方法之间的嵌套行为。 }}
1. `PROPAGATION_REQUIRED`：{{c1:: 如果当前没有事务，就创建一个新事务，如果当前存在事务，就加入该事务，该设置是最常用的设置。 }}
2. `PROPAGATION_SUPPORTS`：{{c1:: 支持当前事务，如果当前存在事务，就加入该事务，如果当前不存在事务，就以非事务执行。 }}
3. `PROPAGATION_MANDATORY`：{{c1:: 支持当前事务，如果当前存在事务，就加入该事务，如果当前不存在事务，就抛出异常。 }}
4. `PROPAGATION_REQUIRES_NEW`：{{c1:: 创建新事务，无论当前存不存在事务，都创建新事务。 }}
5. `PROPAGATION_NOT_SUPPORTED`：{{c1:: 以非事务方式执行操作，如果当前存在事务，就把当前事务挂起。 }}
6. `PROPAGATION_NEVER`：{{c1:: 以非事务方式执行，如果当前存在事务，则抛出异常。 }}
7. `PROPAGATION_NESTED`：{{c1:: 如果当前存在事务，则在嵌套事务内执行。如果当前没有事务，则执行与PROPAGATION_REQUIRED类似的操作。 }}

### Spring5核心容器支持函数式风格GenericApplicationContext [	](spring_20201017075500775)
```java
 // {{c1::
 GenericApplicationContext context = new GenericApplicationContext();
 context.refresh();
 context.registerBean("user1",User.class,() -> new User());
 User user = (User)context.getBean("user1");
//}}
```

### Spring5支持整合JUnit5 [	](spring_20201017075500777)
+ 创建spring测试类
  ```java
   //{{c1::
    @ExtendWith(SpringExtension.class)
    @ContextConfiguration("classpath:bean1.xml")
    public class JTest5 {
        @Autowired
        private UserService userService;
        @Test
        public void test1() {
            userService.accountMoney();
        }
    }
   //}}
  ```
+ 使用一个复合注解替代上面两个注解完成整合
  ```java
    //{{c1::
    @SpringJUnitConfig(locations = "classpath:bean1.xml")
    public class JTest5 {
        @Autowired
        private UserService userService;
        @Test
        public void test1() {
            userService.accountMoney();
        }
    }
    //}}
  ```

### spring整合mybatis配置： [	](spring_20201109090319136)
+ 主要思路：{{c1:: 通过配置SqlSessionFactoryBean类，加载mybaits配置文件和映射文件,替代原Mybatis工具类}}
+ 配置session工厂：
  ```xml
  <!-- {{c1:: -->
    <bean id="sqlSessionFactoryBeanID" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="configLocation" value="classpath:mybatis.xml"/>
        <property name="dataSource" ref="dataSource"/>
    </bean>
  <!-- }} -->
  ```

+ 扫描mapper组件：

  ```xml
  <!-- {{c1:: -->
  <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
    <property name="basePackage" value="org.mybatis.spring.sample.mapper" />
  </bean>
  <!-- }} -->
  ```

  

## spring MVC [	](spring_20201115082829623)

### javaWeb环境中使用spring [	](spring_20201115082829626)

+ 主要思路:{{c1:: 使用`ServletContextListener`创建`ApplicationContext`，将其存储到最大的域`servletContext`域 }}
+ 实际操作：
  1. 在web.xml中配置`ContextLoaderListener`监听器（导入spring-web坐标）
      ```xml
      <!-- {{c1:: -->
      <!--全局参数-->
      <context-param>
          <param-name>contextConfigLocation</param-name>
          <param-value>classpath:applicationContext.xml</param-value>
      </context-param>
      <!--Spring的监听器-->
      <listener>
        <listener-class>
            org.springframework.web.context.ContextLoaderListener
        </listener-class>
      </listener>
      <!-- }} -->
      ```
  2. servlet中使用`WebApplicationContextUtils`获得应用上下文对象`ApplicationContext`
     ```java
     //{{c1::
      ApplicationContext ctx = WebApplicationContextUtils.getWebApplicationContext(servletContext);
     //}}
     ```

### web.xml配置SpringMVC的核心控制器 [	](spring_20201115082829628)
```xml
<!-- {{c1:: -->
  <servlet>
      <servlet-name>DispatcherServlet</servlet-name>
      <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>  
      <init-param>
          <param-name>contextConfigLocation</param-name>
          <param-value>classpath:spring-mvc.xml</param-value>
      </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>   
      <servlet-name>DispatcherServlet</servlet-name>
      <url-pattern>/</url-pattern>
  </servlet-mapping>
<!-- }} -->
```

### @RequestMapping [	](spring_20201115082829631)

+ 作用：{{c1:: 用于建立请求 URL 和处理请求方法之间的对应关系 }}
+ 标注位置：
  + **类**:{{c1:: 请求URL的第一级访问目录。此处不写的话，就相当于应用的根目录 }}
  + **方法**:{{c1:: 请求 \URL的第二级访问目录，与类上的使用`@ReqquestMapping`标注的一级目录一起组成访问虚拟路径 }}
+ 属性：
  + `value`：{{c1:: 用于指定请求的URL。它和path属性的作用是一样的 }}
  + `method`：{{c1:: 用于指定请求的方式 }}
  + `params`：{{c1:: 用于指定限制请求参数的条件。它支持简单的表达式。要求请求参数的`key`和`value`必须和配置的一模一样 }}
+ 例如：
  + `params = {"accountName"}`：{{c1:: 表示请求参数必须有accountName }}
  + `params = {"moeny!100"}`：{{c1:: 表示请求参数中money不能是100 }}

### 配置内部资源视图解析器 [	](spring_20201115082829633)

+ 注意：{{c1:: 如果不在配置文件中配置视图解析器，就会使用`DispatcherServlet.properties`中的默认配置。 }}
```xml
 <!-- {{c1:: -->
  <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/views/"></property>
    <property name="suffix" value=".jsp"></property>
  </bean>
  <!-- }} -->
```
## SpringMVC的数据响应 [	](spring_20201115082829636)

### SpringMVC的数据响应方式 [	](spring_20201115082829638)

1. 页面跳转
  + 直接返回字符串
  + 通过ModelAndView对象返回
2. 回写数据 
  + 直接返回字符串
  + 返回对象或集合

### SpringMVC页面跳转：返回字符串 [	](spring_20201115082829641)

+ 作用：会将返回的字符串与视图解析器的前后缀拼接后跳转。
+ 返回带有前缀的字符串：
  + 转发：{{`forward:index.jsp`
  + 重定向：{{`redirect:index`
+ 例：{{c1:: ![image-20201113125111735](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201113125111735.png) }}

### SpringMVC页面跳转：返回ModelAndView对象 [	](spring_20201115082829643)

+ 主要思路：{{c1:: 使用`modelAndView.setViewName("viewName")`指定视图 }}
+ 例：
  ```java
    //{{c1::
    @RequestMapping("/quick2")
    public ModelAndView quickMethod2(){
      ModelAndView modelAndView = new ModelAndView();
      // modelAndView.setViewName("redirect:index.jsp");
      modelAndView.setViewName("forward:/WEB-INF/views/index.jsp");。
      return modelAndView;
    }
    //}}
  ```
### SpringMVC页面跳转：向request域存储数据 [	](spring_20201115082829646)
+ `request`方式:{{c1:: 通过SpringMVC框架注入的`request`对象`setAttribute()`方法设置 }}
+ `ModelAndView`方式：{{c1:: 通过`ModelAndView`的`addObject()`方法设置 }}
+ 例：
  ```java
  //{{c1::
  @RequestMapping("/quick")
  public String quickMethod(HttpServletRequest request){
    request.setAttribute("name","zhangsan");
    return "index";
  }

  @RequestMapping("/quick3")
  public ModelAndView quickMethod3(){
    ModelAndView modelAndView = new ModelAndView();
    modelAndView.setViewName("forward:/WEB-INF/views/index.jsp");
    modelAndView.addObject("name","lisi");
    return modelAndView;
  }
  //}}
  ```

### SpringMVC回写数据：直接返回字符串 [	](spring_20201115082829649)
+ 通过`response对象`:{{c1:: 通过SpringMVC框架注入的response对象，使用response.getWriter().print(“hello world”) 回写数据，此时不需要视图跳转，业务方法返回值为void。 }}
+ 通过`@ResponseBody`:{{c1:: 将需要回写的字符串直接返回，但此时需要通过@ResponseBody注解告知SpringMVC框架，方法返回的字符串不是跳转是直接在http响应体中返回。 }}
+ 例：
  ```java
    //{{c1::
    @RequestMapping("/quick4")
    public void quickMethod4(HttpServletResponse response) throws
    IOException {
      response.getWriter().print("hello world");
    }

    @RequestMapping("/quick5")
    @ResponseBody
    public String quickMethod5() throws IOException {
      return "hello springMVC!!!";
    }
    //}}
  ```

### SpringMVC回写数据：返回对象或集合 [	](spring_20201115082829651)

1. 需要开启注解驱动：{{c1:: `<mvc:annotation-driven/>` }}
2. 将对象或集合作为返回值：
  ```java
    //{{c1::
    @RequestMapping(value="/quick10")
    @ResponseBody
    //SpringMVC自动将User转换成json格式的字符串
    public User save10() throws IOException {
        User user = new User();
        user.setUsername("lisi2");
        user.setAge(32);
        return user;
    }
  //}}
  ```

## SpringMVC的请求 [	](spring_20201115082829654)
+ SpringMVC处理器方法可以接收如下类型的参数：
  + 基本类型参数：{{c1:: 参数名称要与请求参数的name一致，参数值会自动映射匹配。并且能自动做类型转换； }}
  + POJO类型参数：{{c1:: POJO参数的属性名与请求参数的name一致，参数值会自动映射匹配。 }}
  + 数组类型参数：{{c1:: 数组名称与请求参数的name一致，参数值会自动映射匹配。 }}
  + 集合类型参数：
    1. pojo参数作为集合：{{c1:: 获得集合参数时，要将集合参数包装到一个POJO中才可以 }}
      + 例：
        ```java
        //{{c1::
        // <input type="text" name="userList[0].username"><br/>
        // <input type="text" name="userList[0].age"><br/>
        // <input type="text" name="userList[1].username"><br/>
        // <input type="text" name="userList[1].age"><br/>

        @Data
        public class VO {
            private List<User> userList;
        }
        //...
        @RequestMapping(value="/quick14")
        @ResponseBody
        public void save14(VO vo) throws IOException {
          System.out.println(vo);
        }
        //}}
        ```
     2. `@RequestBody`使用：{{c1:: 当接受到一个json格式List数据的请求时，自动将请求体转换为相应的集合类型 }}
        + 例：
        ```java
          //{{c1::
          @RequestMapping("/quick13")
          @ResponseBody
          public void quickMethod13(@RequestBody List<User> userList) throws IOException {
            System.out.println(userList);
          }
          //}}
        ```

### 静态资源访问的开启(应用) [	](spring_20201115082829657)

+ 原因：{{c1:: SpringMVC的前端控制器DispatcherServlet的url-pattern配置的是/,代表对所有的资源都进行过滤操作 }}
+ 两种开启方式：
  + `<mvc:default-servlet-handler/>`：{{c1:: 对进入DispatcherServlet没有找到资源的URL进行筛查，如果发现是静态资源的请求，就将该请求转由Web应用服务器默认的Servlet处理 }}
  + `<mvc:resources mapping="/js/**"location="/js/"/> `：{{c1:: 由Spring MVC框架自己处理静态资源 }}

### springMVC请求数据乱码问题 [	](spring_20201115082829661)
+ 主要思路：{{c1:: 在web.xml中配置`CharacterEncodingFilter`过滤器，作用是设置`reqeuset`与`response`对象的编码 }}
+ 配置如下：
  ```xml
  <filter>
      <filter-name>CharacterEncodingFilter</filter-name>
      <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
      <init-param>
          <param-name>encoding</param-name>
          <param-value>UTF-8</param-value>
      </init-param>
  </filter>
  <filter-mapping>
      <filter-name>CharacterEncodingFilter</filter-name>
      <url-pattern>/*</url-pattern>
  </filter-mapping>
  ```
### @requestParam [	](spring_20201115082829664)

+ 作用：{{c1:: 当请求的**参数名称**与Controller的业务**方法参数名称**不一致时，就需要通过@RequestParam注解显示的绑定 }}
+ 属性：
  + `value`：{{c1:: 与请求参数名称 }}
  + `required`：{{c1:: 此在指定的请求参数是否必须包括，默认是true，提交时如果没有此参数则报错 }}
  + `defaultValue`：{{c1:: 当没有指定请求参数时，则使用指定的默认值赋值 }}
+ 例：
  ```java
  //{{c1::
    // <form action="${pageContext.request.contextPath}/quick14" // method="post">
    // <input type="text" name="name"><br>
    // <input type="submit" value="提交"><br>
    // </form>

  @RequestMapping("/quick14")
  @ResponseBody
  public void quickMethod14(@RequestParam("name") String username) throws IOException {
    System.out.println(username);
  }
  //}}
  ```
### Restful风格的参数 [	](spring_20201115082829666)

1. {{c1:: `GET`：用于获取资源 }}
2. {{c1:: `POST`：用于新建资源 }}
3. {{c1:: `PUT`：用于更新资源 }}
4. {{c1:: `DELETE`：用于删除资源 }}
+ 例如：
  1. {{c1:: `/user/1 GET `： 得到 id = 1 的 user }}
  2. {{c1:: `/user/1 DELETE`： 删除 id = 1 的 user }}
  3. {{c1:: `/user/1 PUT`： 更新 id = 1 的 user }}
  4. {{c1:: `/user POST`： 新增 user }}

### @PathVariable [	](spring_20201115082829669)

+ 作用：{{c1:: 读取指定占位符的值到请求处理方法形参。地址/user/1可以写成/user/{id}，占位符{id}对应的就是1的值。}}
+ 例：
  ```java
  //{{c1::
  @RequestMapping(value="/quick17/{name}")
  @ResponseBody
  public void save17(@PathVariable(value="name") String username) throws IOException {
        System.out.println(username);
  }
  //}}
  ```

### 自定义类型转换器 [	](spring_20201115082829671)

+ 作用：{{c1:: 映射字符串类型的请求参数到请求处理方法形参 }}
+ 开发步骤：
  1. 定义转换器类实现Converter接口:{{c1:: `implements Converter<String, Date>` }}
  2. 在配置文件中声明转换器类：{{c1:: `ConversionServiceFactoryBean` }}
  3. 在`<annotation-driven>`中指定属性引用转换器:{{c1:: `conversion-service`属性 }}
+ 例：
  1. 定义转换器类实现Converter接口
   ```java
   //{{c1::
  public class DateConverter implements Converter<String, Date> {
      public Date convert(String dateStr) {
          //将日期字符串转换成日期对象 返回
          SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd");
          Date date = null;
          try {
              date = format.parse(dateStr);
          } catch (ParseException e) {
              e.printStackTrace();
          }
          return date;
      }
  }
  //}}
   ```
  2. 在配置文件中声明转换器
  ```xml
  <!-- {{c1:: -->
    <bean id="converterService" class="org.springframework.context.support.ConversionServiceFactoryBean">
      <property name="converters">
          <list>
              <bean class="com.itheima.converter.DateConverter" />
          </list>
      </property>
    </bean>
  <!-- }} -->
  ```
  3. 在`<annotation-driven>`中引用转换器:{{c1::`<mvc:annotation-driven conversion-service="converterService"/>`}}
### 在请求处理方法获取原始ServletAPI [	](spring_20201115082829674)

+ 主要思路：{{c1:: SpringMVC支持使用原始ServletAPI对象作为控制器方法的参数进行注入}} 
+ 常用的对象如下：
  + {{c1:: `HttpServletRequest` }}
  + {{c1:: `HttpServletResponse` }}
  + {{c1:: `HttpSession` }}

### @RequestHeader，@CookieValue [	](spring_20201115082829676)

+ `@RequestHeader`
  + 作用：修饰请求处理**方法形参**,相当于`request.getHeader(name)`
  + 属性：
    + `value`：{{c1:: 请求头的名称 }}
    + `required`：{{c1:: 是否必须携带此请求头 }}
+ `@CookieValue`
  + 作用：修饰请求处理**方法形参**,获得指定Cookie的值
  + 属性：
    + `value`：{{c1:: 指定cookie的名称 }}
    + `required`：{{c1:: 是否必须携带此cookie }}

### 客户端文件上传三要素 [	](spring_20201115082829679)

1. {{c1:: 表单项`type=“file”` }}
2. {{c1:: 表单的提交方式是`post`   }}
3. {{c1:: 表单的`enctype`属性是多部分表单形式，及`enctype=“multipart/form-data”` }}
+ 例：
```html
<!-- {{c1:: -->
  <form action="${pageContext.request.contextPath}/user/quick22" method="post" enctype="multipart/form-data">
    名称<input type="text" name="username"><br/>
    文件1<input type="file" name="uploadFile"><br/>
    <input type="submit" value="提交">
  </form>
<!-- }} -->
```

### 文件上传原理(理解) [	](spring_20201115082829681)

+ `request.getParameter()`失效原因?
+ `application/x-www-form-urlencoded`与`Mutilpat/form-data`的区别?
+ 解释：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/5.jpg) }}

### springMVC文件上传步骤 [	](spring_20201115082829683)

+ 开发步骤：
  1. 导入fileupload和io坐标：{{c1:: `commons-fileupload` `commons-io` }}
  2. 配置文件上传解析器类：{{c1:: `CommonsMultipartResolver` }}
  3. 编写文件上传代码：{{c1:: `MultipartFile`作为形参 }}
+ 注意多文件上传：{{c1:: 将方法参数`MultipartFile`类型修改为`MultipartFile[]`即可 }}
+ 具体实现：
  1. 添加依赖
  ```xml
  <!-- {{c1:: -->
      <dependency>
        <groupId>commons-fileupload</groupId>
        <artifactId>commons-fileupload</artifactId>
        <version>1.3.1</version>
      </dependency>
      <dependency>
        <groupId>commons-io</groupId>
        <artifactId>commons-io</artifactId>
        <version>2.3</version>
      </dependency>
  <!-- }} -->
  ```
  2. 配置文件上传解析器
  ```xml
  <!-- {{c1:: -->
      <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <property name="defaultEncoding" value="UYF-8"/>
          <property name="maxUploadSize" value="500000"/>
      </bean>
  <!-- }} -->
  ```
  3. 后台程序
  ```java
  //{{c1::
      @RequestMapping(value="/quick22")
      @ResponseBody
      public void save22(String username, MultipartFile uploadFile) throws IOException {
        System.out.println(username);
          System.out.println(uploadFile);
      }
  //}}
  ```

## SpringMVC拦截器 [	](spring_20201115082829686)

### SpringMVC拦截器和Servlet Filter的区别 [	](spring_20201115082829689)

| 区别     | 过滤器                                                       | 拦截器                                                       |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 使用范围 | {{c1:: 是 servlet 规范中的一部分，任何Java Web 工程都可以使用 }} | {{c1:: 是 SpringMVC 框架自己的，只有使用了SpringMVC 框架的工程才能用 }} |
| 拦截范围 | {{c1:: 在 url-pattern 中配置了/*之后，可以对**所有要访问的资源**拦截 }} | {{c1:: 只会拦截**请求处理方法**，如果访问的是 `jsp，html,css,image` 或者 `js` 是不会进行拦截的 }} |

### 自定义springMVC拦截器 [	](spring_20201115082829692)
1. 创建拦截器类实现`HandlerInterceptor`接口
2. 配置拦截器:
  ```xml
  <!-- {{c1:: -->
    <mvc:interceptors>
        <mvc:interceptor>
            <!--对哪些资源执行拦截操作-->
            <mvc:mapping path="/**"/>
            <bean class="com.itheima.interceptor.MyInterceptor1"/>
        </mvc:interceptor>
    </mvc:interceptors>
  <!-- }} -->
  ```
3. 拦截器的拦截效果：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201113162620.png) }}
+ 注意拦截器执行顺序：{{c1:: 多个拦截器情况下，配置在前的先执行，配置在后的后执行 }}

### HandlerInterceptor接口方法 [	](spring_20201115082829695)
| 方法                | 说明                                                         |
| :------------------ | :----------------------------------------------------------- |
| `boolean preHandle()`       | {{c1:: 方法将在请求处理之前进行调用，该方法的返回值是布尔值Boolean类型的，当它返回为false 时，表示请求结束，后续的Interceptor 和Controller 都不会再执行；当返回值为true 时就会继续调用下一个Interceptor 的preHandle 方法 }} |
| `void postHandle()`      | {{c1:: 该方法是在当前请求进行处理之后被调用，前提是preHandle 方法的返回值为true 时才能被调用，且它会在DispatcherServlet 进行视图返回渲染之前被调用，所以我们可以在这个方法中对Controller 处理之后的ModelAndView 对象进行操作 }} |
| `void afterCompletion()` | {{c1:: 该方法将在整个请求结束之后，也就是在DispatcherServlet 渲染了对应的视图之后执行，前提是preHandle 方法的返回值为true 时才能被调用 }} |

### SpringMVC异常处理机制 [	](spring_20201115082829697)
+ 主要思路：{{c1:: 系统的Dao、Service、Controller出现都通过throws Exception向上抛出，最后由SpringMVC前端控制器交由异常处理器进行异常处理 }}
+ 异常处理的两种方式
  1. {{c1:: 使用Spring MVC提供的简单异常处理器`SimpleMappingExceptionResolver` }}
  2. {{c1:: 实现Spring的异常处理接口`HandlerExceptionResolver`然后配置成`Bean` }}
+ 例：
  + 简单异常处理器:
  ```xml
  <!-- {{c1:: -->
    <bean class=“org.springframework.web.servlet.handler.SimpleMappingExceptionResolver”>    <property name=“defaultErrorView” value=“error”/>
        <property name=“exceptionMappings”>
            <map>	
                <entry key="com.itheima.exception.MyException" value="error"/>
                <entry key="java.lang.ClassCastException" value="error"/>
            </map>
        </property>
    </bean>
  <!-- }} -->
  ```
  + 自定义异常处理:
    ```java
    //{{c1::
      public class MyExceptionResolver implements HandlerExceptionResolver {
        @Override
        public ModelAndView resolveException(HttpServletRequest request, 
            HttpServletResponse response, Object handler, Exception ex) {
            //处理异常的代码实现
            //创建ModelAndView对象
            ModelAndView modelAndView = new ModelAndView(); 
            modelAndView.setViewName("exceptionPage");
            return modelAndView;
        }
      }
      //<bean id="exceptionResolver" class="com.itheima.exception.MyExceptionResolver"/>
    //}}
    ```