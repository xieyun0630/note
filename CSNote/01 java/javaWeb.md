## Tomcat [	](javaWeb_20201022051052166)

### tomcat目录结构 [	](javaWeb_20201022051052169)
+ `bin`：{{c1:: 启动和关闭tomcat的bat文件 }}
+ `conf`：{{c1:: 配置文件 }}
  + `server.xml`:{{c1:: 该文件用于配置server相关的信息，比如tomcat启动的端口号，配置主机(Host) }}
  + `web.xml`:{{c1:: 文件配置与web应用（web应用相当于一个web站点） }}
  + `tomcat-user.xml`:{{c1:: 配置用户名密码和相关权限. }}
+ `lib`：{{c1:: 该目录放置运行tomcat运行需要的jar包 }}
+ `logs`：{{c1:: 存放日志，当我们需要查看日志的时候，可以查询信息 }}
+ `webapps`：{{c1:: 放置我们的web应用 }}
+ `work`：{{c1:: 该目录用于存放jsp被访问后生成对应的server文件和.class文件 }}

### javaWeb站点目录结构 [	](javaWeb_20201022051052170)
+ `WebContent(WebRoot)`：{{c1:: 存放的是需要部署到服务器的文件 }}
  + `WEB-INF`：{{c1:: 这个目录下的文件，是不能被客户端直接访问的。 }}
    + `classes`：{{c1:: 存放Java字节码文件的目录。 }}
    + `lib`：{{c1:: 用于存放该工程用到的库。 }}
    + `web.xml`：{{c1:: web工程的配置文件，完成用户请求的逻辑名称到真正的servlet类的映射。 }}
  + HTML文件,jsp文件

### 配置tomcat虚拟目录 [	](javaWeb_20201022051052172)
+ 目的:{{c1:: 都放在webapps下不利于对web站点目录的管理，分散到其他磁盘下，可以方便管理 }}
+ 2种方式：
  1. `server.xml`：{{c1:: `server.xml`中的`<Host>`节点下配置：`<Context path="/web1" docBase="D:\web1"/>` }}
  2. 添加xml文件：{{c1:: 进入`conf\Catalina\localhost`目录下添加xml文件:`<Context docBase="D:\web1" reloadable="true"></Context>` }}

### 设置虚拟主机 [	](javaWeb_20201022051052174)
+ 作用：{{c1:: 我现在开发了4个网站，有4个域名。如果我不配置虚拟主机，一个Tomcat服务器运行一个网站，我就需要4台电脑才能把4个网站运行起来。 }}
+ 配置虚拟主机的步骤：
  1. {{c1:: 在tomcat的server.xml文件中添加主机名 }}
    ```xml 
      <!-- {{c1:: -->
      <Host name="xieyun" appBase="D:\web1">
        <Context path="/web1" docBase="D:\web1"/>
      </Host>
      <!-- }} -->
    ```
  2. {{c1:: 访问虚拟主机下的web站点：xieyun:8080/web1/1.html }}
  3. {{c1:: 在hosts文件下配置临时域名 }}

### Tomcat体系结构(图) [	](javaWeb_20201022051052176)
+ {{c1:: ![tomcat_1029](https://gitee.com/xieyun714/nodeimage/raw/master/img/tomcat_1029.png)}}
+ 各组件含义：
  - `Server`: {{c1:: 对应的就是一个 Tomcat 实例。 }}
  - `Service`: {{c1:: 默认只有一个，也就是一个 Tomcat 实例默认一个 Service。 }}
  - `Connector`: {{c1:: 一个 Service 可能多个 连接器，接受不同连接协议。 }}
  - `Container`: {{c1:: 多个连接器对应一个容器，顶层容器其实就是 Engine。 }}
+ 组件之间的关系:
  + `Tomcat`实例: {{c1:: 比如一个`Tomcat`实例包含一个`Service` }}
  + `Service`: {{c1:: 一个`Service` 包含多个**连接器**和一个**容器**。 }}
  + `Container`: {{c1::一个容器包含多个`Host` }}
  + `Host`: {{c1:: `Host`内部可能有多个`Context`容器， }}
  + `Context`: {{c1:: 一个`Context`也会包含多个`Servlet` }}

### 连接器(Connector) [	](javaWeb_20201115082829553)

+ 连接器的结构图：{{c1:: ![image-20201111163036592](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201111163036592.png) }}
+ 各组件作用：
  + `ProtocolHandler `: {{c1::主要处理**网络连接**和**应用层协议**，包含了两个重要部件`EndPoint`和`Processor`}}
    + `ProtocolHandler`继承体系（图）：{{c1::![image-20201111165114291](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201111165114291.png) }}
  + `EndPoint`：{{c1:: 负责网络通信。负责提供字节流给`Processor`}}
  + `Processor`：{{c1:: 负责应用层协议解析。负责提供`Tomcat Request`对象给`Adapter`}}
  + `Adapter`：{{c1:: `Tomcat Request/Response`与`ServletRequest/ServletResponse`的转化。负责提供`ServletRequest`对象给容器。}}

## 常见试题 [	](javaWeb_20201026014023034)

### Tomcat的缺省端口是多少，怎么修改 [	](javaWeb_20201026014023037)
+ 到tomcat主目录下的`conf/server.xml`文件中修改
  ```xml
  <!-- {{c1:: -->
    <Service name="Catalina">
      <!-- ... -->
      <Connector port="8080" protocol="HTTP/1.1" 
                connectionTimeout="20000" 
                redirectPort="8443" />
  <!-- }} -->
  ```
### Tomcat 有哪几种Connector 运行模式(优化)？ [	](javaWeb_20201026014023039)
- `bio`: {{c1:: **传统的Java I/O操作，同步且阻塞IO。** }}
- `nio`: {{c1:: **JDK1.4开始支持，同步阻塞或同步非阻塞IO** }}
- `aio(nio.2)`: {{c1:: **JDK7开始支持，异步非阻塞IO** }}
- `apr`: {{c1:: Tomcat将以JNI的形式调用Apache HTTP服务器的核心动态链接库来处理文件读取或网络传输操作，从而大大地 **提高Tomcat对静态文件的处理性能** }}
+ 配置Tomcat运行模式:
  ```xml
    <!-- {{c1:: -->
      <Connector port="8080" protocol="org.apache.coyote.http11.Http11NioProtocol" connectionTimeout="20000" redirectPort="8443 />
    <!-- }} -->
  ```

### Tomcat有几种部署方式 [	](javaWeb_20201026014023041)
1. {{c1:: 直接把Web项目放在webapps下，Tomcat会自动将其部署 }}
2. {{c1:: 在server.xml文件上配置：` <Context path="/web1" docBase="D:\web1"/>` }}
3. {{c1:: `conf\Catalina\localhost`目录下添加xml配置文件:`<Context path="/web1" docBase="D:\web1"/>`,注意：xml声明 }}

## HTTP [	](javaWeb_20201022051052178)

### HTTP1.0和HTTP1.1的区别 [	](javaWeb_20201022051052180)
+ {{c1:: HTTP1.0协议中，客户端与web服务器建立连接后，只能获得一个web资源【短连接，获取资源后就断开连接】 }}
+ {{c1:: HTTP1.1协议，允许客户端与web服务器建立连接后，在一个连接上获取多个web资源【保持连接】 }}

### http请求结构： [	](javaWeb_20201022051052182)
+ {{c1:: 请求行：描述客户端的**请求方式**、**资源名称**，**HTTP协议版本号** }}
+ {{c1:: 请求头：描述客户端请求哪台主机，以及客户端的一些环境信息等 }}
+ {{c1:: 一个空行}}
+ {{c1:: 请求体}}

### 请求行 [	](javaWeb_20201022051052184)
+ 请求行：{{c1:: `GET /java.html HTTP/1.1` }}
+ 7种请求方式：{{c1:: `POST,GET,HEAD,OPTIONS,DELETE,TRACE,PUT` }}

### POST请求与GET请求 [	](javaWeb_20201022051052186)
+ 区别:{{c1:: 可以简单理解GET方式用来查询数据,POST方式用来提交数据，get的提交速度比post快 }}
+ `GET`方式：{{c1:: 在URL地址后附带的参数是有限制的，其数据容量通常不能超过1K。 }}
+ `POST`方式：{{c1:: 可以在请求的实体内容中向服务器发送数据，传送的数据量无限制。 }}

### 常见请求头 [	](javaWeb_20201022051052188)
| 请求头                                                       | 作用                                                       |
| :----------------------------------------------------------- | :--------------------------------------------------------- |
| `Accept: text/html,image/* `                                 | {{c1:: 浏览器告诉服务器，它支持的数据类型}}                |
| `Accept-Charset: ISO-8859-1 `                                | {{c1:: 浏览器告诉服务器，它支持哪种字符集}}                |
| `Accept-Encoding: gzip,compress `                            | {{c1:: 浏览器告诉服务器，它支持的压缩格式}}                |
| `Accept-Language: en-us,zh-cn `                              | {{c1:: 浏览器告诉服务器，它的语言环境}}                    |
| `Host: www.it315.org:80`                                     | {{c1:: 浏览器告诉服务器，它的想访问哪台主机}}              |
| `If-Modified-Since: Tue, 11 Jul 2000 18:23:51 GMT`           | {{c1:: 浏览器告诉服务器，缓存数据的时间}}                  |
| `Referer: http://www.it315.org/index.jsp`                    | {{c1:: 浏览器告诉服务器，客户机是从那个页面来的---反盗链}} |
| `User-Agent: Mozilla/4.0 (compatible; MSIE 5.5; Windows NT 5.0)` | {{c1:: 浏览器告诉服务器，浏览器的内核是什么}}              |
| `Cookie`                                                     | {{c1:: 浏览器告诉服务器，带来的Cookie是什么}}              |
| `Connection: close/Keep-Alive `                              | {{c1:: 浏览器告诉服务器，请求完后是断开链接还是保持链接}}  |
| `Date: Tue, 11 Jul 2000 18:23:51 GMT`                        | {{c1:: 浏览器告诉服务器，请求的时间}}                      |

### HTTP响应结构 [	](javaWeb_20201022051052190)
1. {{c1:: 一个状态行： 用于描述服务器对请求的处理结果。 }}
2. {{c1:: 多个消息头： 用于描述服务器的基本信息，以及数据的描述，服务器通 过这些数据的描述信息，可以通知客户端如何处理等一会儿它回送的数据}}
3. {{c1:: 一个空行 }}
4. {{c1:: 实体内容： 服务器向客户端回送的数据 }}

### 响应行 [	](javaWeb_20201022051052192)
+ 格式：{{c1:: `HTTP/1.1 200 OK` }}
+ | 分类 | 分类描述                                                |
  | :--- | :------------------------------------------------------ |
  | 1xx  | {{c1:: 信息，服务器收到请求，需要请求者继续执行操作  }} |
  | 2xx  | {{c1:: 成功，操作被成功接收并处理                    }} |
  | 3xx  | {{c1:: 重定向，需要进一步的操作以完成请求            }} |
  | 4xx  | {{c1:: 客户端错误，请求包含语法错误或无法完成请求    }} |
  | 5xx  | {{c1:: 服务器错误，服务器在处理请求的过程中发生了错误}} |

### 常见响应头 [	](javaWeb_20201022051052194)
| 响应头                                              | 作用                                           |
| :-------------------------------------------------- | :--------------------------------------------- |
| `Location: http://www.it315.org/index.jsp `         | {{c1:: 服务器告诉浏览器要跳转到哪个页面 }}     |
| `Server:apache tomcat`                              | {{c1:: 服务器告诉浏览器，服务器的型号是什么 }} |
| `Content-Encoding: gzip `                           | {{c1:: 服务器告诉浏览器数据压缩的格式 }}       |
| `Content-Length: 80 `                               | {{c1:: 服务器告诉浏览器回送数据的长度 }}       |
| `Content-Language: zh-cn `                          | {{c1:: 服务器告诉浏览器，服务器的语言环境 }}   |
| `Content-Type: text/html; charset=GB2312 `          | {{c1:: 服务器告诉浏览器，回送数据的类型 }}     |
| `Last-Modified: Tue, 11 Jul 2000 18:23:51 GMT`      | {{c1:: 服务器告诉浏览器该资源上次更新时间 }}   |
| `Refresh: 1;url=http://www.it315.org`               | {{c1:: 服务器告诉浏览器要定时刷新 }}           |
| `Content-Disposition: attachment; filename=aaa.zip` | {{c1:: 服务器告诉浏览器以下载方式打开数据 }}   |
| `Transfer-Encoding: chunked `                       | {{c1:: 服务器告诉浏览器数据以分块方式回送 }}   |
| `Set-Cookie:SS=Q0=5Lb_nQ; path=/search`             | {{c1:: 服务器告诉浏览器要保存Cookie }}         |
| `Expires: -1`                                       | {{c1:: 服务器告诉浏览器不要设置缓存 }}         |
| `Cache-Control: no-cache `                          | {{c1:: 服务器告诉浏览器不要设置缓存 }}         |
| `Pragma: no-cache `                                 | {{c1:: 服务器告诉浏览器不要设置缓存 }}         |
| `Connection: close/Keep-Alive `                     | {{c1:: 服务器告诉浏览器连接方式 }}             |
| `Date: Tue, 11 Jul 2000 18:23:51 GMT`               | {{c1:: 服务器告诉浏览器回送数据的时间 }}       |

## Servlet [	](javaWeb_20201022051052196)

### Servlet生命周期可分为5个步骤 [	](javaWeb_20201022051052198)

+ **加载Servlet**:{{c1:: 当Tomcat第一次访问Servlet的时候，Tomcat会负责创建Servlet的实例 }}
+ **初始化**:{{c1:: 当Servlet被实例化后，Tomcat会**调用init()方法**初始化这个对象 }}
+ **处理服务**:{{c1:: 当浏览器访问Servlet的时候，Servlet 会**调用service()方法**处理请求 }}
+ **销毁**:{{c1:: 当Tomcat关闭时或者检测到Servlet要从Tomcat删除的时候会自动**调用destroy()方法**，让该实例释放掉所占的资源。一个Servlet如果长时间不被使用的话，也会被Tomcat自动销毁 }}
+ **卸载**:{{c1:: 当Servlet调用完destroy()方法后，等待垃圾回收。如果有需要再次使用这个Servlet，会重新调用init()方法进行初始化操作。 }}
+ 简单总结：{{c1:: 只要访问Servlet，service()就会被调用。init()只有第一次访问Servlet的时候才会被调用。 destroy()只有在Tomcat关闭的时候才会被调用。 }}

### 编写一个Hello world Servlet [	](javaWeb_20201022051052200)
1. {{c1:: 实现Servlet类或者HttpServlet类 }}
2. {{c1:: 配置web.xml文件 }}
  ```xml
    <!-- {{c1:: -->
    <servlet>  
      <servlet-name>firstServlet</servlet-name>  
      <servlet-class>top.xieyun.firstServlet</servlet-class>  
    </servlet>  
    <servlet-mapping>  
      <servlet-name>firstServlet</servlet-name>  
      <!-- 同一个Servlet可以被映射到多个URL上。 -->
      <url-pattern>/servlet/firstServlet.jsp</url-pattern>  
      <url-pattern>/wocao.ppp</url-pattern>  
      <!-- Servlet映射的URL可以使用通配符 -->
      <url-pattern>/*</url-pattern>
    </servlet-mapping>
    <!-- }} -->
  ```
3. {{c1:: 配置tomcat运行Servlet }}


### Servlet的线程安全问题 [	](javaWeb_20201022051052202)
+ 背景：{{c1:: 由于Servlet是单例的，当多个用户访问Servlet的时候，**服务器会为每个用户创建一个线程**。**当多个用户并发访问Servlet共享资源的时候就会出现线程安全问题**。 }}
+ 原则：
  1. {{c1:: 如果一个**变量需要多个用户共享**，则应当在访问该变量的时候，**加同步机制synchronized (对象){}** }}
  2. {{c1:: 如果一个变量**不需要共享**，则**直接在 doGet() 或者 doPost()定义**.这样不会存在线程安全问题 }}

### load-on-startup [	](javaWeb_20201022051052204)

+ 作用：{{c1:: 让WEB应用程序在启动时，就会装载并创建Servlet的实例对象、以及调用Servlet实例对象的init()方法。 }}
+ 配置：
  ```xml
    <!-- {{c1:: -->
    <servlet>  
      <servlet-name>firstServlet</servlet-name>  
      <servlet-class>top.xieyun.firstServlet</servlet-class>  
      <load-on-startup>1</load-on-startup>
    </servlet>  
    <servlet-mapping>  
      <servlet-name>firstServlet</servlet-name>  
      <url-pattern>/*</url-pattern>
    </servlet-mapping>
    <!-- }} -->
  ```

### 手工配置的缺省Servlet，覆盖掉web.xml配置的缺省Servlet [	](javaWeb_20201022051052206)
```xml
  <!-- {{c1:: -->
  <servlet>
    <servlet-name>Demo1</servlet-name>
    <servlet-class>zhongfucheng.web.Demo1</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>Demo1</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
  <!-- }} -->
```
### ServletConfig对象 [	](javaWeb_20201022051052208)

+ 作用:{{c1:: 通过此对象可以读取web.xml中配置的初始化参数`<init-param>`。 }}
+ 在Servlet中获取ServletConfig对象:{{c1::`this.getServletConfig()`}}

### ServletContext对象 [	](javaWeb_20201022051052210)

+ 是什么：{{c1:: Tomcat启动的时候，会创建一个`ServletContext`对象，**代表当前web站点** }}
+ 作用：
  1. Servlet之间通信：{{c1:: ServletContext可以被称之为域对象,`主要用到ServletContext的setAttribute(String name,Object obj)方法`实现 }}
  2. 获取web站点的配置信息：{{c1:: ServletConfig获取的是配置的是单个Servlet的参数信息，ServletContext可以获取的是配置整个web站点的参数信息 }}

### ServletContext对象获取web站点的配置信息 [	](javaWeb_20201022051052212)

+ 背景：{{c1:: web.xml文件支持对整个站点进行配置参数信息,所有Servlet都可以取到该参数信息 }}
+ 示例配置
  ```xml
  <!-- {{c1:: -->
  <context-param>
    <param-name>name</param-name>
    <param-value>zhongfucheng</param-value>
  </context-param>
  <!-- }} -->
  ```
+ 获取配置信息:{{c1:: `String value = servletContext.getInitParameter("name");` }}

### servlet中读取资源文件 [	](javaWeb_20201022051052214)

1. 类路径下：{{c1:: `InputStream inputStream = servletContext.getResourceAsStream("/WEB-INF/classes/zhongfucheng/web/1.png");` }}
2. 将文件放在webRoot目录下：{{c1:: `servletContext.getResourceAsStream("2.png");` }}
3. 通过类装载器读取资源文件：{{c1:: `ServletTest.class.getClassLoader().getResourceAsStream("/zhongfucheng/web/1.png");` }}

## response与request [	](javaWeb_20201022051052216)

### 调用getOutputStream()方法向浏览器输出数据2个方法 [	](javaWeb_20201022051052218)

```xml
  <!-- {{c1:: -->
  <!-- print()方法接收了一个字符串 -->
  response.getOutputStream().print("中国！");
  <!-- write接收字节数组 -->
  response.getOutputStream().write("你好呀我是中国".getBytes("UTF-8"));
  <!-- }} -->
```

### 解决调用getOutputStream()方法输出数据的乱码问题 [	](javaWeb_20201022051052219)

1. 设置消息头的方法：{{c1:: `response.setHeader("Content-Type", "text/html;charset=UTF-8");` }}
2. 使用meta标签模拟http消息头:{{c1:: `servletOutputStream.write("<meta http-equiv='content-type' content='text/html;charset=UTF-8'>".getBytes());` }}

### 调用getWriter()方法向浏览器输出数据 [	](javaWeb_20201022051052221)

+ getWriter()方法作用：{{c1:: 只能向浏览器输出字符数据，不能输出二进制数据 }}
+ 使用getWriter()显示中文数据，只需要一个方法:{{c1:: `response.setContentType("text/html;charset=UTF-8");` }}

### Servlet实现文件下载 [	](javaWeb_20201022051052223)
+ 主要思路：{{c1:: 读取文件为文件流，输出到ServletOutputStream对象 }}
+ 设置消息头以及避免文件名乱码：{{c1:: `response.setHeader("Content-Disposition", "attachment; filename=" + URLEncoder.encode(fileName, "UTF-8"));` }}

### Servlet自动刷新，实现页面的跳转 [	](javaWeb_20201022051052225)
+ 自动刷新，能够实现页面的跳转:{{c1:: `response.setHeader("Refresh", "3;url='/index.jsp'");` }}

### Servlet设置缓存 [	](javaWeb_20201022051052227)
+ 浏览器有三消息头设置缓存，为了兼容性！将三个消息头都设置了:
  ```java
        //{{c1::
        response.setDateHeader("Expires", -1);
        response.setHeader("Cache-Control","no-cache");
        response.setHeader("Pragma", "no-cache");
        //}}
  ```

### Servlet实现数据压缩 [	](javaWeb_20201022051052229)
+ 主要思路：{{c1:: 使用压缩之类的工具类将数据压缩后，再输出到ServletOutputStream对象，注意设置消息头。 }}
  ```java
      // {{c1::
      //告诉浏览器这是gzip压缩的数据
      response.setHeader("Content-Encoding","gzip");
      //再将压缩的数据写给浏览器
      response.getOutputStream().write(bytes);
      //}}
  ```
### HttpServletRequest常用方法 [	](javaWeb_20201022051052231)
| 方法/功能          | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| `getRequestURL()`  | {{c1:: 方法返回客户端发出请求时的完整URL。                          }} |
| `getRequestURI()`  | {{c1:: 方法返回请求行中的资源名部分。                               }} |
| `getQueryString()` | {{c1:: 方法返回请求行中的参数部分。                                 }} |
| `getPathInfo()`    | {{c1:: 方法返回请求URL中的额外路径信息。额外路径信息是请求URL中的位于Servlet的路径之后和查询参数之前的内容，它以“/”开头。 }} |
| `getRemoteAddr()`  | {{c1:: 方法返回发出请求的客户机的IP地址                             }} |
| `getRemoteHost()`  | {{c1:: 方法返回发出请求的客户机的完整主机名                         }} |
| `getRemotePort()`  | {{c1:: 方法返回客户机所使用的网络端口号                             }} |
| `getLocalAddr()`   | {{c1:: 方法返回WEB服务器的IP地址。                                  }} |
| `getLocalName()`   | {{c1:: 方法返回WEB服务器的主机名                                    }} |
| 获得客户机请求头   | {{c1:: `getHeaderNames` `getHeaders`  `getHeaderNames`         }} |
| 获得客户机请求参数 | {{c1:: `getParameter` `getParameterValues` `getParameterNames` `getParameterMap`         }} |

### 重定向跳转 [	](javaWeb_20201022051052233)

+ ServletApi设置：{{c1:: `response.sendRedirect("/zhongfucheng/index.jsp");` }}
+ 设置响应：
   ```java
    //{{c1::
    //设置状态码是302
    response.setStatus(302);
    //HttpServletResponse把常用的状态码封装成静态常量了，所以我们可以使用SC_MOVED_TEMPORARILY代表着302
    response.setStatus(HttpServletResponse.SC_MOVED_TEMPORARILY);
    response.setHeader("Location", "/zhongfucheng/index.jsp");
    //}}
   ```
### getWriter和getOutputStream细节 [	](javaWeb_20201022051052235)
+ **不能同时调用**：{{c1:: getWriter()和getOutputStream()两个方法不能同时调用。如果同时调用就会出现异常}}
+ **作为消息正文**：{{c1:: Servlet程序向ServletOutputStream或PrintWriter对象中写入的数据将被Servlet引擎从response里面获取，Servlet引擎将这些数据当作响应消息的正文，然后再与响应状态行和各响应头组合后输出到客户端}}
+ **Servlet引擎将调用close方法关闭该输出流对象**：{{c1:: Servlet的serice()方法结束后【也就是doPost()或者doGet()结束后】，Servlet引擎将检查getWriter或getOutputStream方法返回的输出流对象是否已经调用过close方法，如果没有，Servlet引擎将调用close方法关闭该输出流对象.}}



### Servlet request获取参数乱码问题： [	](javaWeb_20201022051052237)
+ post方式直接改request对象的编码:{{c1:: `request.setCharacterEncoding("UTF-8");` }}
+ get方式需要手工转换编码:{{c1:: 将tomcat被`ISO 8859-1`编码后的字符串反向转换 }}
+ get方式也可以修改Tomcat服务器的配置，使用页面编码（不推荐）:{{c1:: `Connector`元素`useBodyEncodingForURI`属性 }}
+ 提交数据能用post就用post

### 转发与重定向的区别 [	](javaWeb_20201022051052239)
+ **实际发生位置**不同，**地址栏**不同:
  1. 发生位置:{{c1:: 转发是发生在服务器的,重定向是发生在浏览器的 }}
  2. 地址栏:{{c1:: 转发浏览器的地址栏是没有发生变化的,重定向浏览器的地址会发生变化的 }}
+ **能够去往的URL的范围**不一样:
  + 转发是服务器跳转只能去往当前web应用的资源
    + 转发时"/"代表:{{c1:: 本应用程序的根目录 }}
  + 重定向是浏览器跳转，可以去往任何的资源
    + 重定向时"/"代表:{{c1:: webapps目录 }}
+ **传递数据的类型不同**：转发的request对象可以传递各种类型的数据包括对象，重定向只能传递字符串

### `RequestDispatcher`的`include()` [	](javaWeb_20201022051052241)
+ 作用示意图：{{c1:: ![image-20201022133020639](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20201022133020639.png) }}

## Servlet相关Cookie [	](javaWeb_20201022051052243)

### 什么是会话 [	](javaWeb_20201022051052245)
+ 基本概念: {{c1:: 指用户开一个浏览器，访问一个网站,只要不关闭该浏览器，不管该用户点击多少个超链接，访问多少资源，直到用户关闭浏览器，整个这个过程我们称为一次会话. }}

### Servlet中CookieAPI [	](javaWeb_20201022051052247)
+ `Cookie类`:{{c1:: Cookie类用于创建一个Cookie对象 }}
+ `addCookie方法`:{{c1:: response接口中定义了一个addCookie方法，它用于在其响应头中增加一个相应的Set-Cookie头字段 }}
+ `getCookies方法`:{{c1:: request接口中定义了一个getCookies方法，它用于获取客户端提交的Cookie }}

### Servlet相关的Cookie细节 [	](javaWeb_20201022051052249)
+ 跨域名： {{c1:: Cookie不可跨域名 }}
+ Cookie保存中文：{{c1:: 需要编码与解码 }}
  + 编码：{{c1:: `new Cookie("country", URLEncoder.encode("中文", "UTF-8"));` }}
  + 解码：{{c1:: `URLDecoder.decode(cookies[i].getValue(), "UTF-8");` }}
+ Cookie的有效期:{{c1:: `cookie.setMaxAge(2000);` }}
  + **MaxAge为正数**:{{c1:: 浏览器会把Cookie写到硬盘中，只要还在MaxAge秒之前，登陆网站时该Cookie就有效【不论关闭了浏览器还是电脑】 }}
  + **MaxAge为负数**:{{c1:: Cookie是临时性的，仅在本浏览器内有效，关闭浏览器Cookie就失效了，Cookie不会写到硬盘中。Cookie默认值就是-1。这也就为什么设置Cookie的有效期，在硬盘中就找不到对应的文件。 }}
  + **MaxAge为0**:{{c1:: 则表示删除该Cookie。Cookie机制没有提供删除Cookie对应的方法，把MaxAge设置为0等同于删除Cookie }}

## Session [	](javaWeb_20201022051052251)

### SessionAPI 常用方法 [	](javaWeb_20201022051052253)
| 方法                                           | 说明                      |
| :--------------------------------------------- | :------------------------ |
| `long getCreationTime();`                      | {{c1:: 获取Session被创建时间    }} |
| `String getId();`                              | {{c1:: 获取Session的id          }} |
| `long getLastAccessedTime();`                  | {{c1:: 返回Session最后活跃的时间}} |
| `ServletContext getServletContext();`          | {{c1:: 获取ServletContext对象   }} |
| `void setMaxInactiveInterval(int var1);`       | {{c1:: 设置Session超时时间      }} |
| `int getMaxInactiveInterval();`                | {{c1:: 获取Session超时时间      }} |
| `Object getAttribute(String var1);`            | {{c1:: 获取Session属性          }} |
| `Enumeration<String> getAttributeNames();`     | {{c1:: 获取Session所有的属性名  }} |
| `void setAttribute(String var1, Object var2);` | {{c1:: 设置Session属性          }} |
| `void removeAttribute(String var1);`           | {{c1:: 移除Session属性          }} |
| `void invalidate();`                           | {{c1:: 销毁该Session            }} |
| `boolean isNew();`                             | {{c1:: 该Session是否为新的      }} |

### Session的生命周期 [	](javaWeb_20201022051052255)

+ **Session创建**：{{c1:: Session在用户第一次访问服务器Servlet，jsp等动态资源就会被自动创建，Session对象保存在内存里}}
+ **Session更新**：{{c1:: 如果访问HTML,IMAGE等静态资源Session不会被创建。Session生成后，只要用户继续访问，服务器就会更新Session的最后访问时间，无论是否对Session进行读写，服务器都会认为Session活跃了一次。}}

### Session的超时时间 [	](javaWeb_20201022051052257)

+ 是什么：{{c1:: 为了防止内存溢出，服务器会把长时间没有活跃的Session从内存中删除，这个时间也就是Session的超时时间。 }}
+ 三种方式可以对Session的超时时间进行修改:
  1. 在`tomcat/conf/web.xml`文件中设置:
    ```xml
      <!-- {{c1:: -->
      <session-config>
        <session-timeout>20</session-timeout>
      </session-config>    
      <!-- }} -->
    ```
  2. 在单个的web.xml文件中设置
    ```xml
      <!-- {{c1:: -->
      <session-config>
        <session-timeout>20</session-timeout>
      </session-config>    
      <!-- }} -->
    ```
  + 通过setMaxInactiveInterval()方法设置
    ```java
        //{{c1::
        //设置Session最长超时时间为60秒，这里的单位是秒
        httpSession.setMaxInactiveInterval(60);
        //}}
    ```
### 禁掉Coockie后，使用Session [	](javaWeb_20201022051052259)
+ HttpServletResponse类提供了两个URL地址重写的方法：
  + {{c1:: `encodeURL(String url)` }}
  + {{c1:: `encodeRedirectURL(String url)` }}
+ 需要值得注意的是：{{c1:: 这两个方法会自动判断该浏览器是否支持`Cookie`，如果支持Cookie，重写后的URL地址就不会带有`jsessionid` }}
+ URL地址重写例：
  ```java
    //{{c1::
    String url = "/ouzicheng/Servlet7";
    response.sendRedirect(response.encodeURL(url));
    //}}
  ```

### 配置web项目禁用Cookie [	](javaWeb_20201022051052261)

+ 配置文件位置:
  1. {{c1:: webRoot下`META-INF`文件夹下的`context.xml`文件 }}
  2. {{c1:: tomcat下`conf/context.xml` }}
+ 配置：
  ```xml
    <!-- {{c1:: -->
    <Context path="/ouzicheng" cookies="false">
    </Context>
    <!-- }} -->
  ```

### 实现重启浏览器后，依旧能识别出session [	](javaWeb_20201022051052263)

- 第一种方式：{{c1:: 只需要在处理购买页面上创建Cookie，Cookie的值是Session的id返回给浏览器即可 }}
  ```java
    //{{c1::
    Cookie cookie = new Cookie("JSESSIONID",session.getId());
    cookie.setMaxAge(30*60);
    cookie.setPath("/ouzicheng/");
    response.addCookie(cookie);
    //}}
  ```
- 第二种方式：{{c1:: 在server.xml文件中配置，将每个用户的Session在服务器关闭的时候序列化到硬盘或数据库上保存。 }}

### Session和Cookie的区别 [	](javaWeb_20201022051052265)

- **从存储方式上比较**
  - {{c1:: Cookie只能存储字符串，如果要存储非ASCII字符串还要对其编码。 }}
  - {{c1:: Session可以存储任何类型的数据，可以把Session看成是一个容器 }}
- **从隐私安全上比较**
  - {{c1:: Cookie存储在浏览器中，对客户端是可见的。信息容易泄露出去。如果使用Cookie，最好将Cookie加密 }}
  - {{c1:: Session存储在服务器上，对客户端是透明的。不存在敏感信息泄露问题。 }}
- **从有效期上比较**
  - {{c1:: Cookie保存在硬盘中，只需要设置maxAge属性为比较大的正整数，即使关闭浏览器，Cookie还是存在的 }}
  - {{c1:: Session的保存在服务器中，设置maxInactiveInterval属性值来确定Session的有效期。并且Session依赖于名为JSESSIONID的 }}Cookie，该Cookie默认的maxAge属性为-1。如果关闭了浏览器，该Session虽然没有从服务器中消亡，但也就失效了。
- **从对服务器的负担比较**
  - {{c1:: Session是保存在服务器的，每个用户都会产生一个Session，如果是并发访问的用户非常多，是不能使用Session的，Session会消耗大量 }}的内存。
  - {{c1:: Cookie是保存在客户端的。不占用服务器的资源。像baidu、Sina这样的大型网站，一般都是使用Cookie来进行会话跟踪。 }}
- **从浏览器的支持上比较**
  - {{c1:: 如果浏览器禁用了Cookie，那么Cookie是无用的了！ }}
  - {{c1:: 如果浏览器禁用了Cookie，Session可以通过URL地址重写来进行会话跟踪。 }}
- **从跨域名上比较**
  - {{c1:: Cookie可以设置domain属性来实现跨域名 }}
  - {{c1:: Session只在当前的域名内有效，不可跨域名 }}

### 常见试题 [	](javaWeb_20201026014023043)

### get方式和post方式有何区别： [	](javaWeb_20201026014023044)
+ 数据携带上:
  - {{c1:: GET方式：在URL地址后附带的参数是有限制的，其数据容量通常不能超 }}过1K。
  - {{c1:: POST方式：可以在请求的实体内容中向服务器发送数据，传送的数据量 }}无限制。
+ 请求参数的位置上:
  - {{c1:: GET方式：请求参数放在URL地址后面，以?的方式来进行拼接 }}
  - {{c1:: POST方式:请求参数放在HTTP请求包中 }}
+ 用途上:
  - {{c1:: GET方式一般用来获取数据 }}
  - {{c1:: POST方式一般用来提交数据 }}

### request.getAttribute()和request.getParameter()区别 [	](javaWeb_20201026014023046)
+ 用途上:
  + {{c1:: `request.getAttribute()`一般用于获取request域对象的数据(在跳转之前把数据使用setAttribute来放到request对象上) }}
  + {{c1:: `request.getParameter()`一般用于获取客户端提交的参数 }}
+ 存储数据上:
  + {{c1:: `request.getAttribute()`可以获取Objcet对象}}
  + {{c1:: `request.getParameter()`只能获取字符串(这也是为什么它一般用于获取客户端提交的参数)}}

### tomcat容器是如何创建servlet类实例？用到了什么原理？ [	](javaWeb_20201026014023048)

1. {{c1:: 当容器启动时，会读取在webapps目录下所有的web应用中的web.xml文件，然后对 **xml文件进行解析，并读取servlet注册信息**。然后，将每个应用中注册的servlet类都进行加载，并通过 **反射的方式实例化**。（有时候也是在第一次请求时实例化） }}
2. {{c1:: 在servlet注册时加上`<load-on-startup>1</load-on-startup>`如果为正数，则在一开始就实例化，如果不写或为负数，则第一次请求实例化。 }}

## 过滤器 [	](javaWeb_20201026014023050)

### 实现简单的过滤器步骤 [	](javaWeb_20201026014023052)
1. {{c1:: 实现Filter接口，注意过滤链的调用 }}
2. {{c1:: 在web.xml中配置`<filter>` `<filter-mapping>` }}

### Servlet 过滤器的配置 [	](javaWeb_20201026014023054)
+ `<filter>`
  + `<filter-name>`:{{c1:: 用于为过滤器指定一个名字，该元素的内容不能为空。 }}
  + `<filter-class>`:{{c1:: 元素用于指定过滤器的完整的限定类名。 }}
  + `<init-param>`:{{c1:: 元素用于为过滤器指定初始化参数，它的子元素`<param-name>`指定参数的名字，`<param-value>`:{{c1:: 指定参数的值。在过滤器中，可以使用FilterConfig接口对象来访问初始化参数。 }}
+ `<filter-mapping>`
  + `<filter-name>`:{{c1:: 子元素用于设置filter的注册名称。该值必须是在`<filter>`元素中声明过的过滤器的名字 }}
  + `<url-pattern>`:{{c1:: 设置 filter 所拦截的请求路径(过滤器关联的URL样式) }}
  + `<servlet-name>`:{{c1:: 指定过滤器所拦截的Servlet名称。 }}
  + `<dispatcher>`:{{c1:: 指定过滤器所拦截的资源被 Servlet 容器调用的方式，可以是`REQUEST`,`INCLUDE`,`FORWARD`和`ERROR`之一，默认`REQUEST`。用户可以设置多个`<dispatcher>`子元素用来指定 Filter 对资源的多种调用方式进行拦截。 }}
+ 注解配置：{{c1:: `@WebFilter(filterName = "FilterDemo1",urlPatterns = "/*")` }}
+ 示例代码：
  ```xml
  <!-- {{c1:: -->
    <filter>
      <filter-name>FilterDemo1</filter-name>
      <filter-class>FilterDemo1</filter-class>
      <init-param>
        <param-name>word_file</param-name>
        <param-value>/WEB-INF/word.txt</param-value>
      </init-param>
    </filter>
    <filter-mapping>
        <filter-name>FilterDemo1</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
  <!-- }} -->
  ```

### 过滤器的执行顺序 [	](javaWeb_20201026014023055)

+ FilterChain作用：{{c1:: FilterChain接口是代表着所有的Filter，FilterChain中的doFilter()方法决定着是否放行下一个过滤器执行（如果没有过滤器了，就执行目标资源）。 }}
+ 过滤器之间的执行顺序：{{c1:: 是根据web.xml文件中**mapping**的先后顺序的，如果放在前面就先执行，放在后面就后执行！如果是通过注解的方式配置，就比较**urlPatterns的字符串优先级** }}

## 监听器 [	](javaWeb_20201026014023057)
### Servle监听器 [	](javaWeb_20201026014023059)
+ 监听对象的创建和销毁:{{c1:: `HttpSessionListener`、`ServletContextListener`、`ServletRequestListener`分别监控着`Session`、`Context`、`Request`对象的创建和销毁 }}
+ 监听对象属性变化:{{c1:: `ServletContextAttributeListener`、`HttpSessionAttributeListener`、`ServletRequestAttributeListener`分别监听着`Context`、`Sessio`、`Request`对象属性的变化 }}

### 监听Session内的对象 [	](javaWeb_20201026014023061)
+ 实现`HttpSessionBindingListener`接口:{{c1:: JavaBean 对象可以感知自己被绑定到 Session 中和从 Session 中删除的事件【和HttpSessionAttributeListener的作用是差不多的】 }}
+ 实现`HttpSessionActivationListener`接口:{{c1:: JavaBean 对象可以感知自己被活化和钝化的事件（当服务器关闭时，会将Session的内容保存在硬盘上【钝化】，当服务器开启时，会将Session的内容在硬盘式重新加载【活化】） 。 }}
+ 实现类例：
  ```java
  //{{c1::
    public class User implements HttpSessionBindingListener,HttpSessionActivationListener,Serializable {
        //...
    }
  //}}
  ```
+ 要测试出Session的硬化和钝化，需要修改Tomcat的配置:
  ```xml
  <!-- {{c1:: -->
    <Context>
      <Manager className="org.apache.catalina.session.PersistentManager" maxIdleSwap="1">
      <Store className="org.apache.catalina.session.FileStore" directory="zhongfucheng"/>
      </Manager>
    </Context>
  <!-- }} -->
  ```