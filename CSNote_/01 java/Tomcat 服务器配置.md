# Tomcat 服务器配置

Tomcat 服务器的配置主要集中于 tomcat/conf 下的 catalina.policy、catalina.properties、context.xml、server.xml、tomcat-users.xml、web.xml 文件；

# server.xml

server.xml 是tomcat 服务器的核心配置文件，包含了Tomcat的 Servlet 容器（Catalina）的所有配置。由于配置的属性特别多，我们在这里主要讲解其中的一部分重要配置：

## **Server**

Server是server.xml的根元素，用于创建一个Server实例，默认使用的实现类是org.apache.catalina.core.StandardServer；

```markup
<Server port="8005" shutdown="SHUTDOWN">
...
</Server>
123
```

port : Tomcat 监听的关闭服务器的端口。

shutdown： 关闭服务器的指令字符串。

Server内嵌的子元素为 Listener、GlobalNamingResources、Service。

默认配置的5个Listener 的含义：

```markup
<!‐‐ 用于以日志形式输出服务器 、操作系统、JVM的版本信息 ‐‐>
<Listener className="org.apache.catalina.startup.VersionLoggerListener"/>

<!‐‐ 用于加载（服务器启动） 和 销毁 （服务器停止） APR。 如果找不到APR库， 则会输出日志， 并不影响Tomcat启动 ‐‐>
<Listener className="org.apache.catalina.core.AprLifecycleListener" SSLEngine="on" />

<!‐‐ 用于避免JRE内存泄漏问题 ‐‐>
<Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener" />

<!‐‐ 用户加载（服务器启动） 和 销毁（服务器停止） 全局命名服务 ‐‐>
<Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />

<!‐‐ 用于在Context停止时重建Executor 池中的线程， 以避免ThreadLocal 相关的内存泄漏 ‐‐>
<Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />
1234567891011121314
```

GlobalNamingResources 中定义了全局命名服务：

```markup
<!‐‐ Global JNDI resources
Documentation at /docs/jndi‐resources‐howto.html
‐‐>
<GlobalNamingResources>
<!‐‐ Editable user database that can also be used by
UserDatabaseRealm to authenticate users
‐‐>
	<Resource name="UserDatabase" auth="Container"
	type="org.apache.catalina.UserDatabase"
	description="User database that can be updated and saved"
	factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
	pathname="conf/tomcat‐users.xml" />
</GlobalNamingResources>
12345678910111213
```

## Service

该元素用于创建 Service 实例，默认使用 org.apache.catalina.core.StandardService。默认情况下，Tomcat 仅指定了Service 的名称， 值为 “Catalina”。Service 可以内嵌的元素为 ： Listener、Executor、Connector、Engine，其中 ： Listener 用于为Service添加生命周期监听器， Executor 用于配置Service 共享线程池，Connector 用于配置Service 包含的链接器， Engine 用于配置Service中链接器对应的Servlet 容器引擎。

```markup
<Service name="Catalina">
...
</Service>
123
```

一个Server服务器，可以包含多个Service服务；

## Executor

默认情况下，Service 并未添加共享线程池配置。 如果我们想添加一个线程池， 可以在下添加如下配置：

```markup
<Executor name="tomcatThreadPool"
	namePrefix="catalina‐exec‐"
	maxThreads="200"
	minSpareThreads="100"
	maxIdleTime="60000"
	maxQueueSize="Integer.MAX_VALUE"
	prestartminSpareThreads="false"
	threadPriority="5"
	className="org.apache.catalina.core.StandardThreadExecutor"/>
123456789
```

属性说明：

| 属性                    | 含义                                                         |
| ----------------------- | ------------------------------------------------------------ |
| name                    | 线程池名称，用于 Connector中指定                             |
| namePrefix              | 所创建的每个线程的名称前缀，一个单独的线程名称为namePrefix+threadNumber |
| maxThreads              | 池中最大线程数                                               |
| minSpareThreads         | 活跃线程数，也就是核心池线程数，这些线程不会被销毁，会一直存在 |
| maxIdleTime             | 线程空闲时间，超过该时间后，空闲线程会被销毁，默认值为6000（1分钟），单位毫秒 |
| maxQueueSize            | 在被执行前最大线程排队数目，默认为Int的最大值，也就是广义的无限。除非特殊情况，这个值不需要更改，否则会有请求不会被处理的情况发生 |
| prestartminSpareThreads | 启动线程池时是否启动 minSpareThreads部分线程。默认值为false，即不启动 |
| threadPriority          | 线程池中线程优先级，默认值为5，值从1到10                     |
| className               | 线程池实现类，未指定情况下，默认实现类为org.apache.catalina.core.StandardThreadExecutor。如果想使用自定义线程池首先需要实现org.apache.catalina.Executor接口 |

JDK自带的jconsole.exe可以观察到线程数：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020041510260980.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3oxNzkwNDI0NTc3,size_16,color_FFFFFF,t_70)
如果不配置共享线程池，那么Catalina 各组件在用到线程池时会独立创建；

## Connector

Connector 用于创建链接器实例。默认情况下，server.xml 配置了两个链接器，一个支持HTTP协议，一个支持AJP协议。因此大多数情况下，我们并不需要新增链接器配置，只是根据需要对已有链接器进行优化：

```markup
<Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />
<Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />
12
```

属性说明：

1. port： 端口号，Connector 用于创建服务端Socket 并进行监听，以等待客户端请求链接。如果该属性设置为0，Tomcat将会随机选择一个可用的端口号给当前Connector使用；
2. protocol ： 当前Connector 支持的访问协议。默认为 HTTP/1.1 ，并采用自动切换机制选择一个基于 JAVA NIO 的链接器或者基于本地APR的链接器（根据本地是否含有Tomcat的本地库判定）；

如果不希望采用上述自动切换的机制， 而是明确指定协议， 可以使用以下值：
Http协议：

```java
org.apache.coyote.http11.Http11NioProtocol ， 非阻塞式 Java NIO 链接器
org.apache.coyote.http11.Http11Nio2Protocol ， 非阻塞式 JAVA NIO2 链接器
org.apache.coyote.http11.Http11AprProtocol ， APR 链接器
123
```

AJP协议 ：

```java
org.apache.coyote.ajp.AjpNioProtocol ， 非阻塞式 Java NIO 链接器
org.apache.coyote.ajp.AjpNio2Protocol ，非阻塞式 JAVA NIO2 链接器
org.apache.coyote.ajp.AjpAprProtocol ， APR 链接器
123
```

1. connectionTimeOut : Connector 接收链接后的等待超时时间， 单位为 毫秒。 -1 表示不超时；
2. redirectPort：当前Connector 不支持SSL请求， 接收到了一个请求， 并且也符合security-constraint 约束， 需要SSL传输，Catalina自动将请求重定向到指定的端口；
3. executor ： 指定共享线程池的名称， 也可以通过maxThreads、minSpareThreads等属性配置内部线程池；
4. URIEncoding : 用于指定编码URI的字符编码， Tomcat8.x版本默认的编码为 UTF-8 ,Tomcat7.x版本默认为ISO-8859-1；

完整的配置如下：

```markup
<Connector port="8080"
		protocol="HTTP/1.1"
		executor="tomcatThreadPool"
		maxThreads="1000"
		minSpareThreads="100"
		acceptCount="1000"
		maxConnections="1000"
		connectionTimeout="20000"
		compression="on"
		compressionMinSize="2048"
		disableUploadTimeout="true"
		redirectPort="8443"
		URIEncoding="UTF‐8" />
12345678910111213
```

## Engine

Engine 作为Servlet 引擎的顶级元素，内部可以嵌入： Cluster、Listener、Realm、Valve和Host；

```markup
<Engine name="Catalina" defaultHost="localhost">
...
</Engine>
123
```

属性说明：

1. name： 用于指定Engine 的名称， 默认为Catalina 。该名称会影响一部分Tomcat的存储路径（如临时文件）；
2. defaultHost ： 默认使用的虚拟主机名称， 当客户端请求指向的主机无效时， 将交由默认的虚拟主机处理， 默认为localhost；

## Host

Host 元素用于配置一个虚拟主机， 它支持以下嵌入元素：Alias、Cluster、Listener、Valve、Realm、Context。如果在Engine下配置Realm， 那么此配置将在当前Engine下的所有Host中共享。 同样，如果在Host中配置Realm ， 则在当前Host下的所有Context中共享。Context中的Realm优先级 > Host 的Realm优先级 > Engine中的Realm优先级。

```markup
<Host name="localhost" appBase="webapps" unpackWARs="true" autoDeploy="true">
...
</Host>
123
```

属性说明：

1. name: 当前Host通用的网络名称， 必须与DNS服务器上的注册信息一致。 Engine中包含的Host必须存在一个名称与Engine的defaultHost设置一致；
2. appBase： 当前Host的应用基础目录， 当前Host上部署的Web应用均在该目录下（可以是绝对目录，相对路径）。默认为webapps；
3. unpackWARs： 设置为true， Host在启动时会将appBase目录下war包解压为目录。设置为false， Host将直接从war文件启动；
4. autoDeploy： 控制tomcat是否在运行时定期检测并自动部署新增或变更的web应用；

通过给Host添加别名，我们可以实现同一个Host拥有多个网络名称，配置如下：

```markup
<Host name="www.web1.com" appBase="webapps" unpackWARs="true" autoDeploy="true">
	<Alias>www.web2.com</Alias>
</Host>
123
```

这个时候，我们就可以通过两个域名访问当前Host下的应用（需要确保DNS或hosts中添加了域名的映射配置）；

## Context

Context 用于配置一个Web应用，默认的配置如下：

```markup
<Context docBase="myApp" path="/myApp">
....
</Context>
123
```

属性描述：

1. docBase：Web应用目录或者War包的部署路径。可以是绝对路径，也可以是相对于Host appBase的相对路径；
2. path：Web应用的Context 路径。如果我们Host名为localhost， 则该web应用访问的根路径为： http://localhost:8080/myApp；

它支持的内嵌元素为：CookieProcessor， Loader， Manager，Realm，Resources，WatchedResource，JarScanner，Valve

```markup
<Host name="www.tomcat.com" appBase="webapps" unpackWARs="true" autoDeploy="true">
		<Context docBase="D:\servlet_project03" path="/myApp"></Context>
		<Valve className="org.apache.catalina.valves.AccessLogValve"
		directory="logs"
		prefix="localhost_access_log" suffix=".txt"
		pattern="%h %l %u %t &quot;%r&quot; %s %b" />
</Host>
1234567
```

# tomcat-users.xml

该配置文件中，主要配置的是Tomcat的用户，角色等信息，用来控制Tomcat中manager， host-manager的访问权限；

# Web 应用配置web.xml 

web.xml 是web应用的描述文件， 它支持的元素及属性来自于Servlet 规范定义 。 在Tomcat 中， Web 应用的描述信息包括 tomcat/conf/web.xml 中默认配置 以及 Web应用 WEB-INF/web.xml 下的定制配置。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020041510383458.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3oxNzkwNDI0NTc3,size_16,color_FFFFFF,t_70)

## ServletContext 初始化参数

我们可以通过 添加ServletContext 初始化参数，它配置了一个键值对，这样我们可以在应用程序中使用 javax.servlet.ServletContext.getInitParameter()方法获取参数：

```markup
<context‐param>
		<param‐name>contextConfigLocation</param‐name>
		<param‐value>classpath:applicationContext‐*.xml</param‐value>
		<description>Spring Config File Location</description>
</context‐param>
12345
```

## 会话配置

用于配置Web应用会话，包括 超时时间、Cookie配置以及会话追踪模式。它将覆盖server.xml 和 context.xml 中的配置：

```markup
<session‐config>
	<session‐timeout>30</session‐timeout>
		<cookie‐config>
			<name>JESSIONID</name>
			<domain>www.itcast.cn</domain>
			<path>/</path>
			<comment>Session Cookie</comment>
			<http‐only>true</http‐only>
			<secure>false</secure>
			<max‐age>3600</max‐age>
		</cookie‐config>
	<tracking‐mode>COOKIE</tracking‐mode>
</session‐config>
12345678910111213
```

配置解析：

```java
1） session‐timeout ： 会话超时时间，单位 分钟
2） cookie‐config： 用于配置会话追踪Cookie
			name：Cookie的名称
			domain：Cookie的域名
			path：Cookie的路径
			comment：注释
			http‐only：cookie只能通过HTTP方式进行访问，JS无法读取或修改，此项可以增
			加网站访问的安全性。
			secure：此cookie只能通过HTTPS连接传递到服务器，而HTTP 连接则不会传递该
			信息。注意是从浏览器传递到服务器，服务器端的Cookie对象不受此项影响。
			max‐age：以秒为单位表示cookie的生存期，默认为‐1表示是会话Cookie，浏览器
			关闭时就会消失。
			3） tracking‐mode ：用于配置会话追踪模式，Servlet3.0版本中支持的追踪模式：
			COOKIE、URL、SSL
			A. COOKIE : 通过HTTP Cookie 追踪会话是最常用的会话追踪机制， 而且
			Servlet规范也要求所有的Servlet规范都需要支持Cookie追踪。
			B. URL : URL重写是最基本的会话追踪机制。当客户端不支持Cookie时，可以采
			用URL重写的方式。当采用URL追踪模式时，请求路径需要包含会话标识信息，Servlet容器
			会根据路径中的会话标识设置请求的会话信息。如：
			http：//www.myserver.com/user/index.html;jessionid=1234567890。
			C. SSL : 对于SSL请求， 通过SSL会话标识确定请求会话标识。
123456789101112131415161718192021
```

## Servlet配置

Servlet 的配置主要是两部分， servlet 和 servlet-mapping ：

```markup
<servlet>
	<servlet‐name>myServlet</servlet‐name>
	<servlet‐class>cn.itcast.web.MyServlet</servlet‐class>
	<init‐param>
		<param‐name>fileName</param‐name>
		<param‐value>init.conf</param‐value>
	</init‐param>
	<load‐on‐startup>1</load‐on‐startup>
	<enabled>true</enabled>
</servlet>
<servlet‐mapping>
	<servlet‐name>myServlet</servlet‐name>
	<url‐pattern>*.do</url‐pattern>
	<url‐pattern>/myservet/*</url‐pattern>
</servlet‐mapping>
123456789101112131415
```

配置说明：

1. servlet‐name : 指定servlet的名称， 该属性在web.xml中唯一；
2. servlet‐class : 用于指定servlet类名；
3. init‐param： 用于指定servlet的初始化参数， 在应用中可以通过HttpServlet.getInitParameter 获取；
4. load‐on‐startup： 用于控制在Web应用启动时，Servlet的加载顺序。 值小于0，web应用启动时，不加载该servlet, 第一次访问时加载；
5. enabled： true ， false 。 若为false ，表示Servlet不处理任何请求；
6. url‐pattern： 用于指定URL表达式，一个 servlet‐mapping可以同时配置多个 urlpattern；

Servlet 中文件上传配置：

```markup
<servlet>
	<servlet‐name>uploadServlet</servlet‐name>
	<servlet‐class>cn.itcast.web.UploadServlet</servlet‐class>
	<multipart‐config>
		<location>C://path</location>
		<max‐file‐size>10485760</max‐file‐size>
		<max‐request‐size>10485760</max‐request‐size>
		<file‐size‐threshold>0</file‐size‐threshold>
	</multipart‐config>
</servlet>
12345678910
```

配置说明：

1. location：存放生成的文件地址；
2. max‐file‐size：允许上传的文件最大值。 默认值为‐1， 表示没有限制；
3. max‐request‐size：针对该 multi/form‐data 请求的最大数量，默认值为‐1， 表示无限制；
4. file‐size‐threshold：当数量量大于该值时， 内容会被写入文件；

## Listener配置

Listener用于监听servlet中的事件，例如context、request、session对象的创建、修改、删除，并触发响应事件。Listener是观察者模式的实现，在servlet中主要用于对context、request、session对象的生命周期进行监控。在servlet2.5规范中共定义了8种
Listener。在启动时，ServletContextListener 的执行顺序与web.xml 中的配置顺序一致， 停止时执行顺序相反。

```markup
<listener>
	<listenerclass>org.springframework.web.context.ContextLoaderListener</listenerclass>
</listener>
123
```

## Filter配置

filter 用于配置web应用过滤器， 用来过滤资源请求及响应。 经常用于认证、日志、加密、数据转换等操作， 配置如下：

```markup
<filter>
	<filter‐name>myFilter</filter‐name>
	<filter‐class>cn.itcast.web.MyFilter</filter‐class>
	<async‐supported>true</async‐supported>
	<init‐param>
		<param‐name>language</param‐name>
		<param‐value>CN</param‐value>
	</init‐param>
</filter>
<filter‐mapping>
	<filter‐name>myFilter</filter‐name>
	<url‐pattern>/*</url‐pattern>
</filter‐mapping>
12345678910111213
```

配置说明：

1. filter‐name： 用于指定过滤器名称，在web.xml中，过滤器名称必须唯一；
2. filter‐class ： 过滤器的全限定类名， 该类必须实现Filter接口；
3. async‐supported： 该过滤器是否支持异步；
4. init‐param ：用于配置Filter的初始化参数， 可以配置多个， 可以通过FilterConfig.getInitParameter获取；
5. url‐pattern： 指定该过滤器需要拦截的URL；

## 欢迎页面配置

welcome-file-list 用于指定web应用的欢迎文件列表：

```markup
<welcome‐file‐list>
	<welcome‐file>index.html</welcome‐file>
	<welcome‐file>index.htm</welcome‐file>
	<welcome‐file>index.jsp</welcome‐file>
</welcome‐file‐list>
12345
```

尝试请求的顺序，从上到下。

## 错误页面配置

error-page 用于配置Web应用访问异常时定向到的页面，支持HTTP响应码和异常类两种形式：

```markup
<error‐page>
	<error‐code>404</error‐code>
	<location>/404.html</location>
</error‐page>
<error‐page>
	<error‐code>500</error‐code>
	<location>/500.html</location>
</error‐page>
<error‐page>
	<exception‐type>java.lang.Exception</exception‐type>
	<location>/error.jsp</location>
</error‐page>
123456789101112
```

# Tomcat 管理配置

从早期的Tomcat版本开始，就提供了Web版的管理控制台，他们是两个独立的Web应用，位于webapps目录下。Tomcat 提供的管理应用有用于管理的Host的host-manager和用于管理Web应用的manager；

## host-manager

Tomcat启动之后，可以通过 http://localhost:8080/host-manager/html 访问该Web应用。 host-manager 默认添加了访问权限控制，当打开网址时，需要输入用户名和密码（conf/tomcat-users.xml中配置） 。所以要想访问该页面，需要在conf/tomcatusers.
xml 中配置，并分配对应的角色：

1. admin-gui：用于控制页面访问权限；
2. admin-script：用于控制以简单文本的形式进行访问；

配置如下：

```markup
<role rolename="admin‐gui"/>
<role rolename="admin‐script"/>
<user username="admin" password="123" roles="admin‐script,admin-gui"/>
123
```

登录：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200415105140843.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3oxNzkwNDI0NTc3,size_16,color_FFFFFF,t_70)
界面：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200415105611146.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3oxNzkwNDI0NTc3,size_16,color_FFFFFF,t_70)

## manager

manager的访问地址为 http://localhost:8080/manager， 同样， manager也添加了页面访问控制，因此我们需要为登录用户分配角色为:

```markup
<role rolename="manager‐gui"/>
<role rolename="manager‐script"/>
<user username="admin" password="123" roles="admin‐script,admin-gui,manager‐gui,manager‐script"/>
123
```

界面：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200415105755804.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3oxNzkwNDI0NTc3,size_16,color_FFFFFF,t_70)
Server Status:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200415105824792.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3oxNzkwNDI0NTc3,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200415105834629.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3oxNzkwNDI0NTc3,size_16,color_FFFFFF,t_70)

# JVM 配置

最常见的JVM配置当属内存分配，因为在绝大多数情况下，JVM默认分配的内存可能不能够满足我们的需求，特别是在生产环境，此时需要手动修改Tomcat启动时的内存参数分配。

## JVM内存模型图

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200415105935308.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3oxNzkwNDI0NTc3,size_16,color_FFFFFF,t_70)

## JVM配置选项

windows 平台(catalina.bat)：

```markup
set JAVA_OPTS=‐server ‐Xms2048m ‐Xmx2048m ‐XX:MetaspaceSize=256m ‐XX:MaxMetaspaceSize=256m ‐XX:SurvivorRatio=8
1
```

linux 平台(catalina.sh)：

```markup
JAVA_OPTS="‐server ‐Xms1024m ‐Xmx2048m ‐XX:MetaspaceSize=256m ‐XX:MaxMetaspaceSize=512m ‐XX:SurvivorRatio=8"
1
```

参数说明 ：

| 序号 | 参数                                              | 含义                                                         |
| ---- | ------------------------------------------------- | ------------------------------------------------------------ |
| 1    | -Xms                                              | 堆内存的初始大小                                             |
| 2    | -Xmx                                              | 堆内存的最大大小                                             |
| 3    | -Xmn                                              | 新生代的内存大小，官方建议是整个堆得3/8                      |
| 4    | -XX:MetaspaceSize                                 | 元空间内存初始大小， 在JDK1.8版本之前配置为 -XX:PermSize（永久代） |
| 5    | -XX:MaxMetaspaceSize                              | 元空间内存最大大小， 在JDK1.8版本之前配置为 -XX:MaxPermSize（永久代） |
| 6    | -XX:InitialCodeCacheSize-XX:ReservedCodeCacheSize | 代码缓存区大小                                               |
| 7    | -XX:NewRatio                                      | 设置新生代和老年代的相对大小比例。这种方式的优点是新生代大小会随着整个堆大小动态扩展。如 -XX:NewRatio=3 指定老年代 /新生代为 3/1。 老年代占堆大小的 3/4，新生代占 1/4 |
| 8    | -XX:SurvivorRatio                                 | 指定伊甸园区 (Eden) 与幸存区大小比例。如-XX:SurvivorRatio=10 表示伊甸园区 (Eden)是 幸存区 To 大小的 10 倍 (也是幸存区 From的 10 倍)。 所以， 伊甸园区 (Eden) 占新生代大小的 10/12， 幸存区 From 和幸存区 To 每个占新生代的 1/12 。 注意， 两个幸存区永远是一样大的 |

配置之后, 重新启动Tomcat ,访问：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200415110459680.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3oxNzkwNDI0NTc3,size_16,color_FFFFFF,t_70)

 

