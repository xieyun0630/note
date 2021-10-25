## 注册中心
### 微服务架构
+ 微服务架构特征
  + 单一职责：{{c1::微服务拆分粒度更小，每一个服务都对应唯一的业务能力，做到单一职责，避免重复业务开发}}
  + 面向服务：{{c1::徽服务对外暴露业务接口}}
  + 自治：{{c1::团队独立、技术独立、数据独立、部署独立}}
  + 隔离性强：{{c1::服务调用好隔离容错、降级，避免出现级联问题}}
+ 服务拆分注意事项
    1. 不同微服务，{{c1::不要重复开发相同业务}}
    2. 微服务数据独立，{{c1::不要访问其它微服务的数据库}}
    3. 微服务可以将自己的业务暴露为接口，{{c1::供其它微服务调用}}

### springCloud最简demo
+ 基础springBoot配置
    + 导入脚手架中cloud-demo工程到IDEA。
    + 导入sql,创建cloud_order与cloud_user2个库：{{c1::![image-20210930153552650](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210930153552650.png)}}
    + 修改数据库相关配置。
    + 测试:
        + order模块：http://localhost:8080/order/101
        + user模块：http://localhost:8081/user/1
+ 远程调用实现：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211011163719.png)
    + 注册RestTemplate：{{c1::
        ```java
            @MapperScan("cn.itcast.order.mapper")
            @SpringBootApplication
            public class OrderApplication {
                @Bean
                public RestTemplate restTemplate(){
                    return new RestTemplate();
                }
            }
        ```
        }}
    + 使用RestTemplate:{{c1::
        ```java
            @Service
            public class OrderService {
                @Autowired
                private OrderMapper orderMapper;
                @Autowired
                private RestTemplate restTemplate;
                public Order queryOrderById(Long orderId) {
                    // 1.查询订单
                    Order order = orderMapper.findById(orderId);
                    String url = "http://localhost:8081/user/" + order.getUserId();
                    User user = restTemplate.getForObject(url, User.class);
                    order.setUser(user);
                    // 4.返回
                    return order;
                }
            }
        ```
        }}
    + 测试结果:
        + order模块：http://localhost:8080/order/101
        
### 微服务调用关系
+ 服务提供者：{{c1::暴露接口给其它微服务调用}}
+ 服务消费者：{{c1::调用其它微服务提供的接口}}
+ 相对性：{{c1::提供者与消费者角色其实是相对的，一个服务可以同时是服务提供者和服务消费者}}

### eureka的作用
+ 消费者该如何获取服务提供者具体信息？
    + {{c1::服务提供者启动时向 eureka注册自己的信息}}
    + {{c1::eureka保存这些信息}}
    + {{c1::消费者根据服务名称向 eureka拉取提供者信息}}
+ 如果有多个服务提供者，消费者该如何选择？
    + {{c1::服务消费者利用负载均衡算法，从服务列表中挑选一个}}
+ 消费者如何感知服务提供者健康状态？
    + {{c1::服务提供者会每隔30秒向 Eurekaserver发送心跳请求，报告健康状态}}
    + {{c1::eureka会更新记录服务列表信息，心跳不正常会被别除}}
    + {{c1::消费者就可以拉取到最新的信息}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211012082657.png)}}

### 搭建eureka
+ 注册中心搭建
  1. 创建项目，引入spring-cloud-starter-netflix-eureka-server的依赖{{c1::
      ```xml
      <dependencies>
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
          </dependency>
      </dependencies>
      ```
      }}
  2. 编写启动类，添加@EnableEurekaServer注解：{{c1::
      ```java
      @EnableEurekaServer
      @SpringBootApplication
      public class EurekaApplication {
          public static void main(String[] args) {
              SpringApplication.run(EurekaApplication.class,args);
          }
      }
      ```
      }}
   1. 编写配置：{{c1::
       ```yaml
          spring:
            application:
              name: eurekaserver
          eureka:
            client:
              service-url:
                defaultZone: http://127.0.0.1:10086/eureka/
      ```
      }}
  + 测试：
      + {{c1::http://localhost:10086/}}
      + 结果:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211012090535.png)}}
+ 服务注册
  1. 在user-service项目引入spring-cloud-starter-netflix-eureka-cliente的依赖:{{c1::
      ```xml
      <dependencies>
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
          </dependency>
      </dependencies>
      ```
      }}
  2. 编写配置：{{c1::
      ```yaml
        spring:
          application:
            name: usersercie
        eureka:
          client:
            service-url:
              defaultZone: http://127.0.0.1:10086/eureka/
      ```
      }}
  
### 服务发现
  
  1. 调用其他服务时，用**服务名**代替ip、端口：{{c1::
  ```java
      @Service
      public class OrderService {
      
          @Autowired
          private OrderMapper orderMapper;
          @Autowired
          private RestTemplate restTemplate;
          public Order queryOrderById(Long orderId) {
              // 1.查询订单
              Order order = orderMapper.findById(orderId);
              String url = "http://userservice/user/" + order.getUserId();
              User user = restTemplate.getForObject(url, User.class);
              order.setUser(user);
              // 4.返回
              return order;
          }
      }
  ```
  }}
  2. 在 order- service.项目的启动类 Orderapplication中的 Resttemplate添加负載均衡注解：{{c1::
  ```java
      @MapperScan("cn.itcast.order.mapper")
      @SpringBootApplication
      public class OrderApplication {
      
          public static void main(String[] args) {
              SpringApplication.run(OrderApplication.class, args);
          }
          @Bean
          @LoadBalanced
          public RestTemplate restTemplate(){
              return new RestTemplate();
          }
      }
  ```
  }}
  3. 测试：
      + 注意：{{c1::先启动注册中心，后启动各个微服务，否则会找不到`userservice`实例}}
      + 测试URl: {{c1::`http://localhost:8080/order/102`}}

### Ribbon负载均衡
+ 负载均衡流程:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211016160246.png)}}
+ 负载均衡策略:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211016160511.png)}}
+ 常用策略解释： {{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211016160748.png)}}

### Ribbon负载均衡：配置负载均衡策略
1. 代码方式：{{c1::在xxxApplication类中，定义一个新的Rule:
    ```java
    @MapperScan("cn.itcast.order.mapper")
    @SpringBootApplication
    public class OrderApplication {
        //...
        @Bean
        public IRule randomRule(){
            return new RandomRule();
        }
    }
    ```
    }}
2. 配置文件方式：{{c1::在application ym文件中，添加新的配置:
    ```yml
    userservice:
      ribbon:
        NFLoadBalancerRuleClassName: com.netflix.loadbalancer.RandomRule
    ```
    }}
    
### Ribbon负载均衡：配置饥饿加载
+ 作用：{{c1::Ribbon默认是采用懒加载，即第一次访问时才会去创建 LoadBalanceClient,请求时间会很长，而饥饿加载则会在项目启动时创建，降低第一次访问的耗时。}}
+ 配置：{{c1::
    ```yml
    ribbon:
      eager-load:
        enabled: true 
        clients:  # 指定服务名
          - userservice
          - xxservice
    ```
    }}
### 安装Nacos注册中心
+ 下载Nacos软件包: {{c1::https://github.com/alibaba/nacos}}
    注意：{{c1::linux下载tar包}}
+ 解压到英文目录
+ 启动命令：
    + windows:{{c1:: `startup.cmd -m standalone`}}
    + linux: {{c1::`sh startup.sh -m standalone`}}
+ 端口修改位置：{{c1::`D:\MES\nacos\conf\application.properites`}}
+ 访问地址：{{c1::http://127.0.0.1:8848/nacos}}
+ 默认账号与密码：{{c1::nacos}}

### 将服务注册到Nacos注册中心
+ 在 cloud-demo父工程中添加spring-coud-alibaba的管理依赖：{{c1::
    ```xml
    <dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-alibaba-dependencies</artifactId>
        <version>2.2.5.RELEASE</version>
        <type>pom</type>
        <scope>import</scope>
    </dependency>
    ```
    }}
+ 注释掉order-service和user-service中原有的eureka依赖。
+ 添加nacos的客户端依赖：{{c1::
    ```xml
    <!-- nacos客户端依赖包 -->
    <dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
    </dependency>
    ```
    }}
+ 在服务的application.yml文件修改配置：{{c1::
    ```yaml
    spring:
      cloud:
        nacos:
          server-addr: localhost8848
    ```
    }}
+ 测试：
    + 地址：{{c1::http://127.0.0.1:8848/nacos}}
    
    
 ### Nacos服务分级存储模型
+ 一级:{{c1::一级是服务，例如 userservice}}
+ 二级:{{c1::二级是集群，例如杭州或上海}}
+ 三级:{{c1::三级是实例，例如杭州机房的某台部署了userservices的服务器}}
+ 设置实例的集群属性：{{c1::
```yaml
   spring:
     cloud:
       nacos:
         discovery:
           cluster-name: HZ
```
}}
+ 测试结果：{{c1::![image-20211001201423693](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20211001201423693.png)}}

### Nacos负载均衡配置
+ NacosRule作用：{{c1::这个规则优先会寻找与自己同集群的服务}}
+ 配置IRule：{{c1::
```yaml
    userservice:
      ribbon:
        NFLoadBalancerRuleClassName: com.netflix.loadbalancer.NacosRule
```
}}
+ 配置实例权重：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211018085654.png)}}

### Nacos环境隔离
+ namespace：{{c1::用来做环境隔离，每个 namespace都有唯一id，不同 namespace下的服务不可见}}
+ 创建namespace:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211018091455.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211018091503.png)}}
+ 为服务添加namespace:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211018091415.png)}}
+ 测试结果:{{c1::![image-20211004144639364](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20211004144639364.png)}}

### Nacos和Eureka的对比
+ 临时实例和非临时实例：{{c1::
    ```yaml
    spring:
      cloud:
        nacos:
          discovery:
            ephemeral: false # 设置为非临时实例
    ```
    }}
+ Nacos与eureka的共同点
    + 都支持服务注册和服务拉取
    + 都支持服务提供者心跳方式做健康检测
+ Nacos与Eureka的区别:
    + Nacos支持服务端主动检测提供者状态：临时实例采用心跳模式，非临时实例采用主动检测模式
    + 临时实例心跳不正常会被剔除，非临时实例则不会被别除
    + Nacos支持服务列表变更的消息推送模式，服务列表更新更及时
    + Nacos集群默认采用AP方式，当集群中存在非临时实例时，采用CP模式； Eureka采用AP方式
+ 图示:{{c1::![image-20211004145145652](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20211004145145652.png)}}


### 将配置交给 Nacos管理的步骤
+ 在 Nacosc中添加配置文件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211018114034.png)}}
+ 在微服务中引入nacos的config依赖：
    + 配置获取步骤：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211018114122.png)}}
    1. 引入 Nacose的配置管理客户端依赖：{{c1::
    ```yaml
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
        </dependency>
    ```
    }}
    2. 在userservice中的resource目录添加一个 bootstrap.yml文件，这个文件是引导文件，优先级高于application.yml:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211018114354.png)}}
+ 在微服务中添加bootstrap.yml,配置nacost地址当前环境、服务名称、文件后缀名。这些決定了程序启动时去nacos读取哪个文件
+ Nacost配置更改后，微服务可以实现热更新，方式:
    + 通过`@Vaue`注解注入，结合`@RefreshScope`刷新:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211018114647.png)}}
    + 通过`@ConfigurationProperties`注入，自动刷新:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211018114954.png)}}
+ 多环境配置共享:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211018115215.png)}}

### Nacos集群搭建
+ 主要步骤：
    - {{c1::搭建数据库，初始化数据库表结构}}
    - {{c1::下载nacos安装包}}
    - {{c1::配置nacos}}
    - {{c1::启动nacos集群}}
    - {{c1::nginx反向代理}}
+ 操作手册：nacos集群搭建.md

## Feign
### 定义和使用 Feign客户端
+ Feign的介绍:{{c1::Feign是一个声明式的htp客户端，官方地址：https://github.com/OpenFeign/feign}}
1. 引入依赖：{{c1::
```xml
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-openfeign</artifactId>
    </dependency>
```
}}
2. 在微服务启动类中开启Feign：{{c1::
```java
@EnableFeignClients
@MapperScan("cn.itcast.order.mapper")
@SpringBootApplication
public class OrderApplication {
    public static void main(String[] args) {
        SpringApplication.run(OrderApplication.class, args);
    }
}
```
}}
+ 使用Feign客户端:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021084840.png)}}
    + 调用：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021085135.png)}}

### Feign的常用配置
+ `feign.Logger.Level`：{{c1::修改日志级别,包含四种不同的级别：NONE、BASIC、HEADERS、FULL}}
+ `feign.codec.Decoder`：{{c1::响应结果的解析器,http远程调用的结果做解析，例如解析json字符串为java对象}}
+ `feign.codec.Encoder`：{{c1::请求参数编码,将请求参数编码，便于通过http请求发送}}
+ `feign.Contract`：{{c1::支持的注解格式,默认是SpringMVC的注解}}
+ `feign.Retryer`：{{c1::失败重试机制,请求失败的重试机制，默认是没有，不过会使用Ribbon的重试}}
+ 配置Feign日志有两种方式：
    + 方式一：配置文件方式
        + 全局生效：
        ```yaml
        feign:
          client:
            config:
              default: # 这里用default就是全局配置，如果是写服务名称，则是针对某个微服务的配置
                      
                loggerLevel: FULL #  日志级别 
        ```
        + 局部生效：
        ```yaml
        feign:
          client:
            config:
              userservice: # 这里用default就是全局配置，如果是写服务名称，则是针对某个微服务的配置
                      
                loggerLevel: FULL #  日志级别 
        ```
    + 方式二：java代码方式，需要先声明一个Bean：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021154438.png)}}

### Feign性能优化
+ Feign底层的客户端实现
    + URLonnection:{{c1::默认实现，不支持连接池}}
    + Apache Httplient:{{c1::支持连接池}}
    + OKttp:{{c1::支持连接池}}
+ 因此优化Feign的性能主要包括：{{c1::使用**连接池**代替默认的URLonnection，**日志级别**，最好用 basic或none}}
+ 连接池配置
    + 引入依赖：{{c1::
    ```xml
    <dependency>
        <groupId>io.github.openfeign</groupId>
        <artifactId>feign-httpclient</artifactId>
    </dependency>
    ```
    }}
    + 配置连接池：{{c1::
    ```yaml
    feign:
      client:
        config:
          default: # default全局的配置
            loggerLevel: BASIC # 日志级别，BASIC就是基本的请求和响应信息 
      httpclient:
        enabled: true # 开启feign对HttpClient的支持
        max-connections: 200 # 最大的连接数
        max-connections-per-route: 50 # 每个路径的最大连接数
    ```
    }}

### Feign的最佳实践
+ 方式一（继承）：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021155857.png)}}
+ 方式二（抽取）：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021160054.png)}}
+ 实现最佳实践方式二的步骤如下：
    + 首先创建一个module，命名为feign-api，然后引入feign的starter依赖：{{c1::
    ```xml
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-openfeign</artifactId>
    </dependency>
    ```
    }}
    + 将order-service中编写的UserClient、User、DefaultFeignConfiguration都复制到feign-api项目中：{{c1::![image-20211005015730663](upload/image-20211005015730663.png)}}
    + 在order-service中引入feign-api的依赖：{{c1::
    ```xml
        <dependency>
            <groupId>cn.itcast.demo</groupId>
            <artifactId>feign-api</artifactId>
            <version>1.0</version>
        </dependency>
    ```
    }}
    + 修改order-service中的所有与上述三个组件有关的import部分，改成导入feign-api中的包：
        + 方式一：{{c1::`@EnableFeignClients(basePackages = "cn.itcast.feign.clients")`}}
        + 方式二：{{c1::`@EnableFeignClients(clients = {UserClient.class})`}}
        + 使用图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021163820.png)}}
    + 重启测试

## 网关

### 微服务网关概念
+ 为什么需要网关:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021164903.png)}}
+ 在SpringCloud中网关的实现包括两种：{{c1::`gateway` `zuul`,Zuul是基于Servlet的实现，属于阻塞式编程。而SpringCloudGateway则是基于Spring5中提供的WebFlux，属于响应式编程的实现，具备更好的性能。}}

### 搭建网关服务
+ 创建新的module，引入SpringCloudGateway的依赖和nacos的服务发现依赖：{{c1::
    ```xml
    <!--网关依赖-->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-gateway</artifactId>
    </dependency>
    <!--nacos服务发现依赖-->
    <dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId> 
    </dependency>
    ```
    }}
+ 编写路由配置与nacos地址：{{c1::
    ```yaml
    server:
      port: 10010 # 网关端口
    spring:
      application:
        name: gateway # 服务名称
      cloud:
        nacos:
          server-addr: localhost:8848 # nacos地址
        gateway:
          routes: # 网关路由配置
            - id: user-service # 路由id，自定义，只要唯一即可
              # uri: http://127.0.0.1:8081 # 路由的目标地址 http就是固定地址
              uri: lb://userservice # 路由的目标地址 lb就是负载均衡，后面跟服务名称
              predicates: # 路由断言，也就是判断请求是否符合路由规则的条件
                - Path=/user/** # 这个是按照路径匹配，只要以/user/开头就符合要求
    ```
    }}
+ 测试：{{c1::http://localhost:10010/user/1}}
+ 搭建网关服务流程图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021165751.png)}}


### 网关可配置内容
+ `路由id`：{{c1::路由唯一标示}}
+ `uri`：{{c1::路由目的地，支持lb和http两种}}
+ `predicates`：{{c1::路由断言，判断请求是否符合要求，符合则转发到路由目的地}}
+ `filters`：{{c1::路由过滤器，处理请求或响应}}

### SpringCloudGateway路由断言工厂
+ 常见Predicate:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021170316.png)}}
+ predicates配置例：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021190333.png)

### 路由过滤器
+ 概念：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021190547.png)}}
+ spring提供了31种过滤器，其中常见的如下
    + `AddRequestHeader`:{{c1::给当前请求添加一个请求头}}
    + `RemoveRequestHeader`:{{c1::移除请求中的一个请求头}}
    + `AddResponseHeader`:{{c1::给响应结果中添加一个响应头}}
    + `RemoveResponseHeader`:{{c1::从响应结果中移除有一个响应头}}
    + `RequestRateLimiter`:{{c1::限制请求的流量}}
    + 参考文档：https://docs.spring.io/spring-cloud-gateway/docs/current/reference/html/#gatewayfilter-factories
+ 案例，给所有进入 userservice的请求添加一个请求头：{{c1::
    ```yaml
    spring:
      cloud:
        gateway:
          routes: 
            - id: user-service
              uri: lb://userservice
              predicates:
                - Path=/user/**
              filters:
                - AddRequestHeader= Truth, Itcast is freaking awesome! #添加请求头
    ```
    }}
    + 测试效果：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021191825.png)
 + 全局配置以上效果：{{c1::
     ```yaml
     spring:
       cloud:
         gateway:
           routes: 
             - id: user-service
               uri: lb://userservice
               predicates:
                 - Path=/user/**
           default-filters:
             - AddRequestHeader= Truth, Itcast is freaking awesome! #添加请求头
     ```
     }}

 ### 路由过滤器：自定义全局过滤器
  + 需求：定义全局过滤器，拦截请求，判断请求的参数是否满足下面条件：
  + 参数中是否有 authorization
  + authorization参数值是否为 admin
  + 如果同时满足则放行，否则拦截
  + 实现:
   1. 自定义类，实现GlobalFilter接口，添加@Order注解：{{c1::
   ```java
    @Order(-1)
    @Component
    public class AuthorizeFilter implements GlobalFilter {
            @Override
        public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
                // 1.获取请求参数
            MultiValueMap<String, String> params = exchange.getRequest().getQueryParams();
            // 2.获取authorization参数
            String auth = params.getFirst("authorization");
            // 3.校验
            if ("admin".equals(auth)) {
                    // 放行
                return chain.filter(exchange);
            }
            // 4.拦截
            // 4.1.禁止访问
            exchange.getResponse().setStatusCode(HttpStatus.FORBIDDEN);
            // 4.2.结束处理
            return exchange.getResponse().setComplete();
        }
    }
   ```
   }}
   + 测试：{{c1::localhost:10010/user/1?authorization=admin}}
   
 ### 路由过滤器：过滤器执行顺序
 + 请求进入网关会碰到三类过滤器：{{c1::当前路由的过滤器、 DefaultFilter、 GlobalFilter}}
 + 请求路由后，{{c1::会将当前路由过滤器和 DefaultFilter、 GlobalFilter,合并到个过滤器链（集合）中，排序后依次执行每个过滤器}}
 + 路由过滤器、defaultFilter、全局过滤器的执行顺序？
    + order值越小，{{c1::优先级越高}}
    + 当order值一样时，{{c1::顺序是defaultFilter最先，然后是局部的路由过滤器，最后是全局过滤器}}
   
### 网关的cors跨域配置
+ 跨域：域名不一致就是跨域，主要包括2种情况：
    + {{c1::域名不同： www.taobao.com 和 www.taobao.org 和 www.jd.com 和 miaosha.jd.com}}
    + {{c1::域名相同，端口不同：localhost:8080和localhost8081}}
+ 跨域问题：{{c1::浏览器禁止请求的发起者与服务端发生跨域ajax请求，请求被浏览器拦截的问题}}
+ 解决方案：CORS
+ 所需网关配置如下：{{c1::
    ```yaml
    spring:
      cloud:
        gateway:
          # ...
          globalcors: # 全局的跨域处理
            add-to-simple-url-handler-mapping: true # 解决options请求被拦截问题
            corsConfigurations:
              '[/**]':
                allowedOrigins: # 允许哪些网站的跨域请求 
                  - "http://localhost:8090"
                  - "http://www.leyou.com"
                allowedMethods: # 允许的跨域ajax的请求方式
                  - "GET"
                  - "POST"
                  - "DELETE"
                  - "PUT"
                  - "OPTIONS"
                allowedHeaders: "*" # 允许在请求中携带的头信息
                allowCredentials: true # 是否允许携带cookie
                maxAge: 360000 # 这次跨域检测的有效期
    ```
    }}
+ 测试脚本：{{c1::
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
    <pre>
    spring:
      cloud:
        gateway:
          globalcors: # 全局的跨域处理
            add-to-simple-url-handler-mapping: true # 解决options请求被拦截问题
            corsConfigurations:
              '[/**]':
                allowedOrigins: # 允许哪些网站的跨域请求
                  - "http://localhost:8090"
                  - "http://www.leyou.com"
                allowedMethods: # 允许的跨域ajax的请求方式
                  - "GET"
                  - "POST"
                  - "DELETE"
                  - "PUT"
                  - "OPTIONS"
                allowedHeaders: "*" # 允许在请求中携带的头信息
                allowCredentials: true # 是否允许携带cookie
                maxAge: 360000 # 这次跨域检测的有效期
    </pre>
    </body>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>
      axios.get("http://localhost:10010/user/1?authorization=admin")
      .then(resp => console.log(resp.data))
      .catch(err => console.log(err))
    </script>
    </html>
    ```
    }}
    + 结果：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021205729.png)}}
    
## docker

### docker架构
+ Docker是一个CS架构的程序，由两部分组成：
    + 服务端(server)：{{c1::Docker守护进程，负责处理Docker指令，管理镜像、容器等}}
    + 客户端(client)：{{c1::通过命令或RestAPI向Docker服务端发送指令。可以在本地或远程向服务端发送指令}}
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021210222.png)}}


### 镜像相关命令
+ 总览图示：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021211815.png)
+ 实例:从 Dockerhubr中拉取一个 nginx镜像并查看:![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021212035.png)
+ 实例：利用docker save将nginx镜像导出磁盘，然后再通过load加载回来：
    + {{c1::步骤一：利用docker xx --help命令查看docker save和docker load的语法}}
    + {{c1::步骤二：使用docker save导出镜像到磁盘 }}
    + {{c1::步骤三：使用docker load加载镜像}}
    + 实操：
        +{{c1:: ![image-20211005050511814](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20211005050511814.png)}}
        +{{c1:: ![image-20211005050559651](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20211005050559651.png)}}

### 容器相关命令
+ 总览图示：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021212708.png)
+ 查看各个容器内存占用：`docker stats`
### 数据卷相关命令
+ 数据卷操作的基本语法：{{c1::`docker volume [COMMAND]`}}
    + `create`: {{c1::创建一个volume}}
    + `inspect`: {{c1::显示一个或多个volume的信息}}
    + `ls`: {{c1::列出所有的volume}}
    + `prune`: {{c1::删除未使用的volume}}
    + `rm`: {{c1::删除一个或多个指定的volume}}
+ 挂载数据卷:{{c1::
    ```bash
      docker run \
      --name mn \
      -v html:/root/html \
      -p 8080:80
      nginx \
    ```
    }}
    + 注意：{{c1::如果容器运行时volume不存在，会自动被创建出来}}
+ 实例:创建一个数据卷，并查看数据卷在宿主机的目录位置:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021220146.png)}}
+ 实例:创建一个nginx容器，修改容器内的html目录内的index.html内容:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021220347.png)}}

### 自定义镜像
+ 镜像结构：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021220807.png)
+ 什么是Dockerfile：{{c1::Dockerfile就是一个文本文件，其中包含一个个的指令(Instruction)，用指令来说明要执行什么操作来构建镜像。每一个指令都会形成一层Layer。}}
+ dockerfile常见指令：
    | **FROM**   | **指定基础镜像**                             | **FROM  centos:6**          |
    | ---------- | -------------------------------------------- | --------------------------- |
    | ENV        | {{c1:: 设置环境变量，可在后面指令使用               }}| {{c1:: ENV key value               }}|
    | COPY       | {{c1:: 拷贝本地文件到镜像的指定目录                 }}| {{c1:: COPY ./mysql-5.7.rpm /tmp   }}|
    | RUN        | {{c1:: 执行Linux的shell命令，一般是安装过程的命令   }}| {{c1:: RUN yum install gcc         }}|
    | EXPOSE     | {{c1:: 指定容器运行时监听的端口，是给镜像使用者看的 }}| {{c1:: EXPOSE 8080                 }}|
    | ENTRYPOINT | {{c1:: 镜像中应用的启动命令，容器运行时调用         }}| {{c1:: ENTRYPOINT java -jar xx.jar }}|

### dockerfile实际案例
+ 需求：基于Ubuntu镜像构建一个新镜像，运行一个java项目{{c1::
    ```dockerfile
    # 指定基础镜像
    FROM ubuntu:16.04
    # 配置环境变量，JDK的安装目录
    ENV JAVA_DIR=/usr/local
    
    # 拷贝jdk和java项目的包
    COPY ./jdk8.tar.gz $JAVA_DIR/
    COPY ./docker-demo.jar /tmp/app.jar
    
    # 安装JDK
    RUN cd $JAVA_DIR \
     && tar -xf ./jdk8.tar.gz \
     && mv ./jdk1.8.0_144 ./java8
    
    # 配置环境变量
    ENV JAVA_HOME=$JAVA_DIR/java8
    ENV PATH=$PATH:$JAVA_HOME/bin
    
    # 暴露端口
    EXPOSE 8090
    # 入口，java项目的启动命令
    ENTRYPOINT java -jar /tmp/app.jar
    ```
    }}
+ 基于java:8-alpine镜像，将一个Java项目构建为镜像：{{c1::
    ```dockerfile
    FROM java:8-alpine
    COPY ./app.jar /tmp/app.jar
    EXPOSE 8090
    ENTRYPOINT java -jar /tmp/app.jar
    ```
    }}
    
### DockerCompose安装
+ Linux下需要通过命令下载：
    ```sh
    # 安装
    curl -L https://github.com/docker/compose/releases/download/1.23.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    ```
    + 注意：下载到/usr/local/bin目录，path环境变量默认有该目录
+ 修改文件权限：
    ```sh
    # 修改权限
    chmod +x /usr/local/bin/docker-compose
    ```
+ 添加Base自动补全命令功能：{{c1::
```sh
# 补全命令
curl -L https://raw.githubusercontent.com/docker/compose/1.29.1/contrib/completion/bash/docker-compose > /etc/bash_completion.d/docker-compose
```
    + 如果这里出现错误，需要修改自己的hosts文件：
    ```sh
    echo "199.232.68.133 raw.githubusercontent.com" >> /etc/hosts
    ```
}}

### DockerCompose
+ 作用：{{c1::帮助我们快速部署分布式应用，无需一个个微服务去构建镜像和部署。相当于一次性执行N次docker run命令}}
+ 案例：利用DockerCompose部署微服务集群
    + 微服务工程目录：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211021224455.png)
    + 各个docker-file文件定义：
        + gateway:{{c1::
        ```dockerfile
        FROM java:8-alpine
        COPY ./app.jar /tmp/app.jar
        ENTRYPOINT java -jar /tmp/app.jar
        ```
        }}
        + mysql:无
        + order-service:{{c1::
        ```dockerfile
        FROM java:8-alpine
        COPY ./app.jar /tmp/app.jar
        ENTRYPOINT java -jar /tmp/app.jar
        ```
        }}
        + user-service:{{c1::
        ```dockerfile
        FROM java:8-alpine
        COPY ./app.jar /tmp/app.jar
        ENTRYPOINT java -jar /tmp/app.jar
        ```
        }}
    + docker-compose定义：{{c1::
    ```yaml
    version: "3.2"
    services:
      nacos:
        image: nacos/nacos-server
        environment:
          MODE: standalone
        ports:
          - "8848:8848"
      mysql:
        image: mysql:5.7.25
        environment:
          MYSQL_ROOT_PASSWORD: 123
        volumes:
          - "$PWD/mysql/data:/var/lib/mysql"
          - "$PWD/mysql/conf:/etc/mysql/conf.d/"
      userservice:
        build: ./user-service
      orderservice:
        build: ./order-service
      gateway:
        build: ./gateway
        ports:
          - "10010:10010"
    ```
    }}

### Docker镜像仓库
+ 使用docker-compose搭建镜像仓库:{{c1::
    ```yaml
    version: '3.0'
    services:
      registry:
        image: registry
        volumes:
          - ./registry-data:/var/lib/registry
      ui:
        image: joxit/docker-registry-ui:static
        ports:
          - 8080:80
        environment:
          - REGISTRY_TITLE=Yun私有仓库
          - REGISTRY_URL=http://registry:5000
        depends_on:
          - registry
    ```
    }}
1. 重新tag本地镜像，名称前缀为私有仓库的地址：192.168.150.101:8080/：{{c1::
     ```sh
    docker tag nginx:latest 192.168.150.101:8080/nginx:1.0 
     ```
     }}
2. 推送镜像：{{c1::
    ```sh
    docker push 192.168.150.101:8080/nginx:1.0 
    ```
    }}
3. 拉取镜像：{{c1::
    ```sh
    docker pull 192.168.150.101:8080/nginx:1.0 
    ```
    }}
+ 额外：配置Docker信任地址：
我们的私服采用的是http协议，默认不被Docker信任，所以需要做一个配置：
```sh
# 打开要修改的文件
vi /etc/docker/daemon.json
# 添加内容：注意这里是当前docker主机的地址
"insecure-registries":["http://192.168.150.101:8080"]
# 重加载
systemctl daemon-reload
# 重启docker
systemctl restart docker
```

## MQ

### 同步VS异步
+ 异步通信存在问题
    + **耦合度高**：{{c1::每次加入新的需求，都要修改原来的代码}}
    + **性能下降**：{{c1::调用者需要等待服务提供者响应，如果调用链过长则响应时间等于每次调用的时间之和}}
    + **资源浪费**：{{c1::调用链中的每个服务在等待响应过程中，不能释放请求占用的资源，高井发场景下会极度浪费系统资源}}
    + **级联失败**：{{c1::如果服务提供者出现问题所有调用方都会跟若出问题如同多米诺骨牌一样，迅速导致整个服务群故障}}
+ 异步通信的优点：{{c1::耦合度低、吞吐量提升、故障隔离、流量削峰}}
+ 异步通信的缺点：{{c1::依赖于**Brokers的可靠性、安全性、吞吐能力**、**架构复杂了**，业务没有明显的流程线，不好追踪管理}}
+ 常见MQ技术：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211022084259.png)

### RabbitMQ安装
+ 在docker中拉取：{{c1::`docker pull rabbitmq:3-management`}}
+ 运行容器：{{c1::
```sh 
docker run \
 -e RABBITMQ_DEFAULT_USER=itcast \
 -e RABBITMQ_DEFAULT_PASS=123321 \
 --name mq \
 --hostname mq1 \
 -p 15672:15672 \
 -p 5672:5672 \
 -d \
 rabbitmq:3-management
```
}}
+ 测试：{{c1::http://81.69.43.171:15672/#/}}

### Rabbit MQ的结构和概念
RabbitMQ中的几个概念：
    + `channel`：{{c1::操作MQ的工具}}
    + `exchange`：{{c1::路由消息到队列中}}
    + `queue`：{{c1::缓存消息}}
    + `virtual host`：{{c1::虚拟主机，是对queue、exchange等资源的逻辑分组}}
+ 关系图示：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211022092811.png)

### RabbitMQ常见消息模型
+ 5种常见消息模型：
    + {{c1::基本消息队列( Basicqueue)}}
    + {{c1::工作消息队列( Workqueue)}}
    + {{c1::Fanout Exchange(广播)}}
    + {{c1::Direct Exchange(路由)}}
    + {{c1::Topic Exchange(主题)}}
+ 图示：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201121084131.png)

### 使用SpringAMQP发送消息
+ 引入AMQP依赖:{{c1::
  ```xml
  <!--AMQP依赖，包含RabbitMQ-->
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-amqp</artifactId>
  </dependency>
  ```
  }}
+ 配置mq连接信息：{{c1::
  ```yaml
  spring:
    rabbitmq:
      host: 192.168.150.101 # 主机名
      port: 5672 # 端口
      virtual-host: / # 虚拟主机 
      username: itcast # 用户名
      password: 123321 # 密码
  ```
  }}
+ 发送消息：{{c1::
  ```java
  @RunWith(SpringRunner.class)
  @SpringBootTest
  public class SpringAmqpTest {
        @Autowired
      private RabbitTemplate rabbitTemplate;
      @Test
      public void testSimpleQueue() { 
            String queueName = "simple.queue";
          String message = "hello, spring amqp!";
          rabbitTemplate.convertAndSend(queueName, message);
      }
  }
  ```
  }}
  + 测试:{{c1::![image-20211006112733007](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20211006112733007.png)}}
+ 接收消息:
  + 在consumer中编写消费逻辑，监听`simple.queue`：{{c1::
  ```yaml
  spring:
    rabbitmq:
      host: 192.168.150.101 # 主机名
      port: 5672 # 端口
      virtual-host: / # 虚拟主机 
      username: itcast # 用户名
      password: 123321 # 密码
  ```
  }}
  + 接收消息：{{c1::
  ```java
  @Component
  public class SpringRabbitListener {
    
      @RabbitListener(queues = "simple.queue")
      public void listenSimpleQueueMessage(String msg) throws InterruptedException {
            System.out.println("spring 消费者接收到消息 ：【" + msg + "】");
      }
  }
  ```
  }}

### 模拟WorkQueue，实现一个队列绑定多个消费者
+ 在publisher服务中添加一个测试方法，循环发送50条消息到simple.queue队列
  ```java
  @Test
  public void testWorkQueue() throws InterruptedException {
        // 队列名称
      String queueName = "simple.queue";
      // 消息
      String message = "hello, message__";
      for (int i = 0; i < 50; i++) {
        // 发送消息
        rabbitTemplate.convertAndSend(queueName, message + i);
        // 避免发送太快
        Thread.sleep(20);
      }
  }
  ```
+ 在consumer服务中添加一个消费者，也监听simple.queue：
  ```java
  @RabbitListener(queues = "simple.queue")
  public void listenSimpleQueueMessage(String msg) throws InterruptedException {
        System.out.println("spring 消费者1接收到消息：【" + msg + "】");
      Thread.sleep(25);
  }
  @RabbitListener(queues = "simple.queue") 
  public void listenSimpleQueueMessage2(String msg) throws InterruptedException {
        System.err.println("spring 消费者2接收到消息：【" + msg + "】");
      Thread.sleep(100);
  }
  ```
+ 消费预取限制:{{c1::
  ```yaml
  spring:
    rabbitmq:
      host: 192.168.150.101 # 主机名
      port: 5672 # 端口
      virtual-host: / # 虚拟主机 
      username: itcast # 用户名
      password: 123321 # 密码
      listener:
        simple:
          prefetch: 1 # 每次只能获取一条消息，处理完成才能获取下一个消息
  ```
  }}

### 利用SpringAMQP演示FanoutExchange的使用
1. 在consumer服务声明Exchange、Queue、Binding：
   1. Exchange类体系：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211024130010.png)}}
   2. 编写配置类：{{c1::
   ```java
   @Configuration
   public class FanoutConfig {
         // 声明FanoutExchange交换机
       @Bean
       public FanoutExchange fanoutExchange(){
             return new FanoutExchange("itcast.fanout");
       }
       // 声明第1个队列
       @Bean
       public Queue fanoutQueue1(){
             return new Queue("fanout.queue1");
       }
       //绑 定队列1和交换机
       @Bean
       public Binding bindingQueue1(Queue fanoutQueue1, FanoutExchange fanoutExchange){
             return BindingBuilder.bind(fanoutQueue1).to(fanoutExchange);
       }
       //  ... 略， 以相同方式声明第2个队列，并完成绑定
   }
   ```
   }}
2. 在consumer服务中，编写两个消费者方法，分别监听fanout.queue1和fanout.queue2:{{c1::
   ```java
    @RabbitListener(queues = "fanout.queue1")
    public void listenFanoutQueue1(String msg) {
          System.out.println("消费者1接收到Fanout消息：【" + msg + "】");
    }
    
    @RabbitListener(queues = "fanout.queue2") 
    public void listenFanoutQueue2(String msg) {
          System.out.println("消费者2接收到Fanout消息：【" + msg + "】");
    }
   ```
   }}
3. 在publisher中编写测试方法，向itcast.fanout发送消息:{{c1::
   ```java
   @Test
   public void testFanoutExchange() {
         // 队列名称
       String exchangeName = "itcast.fanout";
       // 消息
       String message = "hello, everyone!";
       // 发送消息，参数分别是：交互机名称、RoutingKey（暂时为空）、消息 
       rabbitTemplate.convertAndSend(exchangeName, "", message);
   }
   ```
   }}
4. 测试：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20211006123055229.png)}}

### 利用SpringAMQP演示DirectExchange的使用
+ 在consumer服务中，编写两个消费者方法，分别监听direct.queue1和direct.queue2,利用@RabbitListener声明Exchange、Queue、RoutingKey:{{c1::
  ```java
  @RabbitListener(bindings = @QueueBinding(
                  value = @Queue(name = "direct.queue1"),
                  exchange = @Exchange(name = "itcast.direct", type = ExchangeTypes.DIRECT),
                  key = {"red", "blue"}
  ))
  public void listenDirectQueue1(String msg){
        System.out.println("消费者1接收到Direct消息：【"+msg+"】");
  }
  
  @RabbitListener(bindings = @QueueBinding(
                  value = @Queue(name = "direct.queue2"),
                  exchange = @Exchange(name = "itcast.direct", type = ExchangeTypes.DIRECT),
                  key = {"red", "yellow"}
  ))
  public void listenDirectQueue2(String msg){
        System.out.println("消费者2接收到Direct消息：【"+msg+"】 ");
  }
  ```
  }}
+ 在publisher中编写测试方法，向itcast. direct发送消息:{{c1::
  ```java
  @Test
  public void testDirectExchange() {
        // 队列名称
      String exchangeName = "itcast.direct";
      // 消息 
      String message = "红色警报！日本乱排核废水，导致海洋生物变异，惊现哥斯拉！";
      // 发送消息，参数依次为：交换机名称，RoutingKey，消息
      rabbitTemplate.convertAndSend(exchangeName, "red", message);
  }
  ```
  }}
+ Direct交换机与Fanout交换机的差异？
  + {{c1::Fanout交换机将消息路由给每一个与之绑定的队列}}
  + {{c1::Direct交换机根据RoutingKey判断路由给哪个队列}}
  + {{c1::如果多个队列具有相同的RoutingKey，则与Fanout功能类似}}

### 发布订阅-TopicExchange
+ 结构图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211024131353.png)}}
+ 利用SpringAMQP演示TopicExchange的使用
  + 在consumer服务中，编写两个消费者方法，分别监听topic.queue1和topic.queue2，并利用@RabbitListener声明Exchange、Queue、RoutingKey：{{c1::
  ```java
  @RabbitListener(bindings = @QueueBinding(
                  value = @Queue(name = "topic.queue1"),
                  exchange = @Exchange(name = "itcast.topic", type = ExchangeTypes.TOPIC),
                  key = "china.#"
  ))
  public void listenTopicQueue1(String msg){
    System.out.println("消费者1接收到Topic消息：【"+msg+"】");
  }
   
  @RabbitListener(bindings = @QueueBinding(
                  value = @Queue(name = "topic.queue2"),
                  exchange = @Exchange(name = "itcast.topic", type = ExchangeTypes.TOPIC),
                  key = "#.news"
  ))
  public void listenTopicQueue2(String msg){
    System.out.println("消费者2接收到Topic消息：【"+msg+"】");
  }
  ```
  }}
  + 在publisher中编写测试方法，向itcast. topic发送消息：{{c1::
  ```java
  @Test
  public void testTopicExchange() {
        // 队列名称
      String exchangeName = "itcast.topic";
      // 消息 
      String message = "喜报！孙悟空大战哥斯拉，胜!";
      // 发送消息
      rabbitTemplate.convertAndSend(exchangeName, "china.news", message);
  }
  ```
  }}

### SpringAMQP消息转换器
+ 作用:{{c1::Spring的对消息对象的处理是由org.springframework.amqp.support.converter.MessageConverter来处理的。而默认实现是SimpleMessageConverter，基于JDK的ObjectOutputStream完成序列化。}}
+ 自定义MessageConverter：
  + 在publisher或consumer服务引入依赖：{{c1::
    ```xml
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
    </dependency>
    ```
    }}
  + 声明具体的MessageConverter：{{c1::
    ```xml
    @Bean
    public MessageConverter jsonMessageConverter(){
          return new Jackson2JsonMessageConverter(); 
    }
    ```
    }}
  + 在publisher中发送消息:{{c1::
    ```java
    @Test
    public void testSendMap() throws InterruptedException {
          // 准备消息
        Map<String,Object> msg = new HashMap<>();
        msg.put("name", "Jack"); 
        msg.put("age", 21);
        // 发送消息
        rabbitTemplate.convertAndSend("object.queue", msg);
    }
    ```
    }}
  + 测试：{{c1::![image-20211006125838868](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20211006125838868.png)}}
  + 在consumer接收消息：{{c1::
    ```java
    @RabbitListener(queues = "object.queue")
    public void listenObjectQueue(Map<String, Object> msg) {
          System.out.println("收到消息：【" + msg + "】"); 
    }
    ```
    }}

## elasticsearch

### elasticsearch技术
+ 什么是elasticsearch：{{c1::一个开源的分布式搜索引擎，可以用来实现搜索、日志统计、分析、系统监控等功能}}
+ 什么是elastic stack（ELK）：{{c1::是以elasticsearch为核心的技术栈，包括beats、Logstash、kibana、elasticsearch}}
+ 什么是Lucene：{{c1::是Apache的开源搜索引擎类库，提供了搜索引擎的核心API}}

### 倒排索引
+ elasticsearch采用倒排索引：
  + 文档（document）：每条数据就是一个文档
  + 词条（term）：文档按照语义分成的词语
+ 图示：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211024164538.png)
+ 倒排索引中包含两部分内容：
  + 词条词典（Term Dictionary）：{{c1::记录所有词条，以及词条与倒排列表（Posting List）之间的关系，会给词条创建索引，提高查询和插入效率}}
  + 倒排列表（Posting List）：{{c1::记录词条所在的文档id、词条出现频率 、词条在文档中的位置等信息}}
    + 文档id：{{c1::用于快速获取文档}}
    + 词条频率（TF）：{{c1::文档在词条出现的次数，用于评分}}
  + 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211024165110.png)}}

### elasticsearch基本概念：
+ 文档：{{c1::elasticsearch是面向文档存储的，可以是数据库中的一条商品数据，一个订单信息。文档数据会被序列化为json格式后存储在elasticsearch中。}}
+ 索引（index）：{{c1::相同类型的文档的集合}}映射（mapping）：索引中文档的字段约束信息，类似表的结构约束
+ 映射（mapping）：{{c1::索引中文档的字段约束信息，类似表的结构约束}}
+ 概念对比：
  | **MySQL** | **Elasticsearch** | **说明**                                                     |
  | --------- | ----------------- | ------------------------------------------------------------ |
  | Table     | Index             | {{c1::索引(index)，就是文档的集合，类似数据库的表(table)           }}|
  | Row       | Document          | {{c1::文档（Document），就是一条条的数据，类似数据库中的行（Row），文档都是JSON格式 }}|
  | Column    | Field             | {{c1::字段（Field），就是JSON文档中的字段，类似数据库中的列（Column） }}|
  | Schema    | Mapping           | {{c1::Mapping（映射）是索引中文档的约束，例如字段类型约束。类似数据库的表结构（Schema） }}|
  | SQL       | DSL               | {{c1::DSL是elasticsearch提供的JSON风格的请求语句，用来操作elasticsearch，实现CRUD }}|

### elasticsearch环境安装
+ 安装ES：
  + 拉取：{{c1::`docker pull elasticsearch:7.12.1`}}
  + 创建容器：{{c1::
  ```sh
  docker run -d \
	--name es \
    -e "ES_JAVA_OPTS=-Xms256m -Xmx256m" \
    -e "discovery.type=single-node" \
    -v es-data:/usr/share/elasticsearch/data \
    -v es-plugins:/usr/share/elasticsearch/plugins \
    --privileged \
    --network es-net \
    -p 9200:9200 \
    -p 9300:9300 \
    elasticsearch:7.12.1
  ```
  }}
  + 命令解释：
      - `-e "cluster.name=es-docker-cluster"`：{{c1::设置集群名称}}
      - `-e "http.host=0.0.0.0"`：{{c1::监听的地址，可以外网访问}}
      - `-e "ES_JAVA_OPTS=-Xms512m -Xmx512m"`：{{c1::内存大小}}
      - `-e "discovery.type=single-node"`：{{c1::非集群模式}}
      - `-v es-data:/usr/share/elasticsearch/data`：{{c1::挂载逻辑卷，绑定es的数据目录}}
      - `-v es-logs:/usr/share/elasticsearch/logs`：{{c1::挂载逻辑卷，绑定es的日志目录}}
      - `-v es-plugins:/usr/share/elasticsearch/plugins`：{{c1::挂载逻辑卷，绑定es的插件目录}}
      - `--privileged`：{{c1::授予逻辑卷访问权}}
      - `--network es-net` ：{{c1::加入一个名为es-net的网络中}}
      - `-p 9200:9200`：{{c1::端口映射配置}}
  - 测试：`http://81.69.43.171:9200`
+ 安装kibana：
  + 拉取：{{c1::`docker pull elasticsearch:7.12.1`}}
  + 创建容器：{{c1::
  ```sh
  docker run -d \
  --name kibana \
  -e ELASTICSEARCH_HOSTS=http://es:9200 \
  --network=es-net \
  -p 5601:5601  \
  kibana:7.12.1
  ```
  }}
  + 命令解释：
    - `--network es-net`：{{c1::加入一个名为es-net的网络中，与elasticsearch在同一个网络中}}
    - `-e ELASTICSEARCH_HOSTS=http://es:9200"`：{{c1::设置elasticsearch的地址，因为kibana已经与elasticsearch在一个网络，因此可以用容器名直接访问elasticsearch}}
    - `-p 5601:5601`：{{c1::端口映射配置}}
  - 测试：`http://81.69.43.171:5601`
+ 安装IK分词器：{{c1::
  ```sh
  # 进入容器内部
  docker exec -it elasticsearch /bin/bash
  # 在线下载并安装
  ./bin/elasticsearch-plugin  install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v7.12.1/elasticsearch-analysis-ik-7.12.1.zip
  #退出
  exit
  #重启容器
  docker restart elasticsearch
  ```
  }}
+ IK分词器的拓展和停用词典：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20211024183800.png)}}
+ IK分词器有几种模式？
  + `ik_smart`：{{c1::智能切分，粗粒度}}
  + `ik_max_word`：{{c1::最细切分，细粒度}}

