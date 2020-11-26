## Ant基础 [	](maven_20200626090144117)

### windows上安装ant [	](maven_20200626090144118)

- {{c1::环境变量`ANT_HOME`：ant的安装目录}}
- {{c1::环境变量`Path`:添加`"%ANT_HOME%\bin"`}}
- {{c1::管理员运行命令行或者powerShell检查安装情况：`ant`}}

### ant命令 [	](maven_20200626090144119)

+ `ant`:{{c1:: 在当前目录下搜索build.xml文件，并执行默认配置}}
+ `ant -find`：{{c1:: 到上级目录搜索build.xml文件，直到文件系统的根路径。}}
+ `ant -f/-file a.xml`:{{c1:: 显示指定a.xml做为生成文件}}
+ `ant -quiet\-q`:{{c1:: 运行ant时只输出必要的信息}}
+ `ant -verbose -l a.log`:{{c1:: 运行ant时输出更多的信息到a.log文件}}
+ `ant -Denv1=%ANT_HOME%`:{{c1:: 设置env1参数的值为环境变量}}
+ `ant -Denv1=$ANT_HOME`:{{c1:: linux上设置env1参数的值为环境变量}}

### `<project>`元素的 [	](maven_20200626090144120)
+ 常用属性:
    + `default`:{{c1::  指定默认target }}
    + `basedir`:{{c1::  指定项目的基准目录 }}
    + `name`:{{c1::  项目名 }}
    + `description`:{{c1:: 项目描述 }}
+ 两个重要元素：
    + `<property .../>`:{{c1:: 用于定义一个或多个属性 }}
    + `<path .../>`:{{c1:: 用于定义一个或多个文件和路径 }}

### `<target>`元素的常用属性： [	](maven_20200626090144121)

- `name`:{{c1:: 必要属性，指定target名 }}
- `depends`:{{c1:: 指定所依赖的一个或多个target名 }}
- `if`:{{c1:: 指定一个属性名，仅当存在该属性才执行该target }}
- `unless`:{{c1:: 指定一个属性名，仅当不存在该属性才执行该target }}
- `description`: {{c1:: 描述信息 }}

### `<path .../>`和`<classpath .../>`的子元素组合使用 [	](maven_20200626090144122)
```xml
<path id="classpath">
<!-- 定义classpath属性值所代表的路径 -->
<!-- {{c1:: -->
<pathelement path="${classpath}" />
<!-- }} -->
<!-- 定义lib路径下所有*.jar文件 -->
<!-- {{c1:: -->
<fileset dir="lib">
    <include name="**/*.jar" />
</fileset>
<!-- }} -->
<!-- 定义build/apps路径下的所有classes路径 -->
<!-- {{c1:: -->
<dirset dir="build">
    <include name="apps/**/classes">
    <exclude name="apps/**/*Test*">
</dirset>
<!-- }} -->
<!-- 定义res路径下的a.properties文件和b.xml文件 -->
<!-- {{c1:: -->
<filelist dir="res" files="a.properties,b.xml" />
<!-- }} -->

        <!-- 指定编译Java文件所需要第三方类库所在的位置 -->
        <!-- 这里是其他地方引用上面path的内容 -->
        <!-- {{c1:: -->
        <classpath refid="classpath"/>
        <!-- }} -->
</path>
```
## Maven基础概念 [	](maven_20200512080327602)

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

| 元素                 | 意义                                                            |
| -------------------- | --------------------------------------------------------------- |
| `<modelVersion>`元素 | {{c1::当前POM模型的版本}}                                       |
| `<groupId>`元素      | {{c1::定义项目属于哪个组，通常与公司域名关联，建立一个myapp组为 `com.google.myapp.`}} |
| `<artifactId>`元素   | {{c1:: 当前项目在组中的唯一ID,通常与模块文件夹名称一致 }}       |
| `<version>`元素      | {{c1:: 定义项目版本,1.0.SHNAPSHOT,其中SHNAPSHOT代表快照版本 }}  |
| `<name>`元素         | {{c1::可选的，声明一个对用户友好的项目名称。}}                  |
| `<packaging>`元素    | {{c1::可选的，打包方式默认为jar。}}                             |

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

![image-20200330173655295](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200330173655295.png)
{{c1:: ![image-20200330173546138](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200330173546138.png) }}

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

![image-20200330175609321](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200330175609321.png)

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

### mvn dependency插件 [	](maven_20200410012359789)
+ 查看当前项目已解析依赖：{{c1:: mvn dependency:list }}
+ 查看当前项目的依赖树：{{c1:: mvn dependency:tree }}
+ 查看当前项目分析当前项目依赖：{{c1:: mvn dependency:analyze }}



## Maven仓库 [	](maven_20200410012359790)

### 仓库路径与坐标的对应关系为： [	](maven_20200410012359792)

{{c1:: groupId/artifactId/version/artifactId-version.packagine }}

### 自定义本地仓库目录地址 [	](maven_20200410012359793)
{{c1::
将以下配置加入settings.xml文件

```xml
<settings>
<localRepository>D:\java\myRepository</localRepository>
</settings>
```
}}

### 将本地项目的构建安装到Maven仓库中 [	](maven_20200410012359794)
命令：{{c1:: `mvn clean install` }}

### Maven仓库的分类 [	](maven_20200410012359796)
+ {{c1:: 本地仓库 }}
+ {{c1:: 远程仓库 }}
    + {{c1:: 中央仓库 }}
    + {{c1:: 私服 }}
    + {{c1:: 其他公共库 }}

## maven私服  [	](maven_20201115082829579)

### 将项目发布到maven私服 [	](maven_20200410012359797)

+ 背景：{{c1:: maven私服是搭建在公司局域网内的maven仓库，公司内的所有开发团队都可以使用。例如技术研发 团队开发了一个基础组件，就可以将这个基础组件打成jar包发布到私服，其他团队成员就可以从私服下载这个jar包到本地仓库并在项目中使用。 }}
+ 具体步骤如下：
  1. 配置maven的settings.xml文件添加认证信息
   ```xml 
    <servers>
        <server>
            <id>prok-releases</id>
            <username>repo-user</username>
            <password>repo-pwd</password>
        </server>
    </servers>
   ```
    + 注意：{{c1:: id必须与POM中需要认证的repository元素ID一致  }}
  2. 配置项目的pom.xml文件
  ```xml
    <!-- {{c1:: -->
    <distributionManagement>
        <repository>
            <id>prok-releases</id>
            <name>Proj Release Repository</name>
            <url>http://192.168.1.100/content/repository/proj-releases</url>
        </repository>
        <snapshotRepository>
            <id>proj-snapshots</id>
            <name>Proj Snapshot Repository</name>
            <url>http://192.168.1.100/content/repository/proj-snapshots</url>
        </snapshotRepository>
    </distributionManagement>
    <!-- }} -->
  ```
    + `<repository>`:{{c1:: 正式版本库 }}
    + `<snapshotRepository>`:{{c1:: 快照版本库 }}
    + `<id>`:{{c1:: 唯一标识符 }}
    + `<name>`:{{c1:: 仓库名称 }}
    + `<url>`:{{c1:: 仓库地址 }}
  3. 执行命令:{{c1:: `mvn deploy` }}

### 从私服下载jar到本地仓库 [	](maven_20201115082829582)

+ 在setting.xml文件中配置下载模板：
    ```xml
    <profile>
        <id>dev</id>
        <repositories>
            <repository>
                <id>nexus</id>
                <url>http://localhost:8081/nexus/content/groups/public/</url>
                <releases>
                    <enabled>true</enabled>
                </releases>
                <snapshots>
                    <enabled>true</enabled>
                    <updatePolicy>always</updatePolicy>
                    <checksumPolicy>fail</checksumPolicy>
                </snapshots>
            </repository>
        </repositories>
        <pluginRepositories>
            <pluginRepository>
                <id>public</id>
                <name>Public Repositories</name>
                <url>http://localhost:8081/nexus/content/groups/public/</url>
            </pluginRepository>
        </pluginRepositories>
    </profile>
    ```
    + `<pluginRepositories>`:{{c1:: 插件仓库，maven的运行依赖插件，也需要从私服下载插件 }}
    + `<url>`:{{c1:: 仓库地址，即nexus仓库组的地址 }}
    + `<releases>`:{{c1:: 是否下载releases构件 }}
    + `<snapshots>`:{{c1:: 是否下载snapshots构件 }}
    + `<updatePolicy>`: {{c1::配置Maven检查更新的频率。 always（一直），daily（默认，每日），interval：X（这里X是以分钟为单位的时间间隔），或者never（从不）。 }}
    + `<checksumPolicy>`: {{c1:: 配置Maven检查检验和文件的策略。}}
+ 在maven的settings.xml文件中配置激活下载模板
    ```xml
    <activeProfiles>
        <activeProfile>dev</activeProfile>
    </activeProfiles>
    ```

### 将第三方jar安装到本地仓库 [	](maven_20201115082829585)

1. 准备所需jar包
2. mvn install命令进行安装
    ```
    #{{c1:: 
    mvn install:install-file 
    -DgroupId=<group-id>  -DartifactId=<artifact-id>  -Dversion=<version> 
    -Dpackaging=<packaging>  -Dfile=<path-to-thirdpart-jar-file>

    mvn install:install-file  
    -DgroupId=com.oracle -DartifactId=ojdbc14 –Dversion=10.2.0.4.0
    -Dpackaging=jar -Dfile=ojdbc14-10.2.0.4.0.jar
    #}}
    ```
3. 查看本地maven仓库，确认安装是否成功

### 将第三方jar安装到maven私服 [	](maven_20201115082829587)

1. 准备所需jar包
1. 在maven的`settings.xml`配置文件中配置第三方仓库的server信息
    ```xml
        <server>
            <id>thirdparty</id>
            <username>admin</username>
            <password>admin123</password>
        </server>
    ```
1. 执行命令:
    ```
        #{{c1::
        ----进入jar包所在目录运行
        mvn deploy:deploy-file -DgroupId=com.alibaba -DartifactId=fastjson -Dversion=1.1.37 
        -Dpackaging=jar -Dfile=fastjson-1.1.37.jar
        -Durl=http://localhost:8081/nexus/content/repositories/thirdparty/ 
        -DrepositoryId=thirdparty
        #}}
    ```

## 中央仓库 [	](maven_20201115082829590)

### 配置中央仓库镜像 [	](maven_20200410012359801)

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

- id：{{c1::唯一标识一个镜像}}
- name：{{c1::镜像名称}}
- url：{{c1::镜像地址}}
- mirrorOf：{{c1::代表一个镜像的替代位置，例如central就表示代替官方的中央仓库}}
- mirrorOf匹配语法如下：
    + {{c1::![image-20200401164331881](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200401164331881.png)}}

### 中央仓库的概念 [	](maven_20200410012359802)
+ 中央仓库是{{c1::Maven配置文件中默认的仓库地址，如果用户没有修改仓库配置，那么Maven默认会从中央仓库下载依赖。}}
+ 其在超级POM文件中{{c1::默认配置了`<repository>`元素}}

### Maven的快照版本机制 [	](maven_20200410012359804)

+ 将当前项目坐标中`<version>`改为类似{{c1::`2.1-SNAPSHOT`}}的值
+ 然后发布到私服中，发布过程中，maven自动为构件打上时间戳。
+ 类似：{{c1:: 2.1-20091214.221414-13.jar }}
}}
+ 强制更新当前快照版本命令：{{c1:: `mvn clean install-U`}}

### Maven生命周期 [	](maven_20200410012359805790

### clean生命周期阶段与插件目标的绑定关系 [	](maven_20200410012359806)

![image-20200401180528655](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200401180528655.png)

{{c1::![image-20200401164755027](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200401164755027.png)}}

### site生命周期阶段与插件目标的绑定关系 [	](maven_20200410012359808)

![image-20200401180710199](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200401180710199.png)

{{c1:: ![image-20200401180626652](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200401180626652.png) }}

 }}

### default生命周期与内置插件绑定关系及具体任务(打包类型: jar) [	](maven_20200410012359809)

| 生命周期阶段           |               插件目标                | 执行任务                               |
| ---------------------- | :-----------------------------------: | -------------------------------------- |
| process-resources      |   maven-resources-plugin:resources    | {{c1::复制主资源文件至主输出目录}}     |
| compile                |     maven-compiler-plugin:compile      | {{c1::编译主代码至主输出目录}}         |
| process-test-resources | maven-resources-plugin:testRresources | {{c1::复制测试资源文件至测试输出目录}} |
| test-compile           |   maven-compiler-plugin:testCompile   | {{c1::编译测试代码至测试输出目录}}     |
| test                   |      maven-surefire-plugin:test       | {{c1::执行测试用例}}                   |
| package                |         maven-jar-plugin:jar          | {{c1::创建项目jar包}}                  |
| install                |     maven-install-plugin:install      | {{c1::将项目输出构件安装到本地仓库}}   |
| deploy                 |      maven-deploy-plugin:deploy       | {{c1::将项目输出构件部署到远程仓库}}   |

### 将`maven-source-plugin`插件的`jar-no-fork`绑定到default生命周期的verify阶段 [	](maven_20200410012359811)

```xml
<!-- {{c1:: -->
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-source-plugin</artifactId>
        <version>2.1.1</version>
        <executions>
            <execution>
                <id>attach-sources</id>
                <phase>verify</phase>
                <goals>
                    <goal>jar-no-fork</goal>
                </goals>
            </execution>
        </executions>
    </plugin>
    <!-- 当执行 verify生命周期阶段的时候，maven-Source-plugin:jar-no-fork会得以执行，它会创建一个以 sources.Jar结尾的源码文件包。}} -->
```

### 配置maven插件方式 [	](maven_20200410012359813)

+ 命令行配置：{{c1:: `mvn install-Dmaven.test.skip=true`跳过安装配置 }}
+ 插件配置：{{c1:: 在POM中`<plugin>`的子元素`<configuration>`中配置}}
+ 插件任务配置：{{c1:: `<configuration>`下`<tasks>`还可配置插件任务}}

## 聚合与继承 [	](maven_20200410012359814)

### maven聚合的概念 [	](maven_20200410012359816)

+ 作用：{{c1:: 使用一条命令就可以构建多个项目，本质上上是maven提供的工具。}}
+ 必要：{{c1:: 聚合模块的打包方式为`pom`}}
+ 父子目录形式的聚合
    ```xml
    <!-- 通常使用该形式 -->
    <!-- {{c1:: -->
    	<modules>
            <module>account-email</module>
            <module>account-persist</module>
	    </modules>
    <!-- }} -->
    ```
+ 平行目录形式的聚合
    ```xml
    <!-- {{c1:: -->
    	<modules>
            <module>../account-email</module>
            <module>../account-persist</module>
	    </modules>
    <!-- }} -->
    ```

### maven继承的概念 [	](maven_20200410012359817)

+ 作用：{{c1:: 消除重复配置 }}
+ 必要：{{c1:: 与聚合一样，继承模块打包方式也为pom }}
+ 继承父模块语法
    ```xml
        <!-- {{c1:: -->
        <parent>
            <artifactId>com.juvenxu.mvnbook.account</artifactId>
            <groupId>account-parent</groupId>
            <version>1.0-SNAPSHOT</version>
            <!-- 平行目录形式，指定父模块的pom文件 -->
            <relativePath>../account-parent/pom.xml</relativePath>
        </parent>   
        <!-- }} -->
    ```
+ `<relativePath>`的默认值：{{c1:: `../pom.xml` (即父目录的pom.xml)}}

### 同一模块中，聚合与继承的区别 [	](maven_20200410012359819)

|              | 聚合                                | 继承                                |
| :----------- | ----------------------------------- | ----------------------------------- |
| **作用**     | {{c1::方便构建项目}}                | {{c1::消除重复配置}}                |
| **语法**     | {{c1::父模块中配置`<modules>`}}     | {{c1::子模块中配置`<parent>`}}      |
| **打包方式** | {{c1::`<packaging>pom<packaging>`}} | {{c1::`<packaging>pom<packaging>`}} |

### 父模块中 `<dependencyManagement> <pluginManagement>` 与 `<dependencies> <plugins>` 区别 [	](maven_20200410012359821)

+  {{c1::`<dependencies> <plugins>`}} 即使在子项目中不写该依赖项，那么子项目仍然会从父项目中继承该依赖项（全部继承）。
+ {{c1::`<dependencyManagement> <pluginManagement>`}} 里只是声明依赖，并不实现引入，因此子项目需要显示的声明需要用的依赖,无需版本号。

### `<dependency>`中的`<scope>import</scope>` [	](maven_20200410012359823)

+ 作用：{{c1:: 将目标POM中`<dependencyManagement`的配置导入并合并到当前POM的`<dependencyManagement`中 }}
+ 必要：{{c1:: import依赖范围通常都是指向打包类型为pom的模块 }}
+ 具体语法：
    ```xml
        <!-- {{c1:: -->
         <dependencyManagement>
            <dependencies>
                <dependency>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-dependencies</artifactId>
                    <version>2.0.1.BUILD-SNAPSHOT</version>
                    <!-- import依赖范围通常都是指向打包类型为pom的模块 -->
                    <type>pom</type>
                    <scope>import</scope>
                </dependency>
            </dependencies>
        </dependencyManagement>
        <!-- }} -->
    ```
### 超级POM概念 [	](maven_20200410012359825)

+ 作用：{{c1:: 任何一个Maven项目都隐式的继承自该POM }}
+ 位置：{{c1:: lib下maven-model-builder-3.6.3.jar包中 }}

### maven的`Reactor Build Order`概念 [	](maven_20200412024742027)
+ {{c1::Maven按顺序读取POM，读取当前模块时，会检查是否有POM依赖链，如果有会从链顶端开始构建模块。}}
+ {{c1::Reactor Build Order是POM的构建顺序。}}

### 裁剪反应堆 [	](maven_20200412024742032)
+ 作用：构建完整反应堆中的某些个模块。
+ 构建指定的几个模块命令：{{c1::`mvn clean install -pl account-email,account-persist`}}
+ 同时构建所列模块的依赖模块：{{c1::`mvn clean install -pl account-email-am`}}
+ 同时构建依赖于所列模块的模块：{{c1::`mvn clean install -pl account-email-amd`}}
+ 在完整的反应堆构建顺序基础上制定从哪个模块开始构建：{{c1::`mvn clean install -rf account-email`}}
+ 在-pl -am或者-pl -amd的基础上应用-rf参数：{{c1::`mvn clean install -pl account-parent -amd -rf acount-email`}}

### windows下安装Nexus与启动 [	](maven_20200412024742034)

1. 下载Nexus安装包后。
2. {{c1:: 在.../nexus-3.14.0-04-win64/nexus-3.14.0-04/bin 目录下，以管理员身份运行cmd。}}
3. 启动nexus服务
   -  启动nexus服务命令：{{c1::`nexus.exe /run`}}
   - 安装nexus本地服务来启动
     - 安装服务：{{c1::`nexus.exe /install <optional-service-name>`}}
     - 启动服务：{{c1::`nexus.exe /start <optional-service-name>`}}
     - 关闭服务：{{c1::`nexus.exe /stop <optional-service-name>`}}
     - 手动开启与关闭服务：{{c1::`控制面板\系统和安全\管理工具\服务`}}
4. 访问Nexus:{{c1::`http://localhost:8081/`}}

### nexus仓库类型 [	](maven_20200412024742035)

默认安装有以下这几个仓库，在控制台也可以修改远程仓库的地址，第三方仓库等。

| 仓库类型 | 作用                                                         |
| -------- | :----------------------------------------------------------- |
| hosted   | {{c1::本地仓库，通常我们会部署自己的构件到这一类型的仓库。比如公司的第二方库}} |
| proxy    | {{c1::代理仓库，它们被用来代理远程的公共仓库，如maven中央仓库。}} |
| group    | {{c1::仓库组，用来合并多个hosted/proxy仓库，当你的项目希望在多个repository使用资源时就不需要多次引用了，只需要引用一个group即可。}} |
| virtual  | {{c1::基本用不到，重点关注上面三个仓库的使用}} |

## Maven测试 [	](maven_20200416080933417)

### maven-surefire-plugin的test目标自动执行测试源码类名的默认规则？ [	](maven_20200416080933420)

+ `* /Test*.java`:{{c1:: 任何子目录下所有命令以Test开头的java类}}
+ `** / * Test.java`:{{c1:: 任何子目录下所有命令以Test结尾的java类}}
+ `** / * TestCase.java`:{{c1:: 任何子目录下所有命令以TestCase结尾的java类}}

### maven构建项目时跳过测试 [	](maven_20200416080933422)

+ 直接跳过测试：{{c1:: `mvn package -DskipTests`}}
+ 跳过测试与测试编译：{{c1:: `mvn package -Dmaven.test.skip=true`}}

### 动态指定要运行的测试用例 [	](maven_20200416080933424)

- 只执行单个测试类：{{c1:: `mvn test -Dtest = RandomGeneratorTest`}}
- 执行符合通配符的类：{{c1:: `mvn test -Dtest = Random*Test`}}
- 结合使星号与逗号指定类：{{c1:: `mvn test -Dtest = Random*Test,AccountCaptchaServiceTest`}}

### Maven生成的基本测试报告 [	](maven_20200416080933426)

- maven-surefire-plugin会在项目的{{c1:: target/surefire-reports}}目录下生成两种风格的错误报告
  1. {{c1::简单测试报告}}
  2. {{c1::与Junit兼容的XML格式}}

### Maven生成代码覆盖率报告 [	](maven_20200416080933428)

- 插件：{{c1::`cobertura-maven-plugin`}}
- 目标命令：{{c1::`mvn cobertura:cobertura`}}
- 报告生成位置：{{c1::`报表生成在target/site/cobertura目录下  `}}

### 配置`maven-surefire-plugin`插件以包含或者排除一些测试类 [	](maven_20200416080933429)

```xml
    <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <atifactId>maven-surefire-plugin</atifactId>
    <version>2.5</version>
    <configuration>
        <!-- 测试以Tests.java结尾的类 -->
        <!-- {{c1:: -->
        <includes>
            <include>** / *Tests.java</include>
        </includes>
        <!-- }} -->
        <!-- 排除运行测试类 -->
        <!-- {{c1:: -->
        <excludes>
            <exclude>** / *ServiceTest.java</exclude>
        </excludes>
        <!-- }} -->
    </configuration>
    </plugin>
```
### TestNG依赖 [	](maven_20200416080933431)
```xml
    <dependency>
    <!-- {{c1:: -->
      <groupId>org.testng</groupId>
      <artifactId>testng</artifactId>
      <version>6.10</version>
      <scope>test</scope>
    <!-- }} -->
    </dependency>
```
### TestNG 与 JUnit 常用类库对应关系 [	](maven_20200416080933433)

| Junit | testNG | 作用 |
|------- | ------- | -------|
|org.junit.Test | org.testng.annotations.Test | {{c1:: 标注方法为测试方法}} |
|org.junit.Assert | org.testng.Assert | {{c1:: 检查测试结果}} |
|org.junit.Before | org.testng.annotations.BeforeMethod | {{c1:: 标注方法在每个测试方法之前运行}} |
|org.junit.After | org.testng.annotations.AfterMethod | {{c1:: 标注方法在每个测试方法之后运行}} |
|org.junit.BeforeClass | org.testng.annotations.BeforeClass | {{c1:: 标注方法在所有测试方法之前运行}} |
|org.junit.AfterClass | org.testng.annotations.AfterClass | {{c1:: 标注方法在所有测试方法之后运行}} |

### 配置maven-surefire-plugin使用testing.xml [	](maven_20200416080933436)
```xml
    <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <atifactId>maven-surefire-plugin</atifactId>
    <version>2.5</version>
    <configuration>
        <!-- {{c1:: -->
        <suiteXmlFiles>
            <suiteXmlFile>testing.xml</suiteXmlFile>
        </suiteXmlFiles>>
        <!-- }} -->
    </configuration>
    </plugin>
```

### 配置TestNG要运行的测试类 [	](maven_20200416080933435)
+ 在`testing.xml`资源文件中配置如下
    ```xml
    <!-- {{c1:: -->
    <suite name="test">
        <test name="login">
            <classes>
                <class name="com.units.mytest.suite.SuiteConfig"/>
                <class name="com.units.mytest.suite.LoginTest"/>
            </classes>
        </test>
    </suite>
    <!-- }} -->
    ```


### `maven-surefire-plugin`测试TestNG测试组中的方法 [	](maven_20200416080933438)

+ 加入测试组：{{c1:: `Test(groups = {"util","medium"})` }}
+ 配置：
    ```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <atifactId>maven-surefire-plugin</atifactId>
            <version>2.5</version>
            <configuration>
            <!-- {{c1:: -->
                <groups>util,medium</groups>
            <!-- }} -->
            </configuration>
        </plugin>
    ```
### maven打包测试代码到本地仓库 [	](maven_20200416080933440)
+ 插件配置：
    ```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <atifactId>maven-jar-plugin</atifactId>
            <version>2.2</version>
            <executions>
                <execution>
                <!-- {{c1:: -->
                    <goals>
                        <goal>test-jar</goal>
                    </goals>
                <!-- }} -->
                </execution>
            </executions>
        </plugin>
    ```
+ 依赖测试包构建配置
    ```xml
        <dependency>
            <groupId>testPackage</groupId>
            <artifactId>testPackage</artifactId>
            <version>1.0.0-SNAPSHOT</version>
            <type>test-jar</type>
            <scope>test</scope>
        </dependency>
    ```
### 生成Maven的web项目目录结构 [	](maven_20200416080933442)
+ pom配置：{{c1:: `<packaging>war</packaging>` }}
+ 在原本的jar项目目录结构之上新添加：{{c1:: `src/main/webapp/`目录结构 }}
+ 该目录结构包含：
    + WEB-INF
        + {{c1:: web.xml }}
    + {{c1:: HTML jsp css js之类的文件 }}

### 配置maven过滤，用指定的参数替换directory下的文件中的参数 [	](maven_20200416080933444)
1. 配置如下
    ```xml
        <build>
            <resources>
            <!-- {{c1:: -->
                <resource>
                    <directory>src/main/resources</directory>
                    <filtering>true</filtering>
                </resource>
            <!-- }} -->
            </resources>
        </build>
    ```
2. 然后在src/main/resources下，添加一个文件，比如叫test.txt。test.txt内容如下：
{{c1:: I want to say :　${name} }}
3. 执行 mvn resources:resources 命令，最后会在target/classes下看到test.txt的内容变成了，如下所示：
{{c1:: I want to say : HelloWorld }}

### 指定maven生成的war包的名字 [	](maven_20200416080933445)
+ 配置：
    ```xml
    <!-- {{c1:: -->
    <build>
        <finalName>account</finalName>
    </build>
    <!-- }} -->
    ```
+ 如果没有设置，{{c1:: 打包后的报名-----artifactId与version拼接的结果 }}

### `jetty-maven-plugin`插件使用 [	](maven_20200416080933447)
1. 配置插件
    ```xml
    <plugin>
        <!-- {{c1:: -->
        <groupId>org.eclipse.jetty</groupId>
        <artifactId>jetty-maven-plugin</artifactId>
        <!-- }} -->
        <version>9.4.7.v20180619</version>
        <configuration>
            <!-- 每隔10秒扫描一次项目变更 -->
            <!-- {{c1:: -->
            <scanInteralSeconds>10</scanInteralSeconds>
            <!-- }} -->	
            <!-- 可以通过：http:localhost:port/test/访问应用 -->
            <!-- {{c1:: -->
            <webAppConfig>
                <contextPath>/test</contextPath>
            </webAppConfig>
            <!-- }} -->	
            <!-- 配置端口号与主机名 -->
            <!-- {{c1:: -->
            <httpConnector>
                <port>8080</port>
                <host>localhost</host>
            </httpConnector>
            <!-- }} -->	
        </configuration>
    </plugin>
    ```
2. 在settings.xml中配置简化命令行:
    ```xml
    <settings>
        <!-- {{c1:: -->
        <pluginGroups>
            <pluginGroup>
                org.eclipse.jetty
            </pluginGroup>
        </pluginGroups>
        <!-- }} -->	
    </settings>
    ```
3. 运行命令行：{{c1:: `mvn jetty:run [-Djetty.port=9999]` }}

### `cargo-maven2-plugin`插件配置 [	](maven_20200416080933449)

1. maven快捷命令配置
    ```xml
    <pluginGroups>
        {{c1::
        <pluginGroup>org.codehaus.cargo</pluginGroup>
        }}
    </pluginGroups>
    ```
2. 本地部署配置
    ```xml
    <plugin>    
    <groupId>org.codehaus.cargo</groupId>    
    <artifactId>cargo-maven2-plugin</artifactId>    
    <version>1.1.3</version>    
    <configuration>    
    <!-- {{c1:: -->
        <container>    
            <containerId>tomcat7x</containerId>    
            <home>E:\tomcat\apache-tomcat-7.0.26</home>    
        </container>    
        <configuration>    
            <type>existing</type>    
            <home>E:\tomcat\apache-tomcat-7.0.26</home>    
            <!--     
            <type>standalone</type>    
            <home>${project.build.directory}/tomcat7x</home>    
            -->    
            <!-- 指定端口 -->
            <properties>
                <cargo.servlet.port>8081</cargo.servlet.port>
            </properties>
        </configuration>
    <!-- }} -->
    </configuration>    
    </plugin>    
    ```
    + standalone模式：{{c1:: 会从Web容器目录复制一份配置到用户指定的目录，然后在此基础上部署应用，每次重新构建，这个目录会被清空，所有配置重新生成}}
    + existing模式：{{c1:: 用户需要指定现有的Web容器配置目录， 然后Cargo会直接使用这些配置并将应用部署到对应的位置。}}
    + 启用命令：{{c1:: `mvn cargo：start`}}
3. 远程部署
    ```xml
             <plugin>
                <groupId>org.codehaus.cargo</groupId>
                <artifactId>cargo-maven2-plugin</artifactId>
                <version>1.0</version>
                <configuration>
                    <!-- {{c1:: -->
                    <container>
                        <containerId>tomcat6x</containerId>
                        <type>remote</type>
                    </container>
                    <configuration>
                        <type>runtime</type>
                        <properties>
                            <cargo.remote.username>admin</cargo.remote.username>
                            <cargo.remote.password>admin</cargo.remote.password>
                            <cargo.remote.manager.url>http://localhost:8080/manager</cargo.remote.manager.url>
                        </properties>
                    </configuration>
                    <!-- }} -->
                </configuration>
            </plugin>
    ```
    + tomcat的tomcat-users.xml中配置管理员密码

    ```xml
        <!-- {{c1:: -->
        <tomcat-users>
            <role rolename="manager"/>
            <user username="admin" password="admin" roles="manager"/>
        </tomcat-users>
        <!-- }} -->
    ```
    + 使用命令:{{c1::`mvn cargo:redeploy`}}

### maven版本号定义约定 [	](maven_20200510104820634)
+ 版本号组成规则：{{c1::<主版本>.<次版本>.<增量版本>-<里程碑版本>}}
+ 例如：{{c1::1.3.4-beta-2 ,3.0-alpha-1}}
+ 主版本：{{c1::表示项目的中大架构变更；}}
+ 次版本：{{c1::表示交大范围的功能增加和变化，及bug修复；}}
+ 增量版本：{{c1::一般只中大bug的修复；}}
+ 里程碑版本：{{c1::与正式版相比，往往表示不是非常稳定，还需要很多测试。}}
+ 排序规则：{{c1::前3项按数字大小顺序，里程碑版本按字符串排序。}}
+ 版本（alpha,beta等）的解释：{{c1:: ![image-20200513071149330](C:\Users\Yun\AppData\Roaming\Typora\typora-user-images\image-20200513071149330.png) }}

### maven-release-plugin [	](maven_20200510104820636)
+ `mvn release:prepare`的作用:{{c1:: 实现自动打tag、递增版本号 }}
+ `mvn release:perform`的作用：{{c1::签出`mvn release:prepare`生成的标签中的源代码，并部署到私库。}}
+ `mvn release:rollback`的作用：{{c1::回退`mvn release:prepare`的操作，不会删除已生产的标签。}}
+ 如果需要跳过单元测试，可以加入参数: {{c1::`-Darguments="-DskipTests"`}}
+ 如果不需要源码与javadoc，可以加入参数:{{c1::`--DuseReleaseProfile=false`}}
+ 必要配置
  1. git远程创库SCM配置
  ```xml
    <scm>
    <!-- {{c1:: -->
        <connection>scm:git:http://git-local.bnz.com/srv/bnz-ep.git</connection>
        <url>http://git-local.bnz.com/srv/bnz-ep</url>
        <developerConnection>scm:git:http://git-local.bnz.com/srv/bnz-ep.git</developerConnection>
    <!-- }} -->
    </scm>
  ```
  2. 私库的权限配置
  ```xml
    <!-- {{c1:: -->
    <server>
      <id>your id</id>
      <username>your username</username>
      <password>your pass</password>
    </server>
    //...
    <!-- }} -->
  ```

### maven的6种属性 [	](maven_20200510104820638)

| 类型            | 含义                                                |
| --------------- | --------------------------------------------------- |
| 2个常用内置属性 | {{c1:: ${basedir}:项目根目录,${version}:项目版本 }} |
| POM属性         | {{c1:: ${project.artifactId} }}                     |
| 自定义属性      | {{c1:: 定义在`<properties>`元素下 }}                |
| Settings属性    | {{c1:: ${settings.localRepository} }}               |
| Java系统属性    | {{c1:: ${user.home} }}                              |
| 环境变量属性    | {{c1:: ${env.JAVA_HOME} }}                          |

### 开启maven的资源过滤 [	](maven_20200510104820640)

```xml
//...
<build>
  <finalName>idea-maven-introduce</finalName>

  <filters> <!-- 指定使用的 filter -->
    <filter>src/main/filters/aaa.properties</filter>
  </filters>
   <!-- 为主资源目录开启过滤 -->
   <!-- {{c1:: -->
  <resources>
    <resource>
      <directory>${project.basedir}/src/main/resources</directory>
      <filtering>true</filtering>
    </resource>
  </resources>
  <!-- }} -->
  <!-- 为测试资源目录开启过滤 -->
   <!-- {{c1:: -->
  <testResources>
    <testResource>
      <directory>${project.basedir}/src/main/resources</directory>
      <filtering>true</filtering>
    </testResource>
  </testResources>
  <!-- }} -->
</build>
```
### maven profile的使用 [	](maven_20200510104820642)

- 查看当前激活的profile：{{c1::`mvn help:active-profiles`}}

- 列出所有的profile命令：{{c1::`mvn help:all-profiles`}}

```xml
<!-- 配置环境名id以及环境中变量的所属名称，建议将id于环境所属变量命名一致 -->
<profiles>
   <!-- {{c1:: -->
    <profile>
        <id>dev</id>
        <properties>
            <env>dev</env>
        </properties>
    </profile>
    <profile>
        <id>pro</id>
        <properties>
            <env>pro</env>
        </properties>
    </profile>
  <!-- }} -->
</profiles>
```

### 激活Profile的方式 [	](maven_20200510104820643)

- 命令行激活：{{c1::`mvn clean install -Pdev-x,dev-y`}}

- settings文件显式激活：
   ```xml
   <settings>
     ...
   <!-- {{c1:: -->
     <activeProfiles>
     	<activeProfile>dev-x</activeProfile>
     </activeProfiles>
   <!-- }} -->
     ...
   </settings>
   ```
- `<activation>`元素配置的4种激活方式
    1. `<activation>`系统属性激活
        ```xml
        <profile>
            <!-- 当存在系统属性test且值为x时，激活该profile -->
            <activation>
            <!-- {{c1:: -->
                <property>
                <name>test</name>
                <value>x</value>
            </property>
            <!-- }} -->
            </activation>
        </profile>
        ```
    2. `<activation>`操作系统环境激活
        ```xml
        <profile>
            <activation>
                <!-- {{c1:: -->
                <os>
                    <name>windows XP</name>
                    <family>windows</family>
                    <arch>x86</arch>
                    <version>5.1.2600</version>
                </os>
                <!-- }} -->
            </activation>
        </profile>
        ```
    3. `<activation>`文件存在与否激活
        ```xml
        <profile>
            <activation>
                <!-- {{c1:: -->
                <file>
                    <missing>x.properties</missing>
                    <exists>y.properties</exists>
                </file>
                <!-- }} -->
            </activation>
        </profile>
        ```
    4. `<activation>`默认激活

        ```xml
        <profile>
            <activation>
                <!-- {{c1:: -->
                <activeByDefault>true</activeByDefault>
                <!-- }} -->
            </activation>
        </profile>
        ```

### maven为web资源目录开启过滤 [	](maven_20200510104820647)
```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-war-plugin</artifactId>
    <version>2.1-beta-1</version>
    <configuration>
     	  <!-- {{c1:: -->
        <webResources>
            <resource>
                <filtering>true</filtering>
                <directory>src/main/webapp</directory>
                <includes>
                    <include>**/*.css</include>
                    <include>**/*.js</include>
                </includes>
            </resource>
        </webResources>
      	<!-- }} -->
    </configuration>
</plugin>
```
### Maven：在profile中激活集成测试配置 [	](maven_20200510104820648)

```xml
<project>
  <!-- {{c1:: -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <!-- 对应 @Test(groups={"unit"})标注的方法 -->
                    <groups>unit</groups>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <profiles>
        <profile>
            <id>full</id>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.apache.maven.plugins</groupId>
                        <artifactId>maven-surefire-plugin</artifactId>
                        <version>2.5</version>
                        <configuration>
                            <groups>unit,integration</groups>
                        </configuration>
                    </plugin>
                </plugins>
            </build>
        </profile>
    </profiles>
    <!-- }} -->
</project>
```
## 项目站点 [	](maven_20200510104820650)

### maven生成项目站点 [	](maven_20200510104820652)

+ 生成项目站点命令：{{c1::`mvn site`}}
+ 将站点预发布到某个本地临时目录下命令：{{c1::`mvn site:stage -DstagingDirectory=D:\tmp`}}
+ 常用的项目报告插件如下
  + 必要配置：{{c1::项目报告插件需要在`<reporting>`元素下的`<plugins>`元素下进行配置。}}
  + maven-javadoc-plugin:{{c1::基于项目源码生成JavaDocs文档}}
  + maven-jxr-plugin:{{c1::将源码生成到web站点上以供查看，聚合项目需配置`<aggregate>`元素}}
  + maven-checkstyle-plugin：{{c1::在站点中生成CheckStyle报告，可使用`<configLocation>`自定义规则。}}
  + maven-pmd-plugin:java：{{c1::源代码分析工具，能够查找代码中的问题，潜在bug，无用代码，可优化代码，重复代码等等。}}
  + maven-changelog-plugin:{{c1::基于当前项目vcs，生成3种不同类型（提交，作者，文件）的变更报告。}}
  + cobertura-maven-plugin:{{c1::在`<reporting>`元素下配置，可以在站点中生成覆盖率报告。}}

### 简单创建一个maven插件 [	](maven_20200510104820654)
+ 使用archetype模板AtifactId：{{c1:: maven-archetype-plugin }}
+ Maven插件项目的两个特色点：
  1. {{c1:: `<packaging>maven-plugin</packaging>` }}
  2. {{c1:: artifactId`为`maven-plugin-api`的依赖 }}
+ 创建自己的Mojo
  1. 继承{{c1:: `AbstractMojo类`}}
  2. 实现{{c1:: `execute()`}}方法
  3. 提供{{c1:: `@goal`标注，在类注解中。}}

### Maven Mojo中`@parameter`的使用 [	](maven_20200510104820656)
```java
    //{{c1::
    @Parameter( property = "sayhi.greeting", defaultValue = "Hello World!",required = true)//}}
    private String greeting;
```
+ 对应配置：
```xml
    <plugin>
        <groupId>sample.plugin</groupId>
        <artifactId>hello-maven-plugin</artifactId>
        <version>1.0-SNAPSHOT</version>
        <configuration>
            <!-- {{c1:: -->
            <greeting>Welcome</greeting>
            <!-- }} -->
        </configuration>
    </plugin>
```

### Maven Mojo中的错误处理和日志 [	](maven_20200510104820658)
- `AbstractMojo`提供了一个 {{c1:: `getLog()` }}方法获得Log对象
- Log对象支持4种级别的日志： {{c1::debug,info,warn,error. }}
  - 例： {{c1:: `getLog().info( "Hello, world." );` }}
- `MojoExecutionException` `MojoFailureException`: {{c1:: 如果`execute()`中有异常输出，就会显示"BUILD ERROR/Failure". }}

### 批处理方式使用archetype [	](maven_20200510104820660)
{{c1:: 
```log
mvn archetype:generate -B \
-DarchetypeArtifactId=yibaiwu-archetype-plugin \
-DarchetypeGroupId=com.alias \
-DarchetypeVersion=1.0-SNAPSHOT \
-DgroupId=com.yibaiwu.demo \
-DartifactId=demo \ 
-Dversion=1.0.0-SNAPSHOT \
-Dpackage=com.yibaiwu.demo \ 
```
}}

### Archetype Maven项目主要包括这4个部分： [	](maven_20200510104820662)
1. `pom.xml`：{{c1:: Archetype自身的POM,与默认maven pom.xml一样。}}
2. `src/main/resources/achetype-resource/pom.xml`：{{c1:: 基于该Archetype生成的项目的POM原型}}
3. `src/main/resources/META-INF/maven/achetype-metadata.xml`：{{c1:: Archetype的描述文件。}}
4. `src/main/resources/archetype-resources/**`：{{c1:: 其他需要包含在Archetype中的内容，常规的有我们自定编写的一些样例代码、配置文件等。}}

### Archetype的描述文件`achetype-metadata.xml` [	](maven_20200510104820664)

- `<directory>`元素：{{c1:: 指定对应的样例代码的文件夹。}}
  - filtered属性：{{c1:: 是否使用maven属性过滤}}
  - packaged属性：{{c1:: 是否将文件放在包文件夹下}}
  - `<include>`:{{c1:: 包含该文件夹下指定文件。}}
- `<requiredProperty>`元素：{{c1:: 定义创建Archetype时必须的参数}}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<archetype-descriptor name="sample">
<!-- {{c1::  -->
    <fileSets>
        <fileSet filtered="true" packaged="true">
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.java</include>
            </includes>
        </fileSet>
    </fileSets>
    <requiredProperties>
        <requiredProperty key="groupId">
            <defaultValue>com.yibaiwu</defaultValue>
        </requiredProperty>
    </requiredProperties>
<!-- }} -->
</archetype-descriptor>
```
