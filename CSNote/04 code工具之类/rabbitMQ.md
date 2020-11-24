## 概述

### 什么是消息中间件
+ 为什么使用MQ: {{c1:: 在项目中，可将一些无需即时返回且耗时的操作提取出来，进行**异步处理**，而这种异步处理的方式大大的节省了服务器的请求响应时间，从而**提高**了**系统**的**吞吐量**。 }}
+ 开发中消息队列通常有如下应用场景：
  1. 任务**异步**处理:{{c1:: 将不需要同步处理的并且耗时长的操作由消息队列通知消息接收方进行异步处理。提高了应用程序的响应时间。 }}
  2. 应用程序**解耦合**:{{c1:: MQ相当于一个中介，生产方通过MQ与消费方交互，它将应用程序进行解耦合。 }}
  3. **削峰填谷**:{{c1:: 如订单系统，在下单的时候就会往数据库写数据。但是数据库只能支撑每秒1000左右的并发写入，并发量再高就容易宕机。低峰期的时候并发也就100多个，但是在高峰期时候，并发量会突然激增到5000以上，这个时候数据库肯定卡死了。 }}
+ MQ是消息通信的模型；实现MQ的大致有两种主流方式：{{c1:: AMQP、JMS }}

### MQ 的劣势

+ 系统可用性降低:{{c1:: 系统引入的外部依赖越多，系统稳定性越差。一旦 MQ 宕机，就会对业务造成影响。如何保证MQ的高可用？}}
+ 系统复杂度提高:{{c1:: MQ 的加入大大增加了系统的复杂度，以前系统间是同步的远程调用，现在是通过 MQ 进行异步调用。如何保证消息没有被重复消费？怎么处理消息丢失情况？那么保证消息传递的顺序性？}}
+ 一致性问题:{{c1:: A 系统处理完业务，通过 MQ 给B、C、D三个系统发消息数据，如果 B 系统、C 系统处理成功，D 系统处理失败。如何保证消息数据处理的一致性？}}


### AMQP 与 JMS 区别
+ AMQP:{{c1:: AMQP（Advanced Message Queue 高级消息队列协议）是一种协议，更准确的说是一种binary wire-level protocol（链接协议）。这是其和JMS的本质差别，AMQP不从API层进行限定，而是直接定义网络交换的数据格式。 }}
+ JMS:{{c1:: JMS即Java消息服务（JavaMessage Service）应用程序接口，是一个Java平台中关于面向消息中间件（MOM）的API，用于在两个应用程序之间，或分布式系统中发送消息，进行异步通信。 }}
+ 区别：
  1. 消息操作：{{c1:: JMS是定义了统一的接口，来对消息操作进行统一；AMQP是通过规定协议来统 一数据交互的格式}}
  2. 跨语言: {{c1:: JMS限定了必须使用Java语言；AMQP只是协议，不规定实现方式，因此是跨语言的。}}
  3. 消息模式: {{c1:: JMS规定了两种消息模式；而AMQP的消息模式更加丰富 }}

### RabbitMQ概要
+ RabbitMQ提供了6种模式：{{c1:: 简单模式，work模式，Publish/Subscribe发布与订阅模式，Routing路由模式，Topics主题模式，RPC远程调用模式； }}
+ 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201121084131.png) }}

### RabbitMQ相关概念

+ `Broker` ：接收和分发消息的应用，RabbitMQ Server就是 Message Broker
+ `Virtual host` ：出于多租户和安全因素设计的，把 AMQP 的基本组件划分到一个虚拟的分组中，类似于网络中的 namespace 概念。当多个不同的用户使用同一个 RabbitMQ server 提供的服务时，可以划分出多个vhost，每个用户在自己的 vhost 创建 exchange／queue 等
+ `Connection` ：publisher／consumer 和 broker 之间的 TCP 连接
+ `Channel` ：如果每一次访问 RabbitMQ 都建立一个 Connection，在消息量大的时候建立 TCP Connection的开销将是巨大的，效率也较低。Channel 是在 connection 内部建立的逻辑连接，如果应用程序支持多线程，通常每个thread创建单独的 channel 进行通讯，AMQP method 包含了channel id 帮助客户端和message broker 识别 channel，所以 channel 之间是完全隔离的。Channel 作为轻量级的 Connection极大减少了操作系统建立 TCP connection 的开销
+ `Exchange` ：message 到达 broker 的第一站，根据分发规则，匹配查询表中的 routing key，分发消息到queue中去。常用的类型有 ：`direct (point-to-point)`, `topic (publish-subscribe)` and `fanout (multicast)`
+ `Queue` ：消息最终被送到这里等待 consumer 取走
+ `Binding` ：exchange 和 queue 之间的虚拟连接，binding 中可以包含 routing key。Binding 信息被保存
到 exchange 中的查询表中，用于 message 的分发依据


### 简单/工作模式：生产者
+ 核心代码示例：
```Java
    ConnectionFactory connectionFactory = new ConnectionFactory();
      connectionFactory.setHost("localhost");
      connectionFactory.setPort(5672);
      connectionFactory.setVirtualHost("/itcast");
      connectionFactory.setUsername("heima");
      connectionFactory.setPassword("heima");
    Connection connection = connectionFactory.newConnection();
    Channel channel = connection.createChannel();

    channel.queueDeclare(QUEUE_NAME, true, false, false, null);

    String message = "你好；小兔子！";
    channel.basicPublish("", QUEUE_NAME, null, message.getBytes());
    System.out.println("已发送消息：" + message);

    channel.close();
    connection.close();
```
+ {{c1::理解}}
### 简单/工作模式：消费者简单示例
+ 核心代码示例：
```java
    Connection connection = ConnectionUtil.getConnection();
    Channel channel = connection.createChannel();
    channel.queueDeclare(Producer.QUEUE_NAME, true, false, false, null);

    DefaultConsumer consumer = new DefaultConsumer(channel){
      @Override
      public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties, byte[] body) throws IOException {
        System.out.println("路由key为：" + envelope.getRoutingKey());
        System.out.println("交换机为：" + envelope.getExchange());
        System.out.println("消息id为：" + envelope.getDeliveryTag());
        System.out.println("接收到的消息为：" + new String(body, "utf-8"));
      }
    };

    channel.basicConsume(Producer.QUEUE_NAME, true, consumer);
    channel.close();
    connection.close();
```
+ {{c1::理解}}

### Exchange

+ 作用：{{c1:: 交换机，图中的X。一方面，接收生产者发送的消息。另一方面，知道如何处理消息，例如递交给某个特别队列、递交给所有队列、或是将消息丢弃。到底如何操作，取决于Exchange的类型。}}
+ Exchange有常见以下3种类型： 
  + `Fanout`：{{c1:: 广播，将消息交给所有绑定到交换机的队列 }}
  + `Direct`：{{c1:: 定向，把消息交给符合指定routing key的队列 }}
  + `Topic`：{{c1:: 通配符，把消息交给符合routing pattern（路由模式） 的队列 }}
+ 注意：{{c1:: **Exchange（交换机）只负责转发消息，不具备存储消息的能力**，因此如果没有任何队列与Exchange绑定，或者没有符合路由规则的队列，那么消息会丢失！ }}

### Publish/Subscribe模式：生产者/消费者
+ 核心代码示例：
```java
    channel.exchangeDeclare(FANOUT_EXCHAGE, BuiltinExchangeType.FANOUT);
    channel.queueDeclare(FANOUT_QUEUE_1, true, false, false, null);
    channel.queueDeclare(FANOUT_QUEUE_2, true, false, false, null);
    channel.queueBind(FANOUT_QUEUE_1, FANOUT_EXCHAGE, "");
    channel.queueBind(FANOUT_QUEUE_2, FANOUT_EXCHAGE, "");
    for (int i = 1; i <= 10; i++) {
      String message = "你好；小兔子！发布订阅模式--" + i;
      channel.basicPublish(FANOUT_EXCHAGE, "", null, message.getBytes());
      System.out.println("已发送消息：" + message);
    }
```
+ 核心代码示例：
```java
  //{{c1::
  channel.exchangeDeclare(Producer.FANOUT_EXCHAGE, BuiltinExchangeType.FANOUT);
  channel.queueDeclare(Producer.FANOUT_QUEUE_1, true, false, false, null);
  channel.queueBind(Producer.FANOUT_QUEUE_1, Producer.FANOUT_EXCHAGE, "");
  DefaultConsumer consumer = new DefaultConsumer(channel){
    @Override
    public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties, byte[] body) throws IOException {
      System.out.println("路由key为：" + envelope.getRoutingKey());
      System.out.println("交换机为：" + envelope.getExchange());
      System.out.println("消息id为：" + envelope.getDeliveryTag());
      System.out.println("消费者1-接收到的消息为：" + new String(body, "utf-8"));
    }
  };
  channel.basicConsume(Producer.FANOUT_QUEUE_1, true, consumer);
  //}}
```
+ {{c1::理解}}


### Routing路由模式:生产者/消费者
+ 生产者核心代码示例：
  ```java
      channel.exchangeDeclare(DIRECT_EXCHAGE_NAME, BuiltinExchangeType.DIRECT);
      channel.queueDeclare(DIRECT_QUEUE_INSERT_NAME, true, false, false, null);
      channel.queueDeclare(DIRECT_QUEUE_UPDATE_NAME, true, false, false, null);
      channel.queueBind(DIRECT_QUEUE_INSERT_NAME, DIRECT_EXCHAGE_NAME, "insert");
      channel.queueBind(DIRECT_QUEUE_UPDATE_NAME, DIRECT_EXCHAGE_NAME, "update");

      String message = "新增了商品。路由模式；routing key 为 insert " ;
      channel.basicPublish(DIRECT_EXCHAGE_NAME, "insert", null, message.getBytes());
      System.out.println("已发送消息：" + message);

      message = "修改了商品。路由模式；routing key 为 update" ;
      channel.basicPublish(DIRECT_EXCHAGE_NAME, "update", null, message.getBytes());
      System.out.println("已发送消息：" + message);
  ```
+ 消费者核心代码示例：
  ```java
  channel.exchangeDeclare(Producer.DIRECT_EXCHAGE_NAME, BuiltinExchangeType.DIRECT);
  channel.queueDeclare(Producer.DIRECT_QUEUE_INSERT_NAME, true, false, false, null);
  channel.queueBind(Producer.DIRECT_QUEUE_INSERT_NAME, Producer.DIRECT_EXCHAGE_NAME, "insert");
  DefaultConsumer consumer = new DefaultConsumer(channel){
    @Override
    public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties, byte[] body) throws IOException {
      System.out.println("路由key为：" + envelope.getRoutingKey());
      System.out.println("交换机为：" + envelope.getExchange());
      System.out.println("消息id为：" + envelope.getDeliveryTag());
      System.out.println("消费者1-接收到的消息为：" + new String(body, "utf-8"));
    }
  };
  channel.basicConsume(Producer.DIRECT_QUEUE_INSERT_NAME, true, consumer);
  ```
+ {{c1::理解}}

### Topics通配符模式
+ 通配符规则：
  + `#`：{{c1:: 匹配一个或多个词 }}
  + `*`：{{c1:: 匹配不多不少恰好1个词 }}
  + `item.#`：{{c1:: 能够匹配`item.insert.abc` 或者 `item.insert` }}
  + `item.*`：{{c1:: 只能匹配`item.insert` }}
+ 生产者核心代码示例：
  ```java
    channel.exchangeDeclare(TOPIC_EXCHAGE_NAME, BuiltinExchangeType.TOPIC);
    channel.basicPublish(TOPIC_EXCHAGE_NAME, "item.insert", null, message1.getBytes());
    channel.basicPublish(TOPIC_EXCHAGE_NAME, "item.update", null, message2.getBytes());
    channel.basicPublish(TOPIC_EXCHAGE_NAME, "item.delete", null, message3.getBytes());
  ```
+ 消费者核心代码示例:
  + 消费者1：
  ```java
    channel.exchangeDeclare(Producer.TOPIC_EXCHAGE_NAME, BuiltinExchangeType.TOPIC);
    channel.queueDeclare(Producer.TOPIC_QUEUE_NAME_1, true, false, false, null);
    channel.queueBind(Producer.TOPIC_QUEUE_NAME_1, Producer.TOPIC_EXCHAGE_NAME, "item.update");
    channel.queueBind(Producer.TOPIC_QUEUE_NAME_1, Producer.TOPIC_EXCHAGE_NAME, "item.delete");
  ```
  + 消费者2：
  ```java
    channel.exchangeDeclare(Producer.TOPIC_EXCHAGE_NAME, BuiltinExchangeType.TOPIC);
    channel.queueDeclare(Producer.TOPIC_QUEUE_NAME_2, true, false, false, null);
    channel.queueBind(Producer.TOPIC_QUEUE_NAME_2, Producer.TOPIC_EXCHAGE_NAME, "item.*");
  ```
+ {{c1::理解}}
### RabbitMQ工作模式
**简单模式 HelloWorld** : {{c1:: 一个生产者、一个消费者，不需要设置交换机（使用默认的交换机） }}
**工作队列模式 Work Queue** : {{c1:: 一个生产者、多个消费者（竞争关系），不需要设置交换机（使用默认的交换机） }}
**发布订阅模式 Publish/subscribe** : {{c1:: 需要设置类型为fanout的交换机，并且交换机和队列进行绑定，当发送消息到交换机后，交换机会将消息发送到绑定的队列 }}
**路由模式 Routing** : {{c1:: 需要设置类型为direct的交换机，交换机和队列进行绑定，并且指定routing key，当发送消息到交换机后，交换机会根据routing key将消息发送到对应的队列 }}
**通配符模式 Topic** : {{c1:: 需要设置类型为topic的交换机，交换机和队列进行绑定，并且指定通配符方式的routing key，当发送消息到交换机后，交换机会根据routing key将消息发送到对应的 队列}}

## Spring整合RabbitMQ

### `<rabbit:queue ..></rabbit:queue>`属性：

+ `id`: {{c1:: bean的名称 }}
+ `name`: {{c1:: queue的名称 }}
+ `auto-declare`: {{c1:: 自动创建 }}
+ `auto-delete`: {{c1:: 自动删除。最后一个消费者和该队列断开连接后，自动删除队列 }}
+ `exclusive`: {{c1:: 是否独占连接 }}
+ `durable`: {{c1:: 是否持久化 }}

### spring配置RabbitMQ生产者
+ 核心配置:
  ```xml
  <!-- 定义rabbitmq connectionFactory -->
  <rabbit:connection-factory id="connectionFactory" host="${rabbitmq.host}" port="${rabbitmq.port}" username="${rabbitmq.username}" password="${rabbitmq.password}" virtual-host="${rabbitmq.virtual-host}" />
  <!--定义管理交换机、队列-->
  <rabbit:admin connection-factory="connectionFactory" />
  
  <!-- 简单模式与工作模式 -->
  <rabbit:queue id="spring_queue" name="spring_queue" auto-declare="true" />

  <!-- 广播模式 -->
  <rabbit:queue id="spring_fanout_queue_1" name="spring_fanout_queue_1" auto-declare="true" />
  <rabbit:queue id="spring_fanout_queue_2" name="spring_fanout_queue_2" auto-declare="true" />
  <rabbit:fanout-exchange id="spring_fanout_exchange" name="spring_fanout_exchange" auto-declare="true">
    <rabbit:bindings>
      <rabbit:binding queue="spring_fanout_queue_1" />
      <rabbit:binding queue="spring_fanout_queue_2" />
    </rabbit:bindings>
  </rabbit:fanout-exchange>
  <!-- 通配符模式 -->
  <rabbit:queue id="spring_topic_queue_star" name="spring_topic_queue_star" auto-declare="true" />
  <rabbit:queue id="spring_topic_queue_well" name="spring_topic_queue_well" auto-declare="true" />
  <rabbit:queue id="spring_topic_queue_well2" name="spring_topic_queue_well2" auto-declare="true" />
  <rabbit:topic-exchange id="spring_topic_exchange" name="spring_topic_exchange" auto-declare="true">
    <rabbit:bindings>
      <rabbit:binding pattern="heima.*" queue="spring_topic_queue_star" />
      <rabbit:binding pattern="heima.#" queue="spring_topic_queue_well" />
      <rabbit:binding pattern="itcast.#" queue="spring_topic_queue_well2" />
    </rabbit:bindings>
  </rabbit:topic-exchange>
  <!-- 定义模板 -->
  <rabbit:template id="rabbitTemplate" connection-factory="connectionFactory" />
  ```
+ 各模式消息发送方式：
  ```java
  rabbitTemplate.convertAndSend("spring_queue", "只发队列spring_queue的消息。");
  rabbitTemplate.convertAndSend("spring_fanout_exchange", "", "发送到spring_fanout_exchange交换机的广播消息");
  rabbitTemplate.convertAndSend("spring_topic_exchange", "heima.bj", "发送到spring_topic_exchange交换机heima.bj的消息");
  ```
+ 理解：{{c1:: 标签 }}

### spring配置RabbitMQ消费者
+ 核心配置：
  ```xml
    <bean id="springQueueListener" class="top.xieyun.rabbitmq.listener.SpringQueueListener"/>
    <rabbit:listener-container connection-factory="connectionFactory" auto-declare="true">
      <rabbit:listener ref="springQueueListener" queue-names="spring_queue"/>
    </rabbit:listener-container>
  ```
+ 监听器实现:
  ```java
  public class SpringQueueListener implements MessageListener {
    @Override
    public void onMessage(Message message) {
      //打印消息
      System.out.println(new String(message.getBody()));
    }
  }
  ```
+ 理解：{{c1:: 标签 }}

## SpringBoot整合RabbitMQ
+ 引入starter：{{c1:: `spring-boot-starter-amqp` }}
+ 配置yml：
  ```yml
  spring:
    rabbitmq:
      host: 172.16.98.133 # ip
      port: 5672
      username: guest
      password: guest
      virtual-host: /
  ```
+ 配置类：定义**交换机**，**队列**以及**绑定关系**
  ```java
  @Configuration
  public class RabbitMQConfig {
      public static final String EXCHANGE_NAME = "boot_topic_exchange";
      public static final String QUEUE_NAME = "boot_queue";
      @Bean("bootExchange")
      public Exchange bootExchange(){
          return ExchangeBuilder.topicExchange(EXCHANGE_NAME).durable(true).build();
      }
      @Bean("bootQueue")
      public Queue bootQueue(){
          return QueueBuilder.durable(QUEUE_NAME).build();
      }
      @Bean
      public Binding bindQueueExchange(@Qualifier("bootQueue") Queue queue, @Qualifier("bootExchange") Exchange exchange){
          return BindingBuilder.bind(queue).to(exchange).with("boot.#").noargs();
      }
  }
  ```
+ 生产者：注入`RabbitTempalte`，调用`convertAndSend(..)`发送消息
+ 消费者：
  ```java
  @Component
  public class RabbimtMQListener {
      @RabbitListener(queues = "boot_queue")
      public void ListenerQueue(Message message){
          System.out.println(new String(message.getBody()));
      }
  }
  ```
+ 理解：{{c1:: 标签 }}


## 消息可靠性概况

1. 持久化
  + {{c1:: exchange要持久化 }}
  + {{c1:: queue要持久化 }}
  + {{c1:: message要持久化 }}
2. Confirm：{{c1:: 生产方确认Confirm }}
3. Ack：{{c1:: 消费方确认Ack }}
4. 高可用：{{c1:: Broker高可用 }}

### 消息的可靠投递

+ 作用：{{c1:: 在使用 RabbitMQ 的时候，作为消息发送方希望杜绝任何消息丢失或者投递失败场景。}}
+ 两种投递可靠性模式
  + {{c1:: `confirm` 确认模式 }}
  + {{c1:: `return` 退回模式 }}
+ 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201121144245.png) }}

###  消息的可靠投递：`confirm` 确认模式的使用
1. 确认模式开启：{{c1:: `ConnectionFactory`中开启`publisher-confirms="true"` }}
2. 在`rabbitTemplate`定义`ConfirmCallBack`回调函数
   ```java
        rabbitTemplate.setConfirmCallback(new RabbitTemplate.ConfirmCallback() {
            /**
             *
             * @param correlationData {{c1:: 相关配置信息 }}
             * @param ack   {{c1:: exchange交换机 是否成功收到了消息。true 成功，false代表失败 }}
             * @param cause {{c1:: 失败原因 }}
             */
            @Override
            public void confirm(CorrelationData correlationData, boolean ack, String cause) {
                System.out.println("confirm方法被执行了....");

                if (ack) {
                    //接收成功
                    System.out.println("接收成功消息" + cause);
                } else {
                    //接收失败
                    System.out.println("接收失败消息" + cause);
                    //做一些处理，让消息再次发送。
                }
            }
        });
        //发送消息
        rabbitTemplate.convertAndSend("test_exchange_confirm111", "confirm", "message confirm....");
   ```
+ 理解：{{c1:: 标签 }}

###  消息的可靠投递：`return` 退回模式的使用
+ 回退模式： 当消息发送给Exchange后，Exchange路由到Queue失败是 才会执行 ReturnCallBack
+ 默认处理：如果消息没有路由到Queue，则丢弃消息
1. 退回模式开启：{{c1:: `ConnectionFactory`中开启`publisher-returns="true"` }}
2. 设置return回调函数
   ```java
        //设置交换机处理失败消息的模式
        rabbitTemplate.setMandatory(true);
        //设置ReturnCallBack
        rabbitTemplate.setReturnCallback(new RabbitTemplate.ReturnCallback() {
            /**
             *
             * @param message   {{c1:: 消息对象 }}
             * @param replyCode {{c1:: 错误码 }}
             * @param replyText {{c1:: 错误信息 }}
             * @param exchange  {{c1:: 交换机 }}
             * @param routingKey {{c1:: 路由键 }}
             */
            @Override
            public void returnedMessage(Message message, int replyCode, String replyText, String exchange, String routingKey) {
                //处理
            }
        });
        rabbitTemplate.convertAndSend("test_exchange_confirm", "confirm", "message confirm....");
    ```
+ 理解：{{c1:: 标签 }}


### Consumer Ack
+ 作用:ack指Acknowledge,确认收到。表示清费诺收到消息后的确认方式 。
+ 三种确认方式：
  + 自动确认：{{c1:: `acknowledge=none` }}
    表示：一旦消息被Consumer接收到，则自动确认收到
  + 手动确认：{{c1:: `acknowledge=manual` }}
    表示：{{c1:: 手动调用`channel.basisAck()`确认收到 }}
  + 根据异常情况确认 ：{{c1:: `acknowledge=auto` }}


### Consumer ACK:手动确认
 1. 设置手动签收：`acknowledge="manual"`
  ```xml
   <rabbit:listener-container connection-factory="connectionFactory" acknowledge="manual" prefetch="1" >
      <rabbit:listener ref="ackListener" queue-names="test_queue_confirm"></rabbit:listener>
   </rabbit:listener-container>
  ```
 2. 让监听器类实现`ChannelAwareMessageListener`接口
    1. 如果消息成功处理，则调用 {{c1:: `channel.basicAck()` 签收 }}
    2. 如果消息处理失败，则调用 {{c1:: `channel.basicNack()`拒绝签收，broker重新发送给`consumer` }}
   ```java
    @Component
    public class AckListener implements ChannelAwareMessageListener {
        @Override
        public void onMessage(Message message, Channel channel) throws Exception {
            long deliveryTag = message.getMessageProperties().getDeliveryTag();
            try {
                //1.接收转换消息
                System.out.println(new String(message.getBody()));
                System.out.println("处理业务逻辑...");
                int i = 3/0;//出现错误
                //3. 手动签收
                channel.basicAck(deliveryTag,true);
            } catch (Exception e) {
                //4.拒绝签收
                // 第三个参数：是否重回队列。如果设置为true，则消息重新回到queue，broker会重新发送该消息给消费端
                channel.basicNack(deliveryTag,true,true);
                //channel.basicReject(deliveryTag,true);
            }
        }
    }
   ```

### 消费端限流机制
+ 作用：{{c1:: 确保消费端最大只能同时处理有限个消息 }}
+ 开启配置：
 1. {{c1:: 确保ack机制为手动确认。{{c1::  }}
 2. {{c1:: 配置prefetch属性：perfetch = 1,表示消费端每次从mq拉去一条消息来消费，直到手动确认消费完毕后，才会继续拉去下一条消息。 }}
  ```xml
  <!-- {{c1:: -->
   <rabbit:listener-container connection-factory="connectionFactory" acknowledge="manual" prefetch="1" >
      <rabbit:listener ref="ackListener" queue-names="test_queue_confirm"></rabbit:listener>
   </rabbit:listener-container>
   <!-- }} -->
  ```

### TTL配置
+ 作用：{{c1:: 全称Time To Live，当消息到达指定时间后，还没有被消费，会被自动清除掉。 }}
+ 队列统一过期配置:{{c1::设置队列过期时间使用参数：`x-message-ttl`。单位：ms }}
  ```xml
    <!-- {{c1:: -->
    <rabbit:queue name="test_queue_ttl" id="test_queue_ttl">
        <rabbit:queue-arguments>
            <entry key="x-message-ttl" value="100000" value-type="java.lang.Integer"></entry>
        </rabbit:queue-arguments>
    </rabbit:queue>
    <!-- }} -->
  ```
+ 消息单独过期配置:{{c1::设置消息过期时间使用参数： `expiration`。单位：ms }}
  ```java
      //{{c1::
      MessagePostProcessor messagePostProcessor = new MessagePostProcessor() {
            @Override
            public Message postProcessMessage(Message message) throws AmqpException {
                message.getMessageProperties().setExpiration("5000");//消息的过期时间
                return message;
            }
        };
      rabbitTemplate.convertAndSend("test_exchange_ttl", "ttl.hehe", "message ttl....",messagePostProcessor);
      //}}
  ```
+ 注意：
  + 时间短：{{c1:: 如果设置了消息的过期时间，也设置了队列的过期时间，它以时间短的为准。 }}
  + 全部移除：{{c1:: 队列过期后，会将队列所有消息全部移除。 }}
  + 队列顶端：{{c1:: 消息过期后，只有消息在队列顶端，才会判断其是否过期(移除掉) }}

### 死信队列
+ 是什么:{{c1:: 死信队列，英文缩写：`DLX` 。`Dead Letter Exchange`（死信交换机），当消息成为`Dead message`后，可以被重新发送到另一个交换机，这个交换机就是`DLX。}}
+ 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201121171736.png) }}
+ 消息成为死信的三种情况：
  1. {{c1:: 队列消息长度到达限制；对应参数:`x-max-length`
 }}
  2. {{c1:: 消费者拒接消费消息，`basicNack/basicReject`,并且不把消息重新放入原目标队列,`requeue=false`； }}
  3. {{c1:: 原队列存在消息过期设置，消息到达超时时间未被消费；对应参数:`x-message-ttl` }}
+ 注意：{{c1:: 死信交换机与普通交换机没有任何区别 }}


### 队列绑定死信交换机
+ 给队列设置参数：{{c1:: `x-dead-letter-exchange` 和 `x-dead-letter-routing-key` }}
+ 配置：
  ```xml
    <!-- {{c1:: -->
    <rabbit:queue name="test_queue_dlx" id="test_queue_dlx">
        <rabbit:queue-arguments>
            <entry key="x-dead-letter-exchange" value="exchange_dlx" />
            <entry key="x-dead-letter-routing-key" value="dlx.xxx" />
            <entry key="x-message-ttl" value="10000" value-type="java.lang.Integer" />
            <entry key="x-max-length" value="10" value-type="java.lang.Integer" />
        </rabbit:queue-arguments>
    </rabbit:queue>
    <rabbit:topic-exchange name="test_exchange_dlx">
        <rabbit:bindings>
            <rabbit:binding pattern="test.dlx.#" queue="test_queue_dlx"></rabbit:binding>
        </rabbit:bindings>
    </rabbit:topic-exchange>
    <!-- }} -->
  ```

### 延迟队列概念
+ 概念：{{c1:: 延迟队列，即消息进入队列后不会立即被消费，只有到达指定时间后，才会被消费。 }}
+ 考虑需求：
  1. 下单后，30分钟未支付，取消订单，回滚库存。
  2. 新用户注册成功7天后，发送短信问候。
+ 解释：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201121174434.png) }}

### RabbitMQ实现延时队列
+ 主要思路：{{c1:: TTL+死信队列 组合实现延迟队列的效果。 }}
+ 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201121174711.png) }}
+ 实现步骤：
  1. {{c1:: 定义正常交换机（order_exchange）和队列(order_queue) }}
  2. {{c1:: 定义死信交换机（order_exchange_dlx）和队列(order_queue_dlx) }}
  3. {{c1:: 绑定，设置正常队列过期时间为30分钟 }}
+ 具体实现：
  ```xml
  <!-- {{c1:: -->
      <rabbit:queue id="order_queue" name="order_queue">
        <rabbit:queue-arguments>
            <entry key="x-dead-letter-exchange" value="order_exchange_dlx" />
            <entry key="x-dead-letter-routing-key" value="dlx.order.cancel" />
            <entry key="x-message-ttl" value="10000" value-type="java.lang.Integer" />
        </rabbit:queue-arguments>
    </rabbit:queue>
    <rabbit:topic-exchange name="order_exchange">
        <rabbit:bindings>
            <rabbit:binding pattern="order.#" queue="order_queue"></rabbit:binding>
        </rabbit:bindings>
    </rabbit:topic-exchange>

    <rabbit:queue id="order_queue_dlx" name="order_queue_dlx"><rabbit:queue>
    <rabbit:topic-exchange name="order_exchange_dlx">
        <rabbit:bindings>
            <rabbit:binding pattern="dlx.order.#" queue="order_queue_dlx"></rabbit:binding>
        </rabbit:bindings>
    </rabbit:topic-exchange>
  <!-- }} -->
  ```

### rabbitmqctl管理和监控命令

+ RabbitMQ默认日志存放路径：{{c1:: /var/log/rabbitmq/rabbit@xxx.log }}
+ `rabbitmqctl list_queues`:{{c1:: 查看队列 }}
+ `rabbitmqctl list_exchanges`:{{c1:: 查看exchanges }}
+ `rabbitmqctl list_users`:{{c1:: 查看用户 }}
+ `rabbitmqctl list_connections`:{{c1:: 查看连接 }}
+ `rabbitmqctl list_consumers`:{{c1:: 查看消费者信息 }}
+ `rabbitmqctl environment`:{{c1:: 查看环境变量 }}
+ `rabbitmqctl list_queues name messages_unacknowledged`:{{c1:: 查看未被确的队列 }}
+ `rabbitmqctl list_queues name memory`:{{c1:: 查看单个队列的内存使用 }}
+ `rabbitmqctl list_queues name messages_ready`:{{c1:: 查看准备就绪的队列 }}

### 消息追踪
+ 打开 trace 会影响消息写入功能，适当打开后请关闭。/
+ `rabbitmqctl trace_on`：{{c1:: 开启Firehose命令 }}
+ `rabbitmqctl trace_off`：{{c1:: 关闭Firehose命令 }}
+ 启用插件：`rabbitmq-plugins enable rabbitmq_tracing`

### 消息可靠性/与幂等性保障--消息补偿/乐观锁
+ 图示:![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201122190625.png)

## RabbitMQ集群搭建

+ 首先确保RabbitMQ运行没有问题:`rabbitmqctl status`
+ 停止rabbitmq服务:`service rabbitmq-server stop`
+ 启动第一个节点:`RABBITMQ_NODE_PORT=5673 RABBITMQ_NODENAME=rabbit1 rabbitmq-server start`
+ 启动第一个节点:`RABBITMQ_NODE_PORT=5674 RABBITMQ_SERVER_START_ARGS="-rabbitmq_management listener [{port,15674}]" RABBITMQ_NODENAME=rabbit2 rabbitmq-server start`
+ 结束命令：
  + `rabbitmqctl -n rabbit1 stop`
  + `rabbitmqctl -n rabbit2 stop`

### 开启镜像代理
+ 确认RabbitMQ运行与启动：`rabbitmqctl status`
+ 停掉服务： `service rabbitmq-server stop`
+ 启动第一节点：`RABBITMQ_NODE_PORT=5673 RABBITMQ_NODENAME=rabbit1 rabbitmq-server start`
  + 注意：这是前台启动方式
+ `RABBITMQ_NODE_PORT=5674 RABBITMQ_SERVER_START_ARGS="-rabbitmq_management listener [{port,15674}]" RABBITMQ_NODENAME=rabbit2 rabbitmq-server start`
  + 注意:与前一条命令的区别，管理控制台端口，与服务端口的不同
+ 分别访问已开启2个端口的控制台。
+ rabbit1操作作为主节点：
  + `rabbitmqctl -n rabbit1 stop_app  `
  + `rabbitmqctl -n rabbit1 reset`
  + `rabbitmqctl -n rabbit1 start_app`
+ rabbit2操作为从节点：
  + `rabbitmqctl -n rabbit2 stop_app`
  + `rabbitmqctl -n rabbit2 reset`
  + `rabbitmqctl -n rabbit2 join_cluster rabbit1@'super' `
    + 注意：super是**主机名**需要换成自己的
  + `rabbitmqctl -n rabbdddit2 start_app`
+ 此时存在问题：数据是无法同步的。
+ 开启主节点网页的管理端`Admin->Policies`配置如下
  + ![1566072300852](https://gitee.com/xieyun714/nodeimage/raw/master/img/1566072300852.png)
  + 等价的命令配置：`rabbitmqctl set_policy my_ha "^" '{"ha-mode":"all"}'`
+ 理解：{{c1:: 标签 }}

### 负载均衡-HAProxy插件配置
+ 作用：{{c1:: 提供统一的端口访问各个RabbitMQ节点 }}
+ 下载依赖包:`yum install gcc vim wget`
+ 上传haproxy源码包
+ 解压：`tar -zxvf haproxy-1.6.5.tar.gz -C /usr/local`
+ 进入目录、进行编译、安装：
  + `cd /usr/local/haproxy-1.6.5`
  + `make TARGET=linux31 PREFIX=/usr/local/haproxy`
  + `make install PREFIX=/usr/local/haproxy`
+ 赋权
  + `groupadd -r -g 149 haproxy`
  + `useradd -g haproxy -r -s /sbin/nologin -u 149 haproxy`
+ 创建haproxy配置文件
  + `mkdir /etc/haproxy`
  + `vim /etc/haproxy/haproxy.cfg`
+ 配置HAProxy：
  + 主要思路:
    1. 修改rabbitmq_cluster下，绑定**对外端口号**
    2. 修改balance roundrobin下，配置**节点通信**
    3. 修改listen stats下，配置HA管理控制台端口：
  + 配置如下：
  ```yaml
  #logging options
  global
    log 127.0.0.1 local0 info
    maxconn 5120
    chroot /usr/local/haproxy
    uid 99
    gid 99
    daemon
    quiet
    nbproc 20
    pidfile /var/run/haproxy.pid

  defaults
    log global
    
    mode tcp

    option tcplog
    option dontlognull
    retries 3
    option redispatch
    maxconn 2000
    contimeout 5s
    
      clitimeout 60s

      srvtimeout 15s  
  #front-end IP for consumers and producters

  listen rabbitmq_cluster
    bind 0.0.0.0:5672
    
    mode tcp
    #balance url_param userid
    #balance url_param session_id check_post 64
    #balance hdr(User-Agent)
    #balance hdr(host)
    #balance hdr(Host) use_domain_only
    #balance rdp-cookie
    #balance leastconn
    #balance source //ip
    
    balance roundrobin
    
          server node1 127.0.0.1:5673 check inter 5000 rise 2 fall 2
          server node2 127.0.0.1:5674 check inter 5000 rise 2 fall 2

  listen stats
    bind 172.16.98.133:8100
    mode http
    option httplog
    stats enable
    stats uri /rabbitmq-stats
    stats refresh 5s
  ```
+ 指定配置文件路径启动HAproxy负载：`/usr/local/haproxy/sbin/haproxy -f /etc/haproxy/haproxy.cfg`\
+ 查看haproxy进程状态:`ps -ef | grep haproxy`
+ 访问如下地址对mq节点进行监控:`http://172.16.98.133:8100/rabbitmq-stats`
+ 理解：{{c1:: 标签 }} 