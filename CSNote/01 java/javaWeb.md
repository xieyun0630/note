## Tomcat

### tomcat目录结构
+ `bin`：{{c1:: 启动和关闭tomcat的bat文件 }}
+ `conf`：{{c1:: 配置文件 }}
  + `server.xml`:{{c1:: 该文件用于配置server相关的信息，比如tomcat启动的端口号，配置主机(Host) }}
  + `web.xml`:{{c1:: 文件配置与web应用（web应用相当于一个web站点） }}
  + `tomcat-user.xml`:{{c1:: 配置用户名密码和相关权限. }}
+ `lib`：{{c1:: 该目录放置运行tomcat运行需要的jar包 }}
+ `logs`：{{c1:: 存放日志，当我们需要查看日志的时候，可以查询信息 }}
+ `webapps`：{{c1:: 放置我们的web应用 }}
+ `work`：{{c1:: 该目录用于存放jsp被访问后生成对应的server文件和.class文件 }}

### javaWeb站点目录结构
+ `WebContent(WebRoot)`：{{c1:: 存放的是需要部署到服务器的文件 }}
  + `WEB-INF`：{{c1:: 这个目录下的文件，是不能被客户端直接访问的。 }}
    + `classes`：{{c1:: 存放Java字节码文件的目录。 }}
    + `lib`：{{c1:: 用于存放该工程用到的库。 }}
    + `web.xml`：{{c1:: web工程的配置文件，完成用户请求的逻辑名称到真正的servlet类的映射。 }}
  + HTML文件,jsp文件

### 配置tomcat虚拟目录
+ 目的:{{c1:: 都放在webapps下不利于对web站点目录的管理，分散到其他磁盘下，可以方便管理 }}
+ 2种方式：
  1. `server.xml`：{{c1:: `server.xml`中的`<Host>`节点下配置：`<Context path="/web1" docBase="D:\web1"/>` }}
  2. 添加xml文件：{{c1:: 进入`conf\Catalina\localhost`目录下添加xml文件:`<Context docBase="D:\web1" reloadable="true"></Context>` }}

### 设置虚拟主机
+ 作用：我现在开发了4个网站，有4个域名。如果我不配置虚拟主机，一个Tomcat服务器运行一个网站，我就需要4台电脑才能把4个网站运行起来。
+ 配置虚拟主机的步骤：
  1. 在tomcat的server.xml文件中添加主机名
    ```xml 
      <Host name="xieyun" appBase="D:\web1">
        <Context path="/web1" docBase="D:\web1"/>
      </Host>
    ```
  2. 访问虚拟主机下的web站点：xieyun:8080/web1/1.html
+ 在hosts文件下配置临时域名

### Tomcat体系结构(图)
+ {{c1:: ![img](javaWeb.assets/view) }}

## HTTP

### HTTP1.0和HTTP1.1的区别
+ {{c1:: HTTP1.0协议中，客户端与web服务器建立连接后，只能获得一个web资源【短连接，获取资源后就断开连接】 }}
+ {{c1:: HTTP1.1协议，允许客户端与web服务器建立连接后，在一个连接上获取多个web资源【保持连接】 }}

### http请求结构：
+ {{c1:: 请求行：描述客户端的**请求方式**、**资源名称**，**HTTP协议版本号** }}
+ {{c1:: 请求头：描述客户端请求哪台主机，以及客户端的一些环境信息等 }}
+ {{c1:: 一个空行}}
+ {{c1:: 请求体}}

### 请求行
+ 请求行：{{c1:: `GET /java.html HTTP/1.1` }}
+ 7种请求方式：{{c1:: `POST,GET,HEAD,OPTIONS,DELETE,TRACE,PUT` }}

### POST请求与GET请求
+ 区别:{{c1:: 可以简单理解GET方式用来查询数据,POST方式用来提交数据，get的提交速度比post快 }}
+ `GET`方式：{{c1:: 在URL地址后附带的参数是有限制的，其数据容量通常不能超过1K。 }}
+ `POST`方式：{{c1:: 可以在请求的实体内容中向服务器发送数据，传送的数据量无限制。 }}

### 常见请求头
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

### HTTP响应结构
1. {{c1:: 一个状态行： 用于描述服务器对请求的处理结果。 }}
2. {{c1:: 多个消息头： 用于描述服务器的基本信息，以及数据的描述，服务器通 过这些数据的描述信息，可以通知客户端如何处理等一会儿它回送的数据}}
3. {{c1:: 一个空行 }}
4. {{c1:: 实体内容： 服务器向客户端回送的数据 }}

### 状态行
+ 格式：{{c1:: HTTP版本号　状态码　原因叙述 }}
  
  + 例：{{c1:: HTTP/1.1 200 OK }}
+ | 分类 | 分类描述                                                |
  | :--- | :------------------------------------------------------ |
  | 1xx  | {{c1:: 信息，服务器收到请求，需要请求者继续执行操作  }} |
  | 2xx  | {{c1:: 成功，操作被成功接收并处理                    }} |
  | 3xx  | {{c1:: 重定向，需要进一步的操作以完成请求            }} |
  | 4xx  | {{c1:: 客户端错误，请求包含语法错误或无法完成请求    }} |
  | 5xx  | {{c1:: 服务器错误，服务器在处理请求的过程中发生了错误}} |

### 常见响应头
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

## Servlet

### Servlet生命周期可分为5个步骤

+ **加载Servlet**:{{c1:: 当Tomcat第一次访问Servlet的时候，Tomcat会负责创建Servlet的实例 }}
+ **初始化**:{{c1:: 当Servlet被实例化后，Tomcat会**调用init()方法**初始化这个对象 }}
+ **处理服务**:{{c1:: 当浏览器访问Servlet的时候，Servlet 会**调用service()方法**处理请求 }}
+ **销毁**:{{c1:: 当Tomcat关闭时或者检测到Servlet要从Tomcat删除的时候会自动**调用destroy()方法**，让该实例释放掉所占的资源。一个Servlet如果长时间不被使用的话，也会被Tomcat自动销毁 }}
+ **卸载**:{{c1:: 当Servlet调用完destroy()方法后，等待垃圾回收。如果有需要再次使用这个Servlet，会重新调用init()方法进行初始化操作。 }}
+ 简单总结：{{c1:: 只要访问Servlet，service()就会被调用。init()只有第一次访问Servlet的时候才会被调用。 destroy()只有在Tomcat关闭的时候才会被调用。 }}

### 编写一个Hello world Servlet
1. 实现Servlet类或者HttpServlet类
2. 配置web.xml文件
  ```xml
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
  ```
3. 配置tomcat运行Servlet


### Servlet的线程安全问题
+ 背景：{{c1:: 由于Servlet是单例的，当多个用户访问Servlet的时候，**服务器会为每个用户创建一个线程**。**当多个用户并发访问Servlet共享资源的时候就会出现线程安全问题**。 }}
+ 原则：
  1. {{c1:: 如果一个**变量需要多个用户共享**，则应当在访问该变量的时候，**加同步机制synchronized (对象){}** }}
  2. {{c1:: 如果一个变量**不需要共享**，则**直接在 doGet() 或者 doPost()定义**.这样不会存在线程安全问题 }}

### load-on-startup

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

### 手工配置的缺省Servlet，覆盖掉web.xml配置的缺省Servlet
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
### ServletConfig对象

+ 作用:{{c1:: 通过此对象可以读取web.xml中配置的初始化参数`<init-param>`。 }}
+ 在Servlet中获取ServletConfig对象:{{c1::`this.getServletConfig()`}}

### ServletContext对象

+ 是什么：Tomcat启动的时候，会创建一个`ServletContext`对象，**代表当前web站点**
+ 作用：
  1. Servlet之间通信：{{c1:: ServletContext可以被称之为域对象,`主要用到ServletContext的setAttribute(String name,Object obj)方法`实现 }}
  2. 获取web站点的配置信息：{{c1:: ServletConfig获取的是配置的是单个Servlet的参数信息，ServletContext可以获取的是配置整个web站点的参数信息 }}

### ServletContext对象获取web站点的配置信息

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

### servlet中读取资源文件

1. 类路径下：{{c1:: `InputStream inputStream = servletContext.getResourceAsStream("/WEB-INF/classes/zhongfucheng/web/1.png");` }}
2. 将文件放在webRoot目录下：{{c1:: `servletContext.getResourceAsStream("2.png");` }}
3. 通过类装载器读取资源文件：{{c1:: `ServletTest.class.getClassLoader().getResourceAsStream("/zhongfucheng/web/1.png");` }}

## response与request

### 调用getOutputStream()方法向浏览器输出数据
```xml
  <!-- print()方法接收了一个字符串 -->
  response.getOutputStream().print("中国！");
  <!-- write接收字节数组 -->
  response.getOutputStream().write("你好呀我是中国".getBytes("UTF-8"));
```

### 解决Servlet响应输出中的乱码问题

1. 设置消息头的方法：{{c1:: `response.setHeader("Content-Type", "text/html;charset=UTF-8");` }}
2. 使用meta标签模拟http消息头:{{c1:: `servletOutputStream.write("<meta http-equiv='content-type' content='text/html;charset=UTF-8'>".getBytes());` }}