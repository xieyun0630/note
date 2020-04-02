### windows上安装Maven [	](maven_20200331123149423)

- {{c1::环境变量`M2_HOME`：Maven安装目录}}
- {{c1::环境变量`Path`:添加`"%M2_HOME%\bin"`}}
- {{c1::管理员运行命令行检查安装情况：`mvn -v`}}
### .m2文件夹的作用 [	](maven_20200331123149426)
- 位置：{{c1::~/.m2}}
- .m2/repository ：{{c1::本地仓库}}
- .m2/settings.xml：{{c1::本地Maven配置文件}}
### 配置HTTP代理的作用(实践搜索) [	](maven_20200331123149427)

- 背景：{{c1::公司不允许直接访问外部网络，需要经过代理验证（比如在安全限制上设置了白名单网站），这时，maven需要通过配置http代理访问中央仓库（repo1.maven.org）}}
- 搜索：{{c1:: MAVEN配置HTTP代理 }}

### MAVEN_OPTS环境变量的作用 [	](maven_20200331123149428)
+ 通常需要设置MAVEN_OPTS的值为:{{c1::`-Xms128m  -Xmx512m`}}
+ 含义：{{c1:: 因为Java默认的最大可用内存往往不够满足Maven运行需要，比如较大的项目时，使用Maven生成项目站点需要占用大量内存。如果没有该配置，则很容易得到java.lang.OutOfMeneoryError。因此，一开始就配置该变量是推荐的做法。}}

### pom.xml文件中概要 [	](maven_20200331123149430)

|  元素  | 意义  |
|  ----  | ----  |
|`<modelVersion>`元素 | {{c1::当前POM模型的版本}}|
|`<groupId>`元素 | {{c1::定义项目属于哪个组，通常与公司域名关联，建立一个myapp组为|`com.google.myapp.`}}|
|`<artifactId>`元素 | {{c1:: 当前项目在组中的唯一ID }}|
|`<version>`元素 | {{c1:: 定义项目版本,1.0.SHNAPSHOT,其中SHNAPSHOT代表快照版本 }}|
|`<name>`元素|{{c1::可选的，声明一个对用户友好的项目名称。}}|
|`<packaging>`元素|{{c1::可选的，打包方式默认为jar。}}|

### maven项目主要骨架 [	](maven_20200331123149431)

+ {{c1:: ./src/main/java }}
+ {{c1:: ./src/main/resources }}
+ {{c1:: ./src/test/java }}
+ {{c1:: ./src/test/resources }}
+ {{c1:: ./pom.xml }}

### maven的默认编译使用的jdk版本是1.3,如何解决？（实践搜索） [	](maven_20200331123149432)
+ {{c1:: maven会用maven-compiler-plugin默认的jdk版本来进行处理，以至于可能导致编译不通过的问题，需要显示在pom文件中配置插件。}}
+ {{c1::搜索：maven-compiler-plugin}}

### maven配置生成可执行的jar（搜索） [	](maven_20200331123149434)
含义：{{c1::maven默认打包生成jar是不能直接运行的，因为带有main方法的类信息不会添加到MANIFEST.MF文件,需要配置.}}
搜索:{{c1::`maven-shade-plugin`}}

### 使用archetype生成项目骨架 [	](maven_20200331123149437)
{{c1::
简单运行命令行：mvn archetype:generate
}}
### maven官方插件坐标的格式 [	](maven_20200331123149438)
{{c1::
```xml
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
```
}}

### 项目构件的文件名生成规则 [	](maven_20200331123149440)
一般规则为：{{c1:: `artifactId-version [-classifer] .packaging` }}

### 依赖范围与classpath之间的关系 [	](maven_20200331123149441)

- 3种classpath：{{c1::编译classpath，测试classpath，运行时classpath。}}
- 5种依赖范围：
  1. compile: {{c1::都有效，例子：spring-core}}
  2. test: {{c1::只对测试有效 例子：JUnit}}
  3. provided: {{c1::只对运行时无效，例子：servlet-api}}
  4. runtime: {{c1::只对编译无效，例子：JDBC驱动实现。}}
  5. System:{{c1::与provided一致，代表本地的，仓库之外的，需要配置systemPath元素。}}

### 依赖范围对传递性依赖的影响 [	](maven_20200331123149442)

![image-20200330173655295](maven.assets/image-20200330173655295.png)
{{c1:: ![image-20200330173546138](maven.assets/image-20200330173546138.png) }}

### 依赖冲突原则 [	](maven_20200331123149443)

有依赖关系如下：
1. A->B->C->X（1.0）、A->D->X（2.0）
2. A->B->X（1.0）、A->C->X（2.0）

分别对应什么依赖调解原则？
- {{c1:: 最短路径优先：X(2.0) }}
- {{c1:: 第一声明优先：X(1.0) }}

### `<dependency>`子元素`<optional>`的作用： [	](maven_20200331123149444)

{{c1:: 可选的，当optional为true时，<dependency>引用的依赖不会被传递给当前项目的引用者，通常需要引用者自己提供一个代替依赖。}}

### `<exclusion>`元素的使用场景以及使用例子 [	](maven_20200331123149445)

{{c1::

![image-20200330175609321](maven.assets/image-20200330175609321.png)

}}

+ {{c1:: 通常用于修改某个间接依赖版本。}}


{{c1:: 
```xml
    <exclusions>  
        <exclusion>  
            <groupId>org.springframework</groupId>  
            <artifactId>spring-beans</artifactId>  
        </exclusion> 
    <exclusions>
```
}}



### pom.xml中`<properties>`元素的使用 [	](maven_20200331123149447)

{{c1::
```xml
<properties>
 <spring.version>1.2.6</spring.version>
</properties>
```
```xml
<dependency>
 <groupId>org.springframework</groupId>
 <artifactId>spring-core</artifactId>
 <version>${spring.version}</version>
</dependency>
<dependency>
 <groupId>org.springframework</groupId>
 <artifactId>spring-aop</artifactId>
 <version>${spring.version}</version>
</dependency>
```
}}

### mvn dependency插件
+ 查看当前项目已解析依赖：{{c1:: mvn dependency:list }}
+ 查看当前项目的依赖树：{{c1:: mvn dependency:tree }}
+ 查看当前项目分析当前项目依赖：{{c1:: mvn dependency:analyze }}



## Maven仓库

### 仓库路径与坐标的对应关系为：

{{c1:: groupId/artifactId/version/artifactId-version.packagine }}

### 自定义本地仓库目录地址
{{c1::
将以下配置加入settings.xml文件
```xml
<settings>
<localRepository>D:\java\myRepository</localRepository>
</settings>
```
}}

### 将本地项目的构建安装到Maven仓库中
{{c1:: 命令：{{c1:: mvn clean install }}

### Maven仓库的分类
+ {{c1:: 本地仓库 }}
+ {{c1:: 远程仓库 }}
    + {{c1:: 中央仓库 }}
    + {{c1:: 私服 }}
    + {{c1:: 其他公共库 }}

### 远程仓库认证的配置
{{c1::
在settings.xml文件中配置
```xml 
<servers>
<server>
<!-- id必须与POM中需要认证的repository元素ID一致 -->
<id>prok-releases</id>
<username>repo-user</username>
<password>repo-pwd</password>
</server>
</servers>
```
}}

### 部署远程仓库的配置
```xml
<distributionManagement>
    <repository>
        <!-- 唯一标识符 -->
        <id>prok-releases</id>
        <!-- 仓库名称 -->
        <name>Proj Release Repository</name>
        <!-- 仓库地址 -->
        <url>http://192.168.1.100/content/repository/proj-releases</url>
    </repository>
    <snapshotRepository>
        <id>proj-snapshots</id>
        <name>Proj Snapshot Repository</name>
        <url>http://192.168.1.100/content/repository/proj-snapshots</url>
    </snapshotRepository>
</distributionManagement>
```
+ 以上配置到POM中后，配置正确的认证信息到settings.xml中
+ 运行`mvn clean deploy`命令部署。

### 远程仓库的配置

```xml
<repositories>
        <repository>
            <id>maven-ali</id>
            <url>https://maven.aliyun.com/repository/public</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
                <!-- daily,always -->
                <updatePolicy>always</updatePolicy>
                <!-- ignore,warn,fail -->
                <checksumPolicy>fail</checksumPolicy>
            </snapshots>
        </repository>
</repositories>
```
+ `<updatePolicy>`: {{c1:: 配置Maven检查更新的频率。}}
+ `<checksumPolicy>`: {{c1:: 配置Maven检查检验和文件的策略。}}

### 配置中央仓库镜像

{{c1::

```xml
<mirror>
<id>alimaven</id>
<name>aliyun maven</name>
<url>http://maven.aliyun.com/nexus/content/groups/public/</url>
<mirrorOf>central</mirrorOf>
</mirror>
```
}}

- id：唯一标识一个镜像
- name：镜像名称
- url：镜像地址
- mirrorOf：代表一个镜像的替代位置，例如central就表示代替官方的中央仓库
- mirrorOf用法如下：

{{c1::![image-20200401164331881](maven.assets/image-20200401164331881.png)}}

### Maven的快照版本机制
{{c1::
+ 将当前项目坐标中`<version>`改为类似2.1-SNAPSHOT的值
+ 然后发布到私服中，发布过程中，maven自动为构件打上时间戳。
+ 类似：2.1-20091214.221414-13.jar
}}
+ 强制更新命令：{{c1:: `mvn clean install-U`}}

### Maven生命周期

### clean生命周期阶段与插件目标的绑定关系

![image-20200401180528655](maven.assets/image-20200401180528655.png)

{{c1::![image-20200401164755027](maven.assets/image-20200401164755027.png)}}

### site生命周期阶段与插件目标的绑定关系

![image-20200401180710199](maven.assets/image-20200401180710199.png)

{{c1:: ![image-20200401180626652](maven.assets/image-20200401180626652.png) }}

 }}

### default生命周期与内置插件绑定关系及具体任务(打包类型: jar)

| 生命周期阶段           |               插件目标                | 执行任务                               |
| ---------------------- | :-----------------------------------: | -------------------------------------- |
| process-resources      |   maven-resources-plugin:resources    | {{c1::复制主资源文件至主输出目录}}     |
| compile                |     maven-compile-plugin:compile      | {{c1::编译主代码至主输出目录}}         |
| process-test-resources | maven-resources-plugin:testRresources | {{c1::复制测试资源文件至测试输出目录}} |
| test-compile           |   maven-compiler-plugin:testCompile   | {{c1::编译测试代码至测试输出目录}}     |
| test                   |      maven-surefire-plugin:test       | {{c1::执行测试用例}}                   |
| package                |         maven-jar-plugin:jar          | {{c1::创建项目jar包}}                  |
| install                |     maven-install-plugin:install      | {{c1::将项目输出构件安装到本地仓库}}   |
| deploy                 |      maven-deploy-plugin:deploy       | {{c1::将项目输出构件部署到远程仓库}}   |