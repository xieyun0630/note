### Dubbo架构 [	](Dubbo_20201115082829520)

+ Dubbo架构图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/Dubbo_2.png)
+ RPC：{{c1:: 全称为remote procedure call，即**远程过程调用**。 }}
+ 解释：
| 节点      | 角色名称                               |
| --------- | -------------------------------------- |
| `Provider`  | {{c1:: 暴露服务的服务提供方                  }} |
| `Consumer`  | {{c1:: 调用远程服务的服务消费方              }} |
| `Registry`  | {{c1:: 服务注册与发现的注册中心              }} |
| `Monitor`   | {{c1:: 统计服务的调用次数和调用时间的监控中心}} |
| `Container` | {{c1:: 服务运行容器                          }} |
+ 蓝色虚线:{{c1:: 在启动时完成的功能 }}
+ 红色虚线(实线):{{c1:: 都是程序运行过程中执行的功能 }}

### Zookeeper树型目录服务 [	](Dubbo_20201115082829522)
+ ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/Dubbo_3.png)
+ 流程说明：
  - 服务提供者(Provider)启动时:{{c1:: 向 `/dubbo/com.foo.BarService/providers` 目录下写入自己的 URL 地址}}
  - 服务消费者(Consumer)启动时:{{c1:: 订阅 `/dubbo/com.foo.BarService/providers` 目录下的提供者 URL 地址。并向 `/dubbo/com.foo.BarService/consumers` 目录下写入自己的 URL 地址}}
  - 监控中心(Monitor)启动时:{{c1:: 订阅 `/dubbo/com.foo.BarService` 目录下的所有提供者和消费者 URL 地址}}

### Dubbo注册与订阅服务配置 [	](Dubbo_20201115082829525)
+ provider站点的spring配置
  ```xml
  <dubbo:application name="dubbodemo_provider" />
  <dubbo:registry address="zookeeper://192.168.134.129:2181"/>
  <dubbo:protocol name="dubbo" port="20881"></dubbo:protocol>
  <dubbo:annotation package="com.itheima.service.impl" />
  ```
  + `application`:{{c1:: 当前应用名称，用于注册中心计算应用间依赖关系，注意：消费者和提供者应用名不要一 }}
  + `registry`:{{c1:: 连接服务注册中心zookeeper ip为zookeeper所在服务器的ip }}
  + `protocol`:{{c1:: 注册协议和port,端口默认是2088 }}
  + `annotation`:{{c1:: 扫描指定包，加入`@Service`注解的类会被发布为服务 }}
  + `@Service`:{{c1:: 注意该注解使用的是Dubbo包中提供的}}
+ consumer站点的spring配置
  ```xml
  <dubbo:application name="dubbodemo-consumer" />
  <dubbo:registry address="zookeeper://192.168.134.129:2181"/>
  <dubbo:annotation package="com.itheima.controller" />
  ```
  + `application`:{{c1:: 当前应用名称，用于注册中心计算应用间依赖关系，注意：消费者和提供者应用名不要一 }}
  + `registry`:{{c1:: 连接服务注册中心zookeeper ip为zookeeper所在服务器的ip }}
  + `annotation`:{{c1:: 扫描的方式暴露接口，Controller中注入HelloService使用的是Dubbo提供的@Reference注解 }}

### Dubbo管理控制台 [	](Dubbo_20201115082829528)
+ 作用：{{c1:: 为Zookeeper注册中心的服务提供一个UI管理平台。 }}
+ 安装流程：
  + 将`dubbo-admin-2.6.0.war`文件复制到tomcat的webapps目录下
  + 启动tomcat，此war文件会自动解压
  + 修改WEB-INF下的`dubbo.properties`文件，添加`zookeeper`地址：
    ```Properites
    dubbo.registry.address=zookeeper://192.168.134.129:2181
    dubbo.admin.root.password=root
    dubbo.admin.guest.password=guest
    ```
  + 重启tomcat


### dubbo:不使用包扫描发布应用服务 [	](Dubbo_20201115082829530)
+ 包扫描配置
  ```xml
  <dubbo:annotation package="com.itheima.service" />
  ```
+ 如果不使用包扫描，也可以通过如下配置的方式来发布服务：
  ```xml
  <!-- {{c1:: -->
  <bean id="helloService" class="com.itheima.service.impl.HelloServiceImpl" />
  <dubbo:service interface="com.itheima.api.HelloService" ref="helloService" />
  <!-- }} -->
  ```
+ 作为服务消费者，可以通过如下配置来引用服务：
  ```xml
  <!-- {{c1:: -->
  <!-- 生成远程服务代理，可以和本地bean一样使用helloService -->
  <dubbo:reference id="helloService" interface="com.itheima.api.HelloService" />
  <!-- }} -->
  ```
+ 注意：{{c1:: 上面这种方式发布和引用服务，一个配置项(`<dubbo:service>` `<dubbo:reference>`)只能发布或者引用一个服务，如果有多个服务，这种方式就比较繁琐了。推荐使用包扫描方式。 }}

### dubbo协议 [	](Dubbo_20201115082829532)
+ 配置：`<dubbo:protocol name="dubbo" port="20880"/>`
+ 作用: {{c1:: 一般在provider站点下配置 }}
+ 其中Dubbo支持的协议有：dubbo、rmi、hessian、http、webservice、rest、redis等。
+ 可以在同一个工程中配置多个协议，不同服务可以使用不同的协议，例如：
  ```xml
  <!-- 多协议配置 -->
  <dubbo:protocol name="dubbo" port="20880" />
  <dubbo:protocol name="rmi" port="1099" />
  <!-- 使用dubbo协议暴露服务 -->
  <dubbo:service interface="com.itheima.api.HelloService" ref="helloService" protocol="dubbo" />
  <!-- 使用rmi协议暴露服务 -->
  <dubbo:service interface="com.itheima.api.DemoService" ref="demoService" protocol="rmi" /> 
  ```

### dubbo关闭启动时检查 [	](Dubbo_20201115082829535)

+ 配置：`<dubbo:consumer check="false"/>`
+ 作用：{{c1:: Dubbo 会在启动时缺省检查依赖的服务是否可用，不可用时会抛出异常，阻止 Spring 初始化完成. }}
+ 建议:{{c1:: 在开发阶段将check值设置为false，在生产环境下改为true。 }}

### dubbo:负载均衡 [	](Dubbo_20201115082829539)
+ 负载均衡：{{c1:: Load Balance其实就是将请求分摊到多个操作单元上进行执行，从而共同完成工作任务。 }}
+ 负载均衡策略:包含随机、轮询、最少活跃调用数、一致性Hash
+ 配置:
  + `consumer`中：{{c1:: `@Reference(check = false,loadbalance = "random")` }}
  + `provider`中：{{c1:: `@Service(loadbalance = "random")` }}
+ 在一台机器上启动多个服务提供者：{{c1:: 所以需要修改tomcat的端口号和Dubbo服务的端口号来防止端口冲突。 }}

### 解决Dubbo无法发布被事务代理的Service问题 [	](Dubbo_20201115082829541)
+ 问题原因：默认情况下Spring是基于JDK动态代理方式创建代理对象，而此代理对象的完整类名为com.sun.proxy.$Proxy42（最后两位数字不是固定的），导致Dubbo在发布服务前**进行包匹配时**无法完成匹配，进而没有进行服务的发布。
+ 断点调试的方式查看该问题：
  + ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/Dubbo_14.png)
  + Dubbo通过AnnotationBean的postProcessAfterInitialization方法进行处理
+ 解决方式操作步骤：
  1. 修改spring配置文件，开启事务控制注解支持时指定proxy-target-class属性:
    ```xml
    <!-- {{c1:: -->
    <tx:annotation-driven transaction-manager="transactionManager" proxy-target-class="true"/>
    <!-- }} -->
    ```
  2. 修改HelloServiceImpl类，在Service注解中加入interfaceClass属性
    ```java
    //{{c1::
    @Service(interfaceClass = HelloService.class)
    @Transactional
    public class HelloServiceImpl implements HelloService {
        public String sayHello(String name) {
            return "hello " + name;
        }
    }
    //}}
    ```

