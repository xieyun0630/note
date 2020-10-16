### Tomcat目录结构

+ `bin`:{{c1:: 启动和关闭需要的bat文件所在的目录}}
+ `conf`:{{c1:: 配置目录}}
  + `Catalina`:{{c1:: 用于存储针对每个虚拟机的 Context配置 }}
  + `contextxml`:{{c1:: 用于定义所有web应用均需加载的 ontext配置，如果web应用指定了自己的 context.xml该文件将被覆盖 }}
  + `catalina.properties`:{{c1:: Tomcat的环境变量配置 }}
  + `catalina.policy`:{{c1:: Tomcat运行的安全策略配置 }}
  + `loggingproperties`:{{c1:: Tomcat的日志配置文件，可以通过该文件修改 Tomcat的日志级别及日志路径等 }}
  + `serverxml`:{{c1:: Tomcat服务器的核心配置文件 }}
  + `tomcat-users.xml`:{{c1:: 定义 Tomcats默认的用户及角色映射信息配置 }}
  + `web.xml`:{{c1:: Tomcat中所有应用默认的部署描述文件，主要定义了基础 Servlet和MME映射。 }}
+ `lib`:{{c1:: tomcat运行时需要的jar包所在的目录}}
+ `logs`:{{c1:: 日志文件所在的目录}}
+ `temp`:{{c1:: tomcat运行时产生的临时文件存放的目录,不需要我们管理}}
+ `webapps`:{{c1:: 开发中最常用的目录,web应用放置到此目录下浏览器可以直接访问}}
+ `work`:{{c1:: 工作目录,tomcat运行时产生的工作文件存放在这个目录中}}

