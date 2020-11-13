<!-- @format -->

# Spring 集成 web 环境

### 导入 Spring 集成 web 的坐标

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-web</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
```

### 配置 ContextLoaderListener 监听器

```xml
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
```

### 通过工具获得应用上下文对象

```java
ApplicationContext applicationContext =
    WebApplicationContextUtils.getWebApplicationContext(servletContext);
Object obj = applicationContext.getBean("id");
```

# SpringMVC 快速入门

### **开发步骤**

1. 导入 SpringMVC 相关坐标

2. 配置 SpringMVC 核心控制器 DispathcerServlet

3. 创建 Controller 类和视图页面

4. 使用注解配置 Controller 类中业务方法的映射地址

5. 配置 SpringMVC 核心文件 spring-mvc.xml

6. 客户端发起请求测试

### **代码实现**

#### 导入 Spring 和 SpringMVC 的坐标、导入 Servlet 和 Jsp 的坐标

    ```xml
    <!--Spring坐标-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.0.5.RELEASE</version>
    </dependency>
    <!--SpringMVC坐标-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.0.5.RELEASE</version>
    </dependency>
    <!--Servlet坐标-->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>servlet-api</artifactId>
        <version>2.5</version>
    </dependency>
    <!--Jsp坐标-->
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>jsp-api</artifactId>
        <version>2.0</version>
    </dependency>

````

#### 在web.xml配置SpringMVC的核心控制器

```xml
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
```

#### 创建 Controller 和业务方法

```java
public class QuickController {
    public String quickMethod(){
        System.out.println("quickMethod running.....");
        return "index";
    }
}
```

#### 创建视图页面 index.jsp

    ```jsp
    <html>
    <body>
        <h2>Hello SpringMVC!</h2>
    </body>
    </html>
    ```

#### 配置注解

```java
    @Controller
    public class QuickController {
        @RequestMapping("/quick")
        public String quickMethod(){
            System.out.println("quickMethod running.....");
                return "index";
        }
    }
```

#### 创建 spring-mvc.xml

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/mvc
    http://www.springframework.org/schema/mvc/spring-mvc.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd">
    <!--配置注解扫描-->
    <context:component-scan base-package="com.itheima"/>
</beans>
```

#### 访问测试地址
+ http://localhost:8080/itheima_springmvc1/quick