### mall实现的功能概览 [ ](mall_20210917101115688)

- 商品模块
  - 商品管理
  - 商品分类管理
  - 商品类型管理
  - 品牌管理
- 订单模块
  - 订单管理
  - 订单设置
  - 退货申请处理
  - 退货原因设置
- 营销模块
  - 秒杀活动管理
  - 优惠价管理
  - 品牌推荐管理
  - 新品推荐管理
  - 人气推荐管理
  - 专题推荐管理
  - 首页广告管理
+ 理解：{{c1::标签}}

### mall数据库表概览 [ ](mall_20210917101115691)

- cms_*：{{c1::内容管理模块相关表}}
- oms_*：{{c1::订单管理模块相关表}}
- pms_*：{{c1::商品模块相关表}}
- sms_*：{{c1::营销模块相关表}}
- ums_*：{{c1::会员模块相关表}}

### 整合SpringBoot+MyBatis搭建基本骨架 [ ](mall_20210917101115693)

1. 使用IDEA初始化一个SpringBoot项目
2. 添加项目依赖
  ```xml
  <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.3.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <dependencies>
        <!--SpringBoot通用依赖模块-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-aop</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <!--MyBatis分页插件-->
        <dependency>
            <groupId>com.github.pagehelper</groupId>
            <artifactId>pagehelper-spring-boot-starter</artifactId>
            <version>1.2.10</version>
        </dependency>
        <!--集成druid连接池-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <!-- MyBatis 生成器 -->
        <dependency>
            <groupId>org.mybatis.generator</groupId>
            <artifactId>mybatis-generator-core</artifactId>
            <version>1.3.3</version>
        </dependency>
        <!--Mysql数据库驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.15</version>
        </dependency>
    </dependencies>
  ```
3. 修改SpringBoot配置文件:
  + 位置:{{c1::在application.yml中添加数据源配置和MyBatis的mapper.xml的路径配置。}}
  ```yml
    server:
        port: 8080
    spring:
        datasource:
        url: jdbc:mysql://localhost:3306/mall?useUnicode=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai
        username: root
        password: root
    mybatis:
        mapper-locations:
        - classpath:mapper/*.xml
        - classpath*:com/**/mapper/*.xml
  ```
4. 项目结构说明:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210916161720.png)}}
5. `Mybatis generator`配置文件:
  + 配置数据库连接，Mybatis generator生成model、mapper接口及mapper.xml的路径
     ```properties
     jdbc.driverClass=com.mysql.cj.jdbc.Driver
     jdbc.connectionURL=jdbc:mysql://81.69.43.171:3306/mall?useUnicode=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai
     jdbc.userId=root
     jdbc.password=123456
    ```
    
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE generatorConfiguration
            PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
            "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
    
    <generatorConfiguration>
        <properties resource="generator.properties"/>
        <context id="MySqlContext" targetRuntime="MyBatis3" defaultModelType="flat">
            <property name="beginningDelimiter" value="`"/>
            <property name="endingDelimiter" value="`"/>
            <property name="javaFileEncoding" value="UTF-8"/>
            <!-- 为模型生成序列化方法-->
            <plugin type="org.mybatis.generator.plugins.SerializablePlugin"/>
            <!-- 为生成的Java模型创建一个toString方法 -->
            <plugin type="org.mybatis.generator.plugins.ToStringPlugin"/>
            <!--可以自定义生成model的代码注释-->
            <commentGenerator type="top.xieyun.mall.tiny.mbg.CommentGenerator">
                <!-- 是否去除自动生成的注释 true：是 ： false:否 -->
                <property name="suppressAllComments" value="true"/>
                <property name="suppressDate" value="true"/>
                <property name="addRemarkComments" value="true"/>
            </commentGenerator>
            <!--配置数据库连接-->
            <jdbcConnection driverClass="${jdbc.driverClass}"
                            connectionURL="${jdbc.connectionURL}"
                            userId="${jdbc.userId}"
                            password="${jdbc.password}">
                <!--解决mysql驱动升级到8.0后不生成指定数据库代码的问题-->
                <property name="nullCatalogMeansCurrent" value="true" />
            </jdbcConnection>
            <!--指定生成model的路径-->
            <javaModelGenerator targetPackage="top.xieyun.mall.tiny.mbg.model" targetProject="mall-tiny-01\src\main\java"/>
            <!--指定生成mapper.xml的路径-->
            <sqlMapGenerator targetPackage="top.xieyun.mall.tiny.mbg.mapper" targetProject="mall-tiny-01\src\main\resources"/>
            <!--指定生成mapper接口的的路径-->
            <javaClientGenerator type="XMLMAPPER" targetPackage="top.xieyun.mall.tiny.mbg.mapper"
                                targetProject="mall-tiny-01\src\main\java"/>
            <!--生成全部表tableName设为%-->
            <table tableName="pms_brand">
                <generatedKey column="id" sqlStatement="MySql" identity="true"/>
            </table>
        </context>
    </generatorConfiguration>
    ```
6. 运行Generator的main函数生成代码:
  ```java
  package top.xieyun.mall.tiny.mbg;
  
  import org.mybatis.generator.api.MyBatisGenerator;
  import org.mybatis.generator.config.Configuration;
  import org.mybatis.generator.config.xml.ConfigurationParser;
  import org.mybatis.generator.internal.DefaultShellCallback;
  
  import java.io.InputStream;
  import java.util.ArrayList;
  import java.util.List;
  
  /**
   * 用于生产MBG的代码
   * Created by macro on 2018/4/26.
   */
  public class Generator {
      public static void main(String[] args) throws Exception {
          //MBG 执行过程中的警告信息
          List<String> warnings = new ArrayList<String>();
          //当生成的代码重复时，覆盖原代码
          boolean overwrite = true;
          //读取我们的 MBG 配置文件
          InputStream is = Generator.class.getResourceAsStream("/generatorConfig.xml");
          ConfigurationParser cp = new ConfigurationParser(warnings);
          Configuration config = cp.parseConfiguration(is);
          is.close();
  
          DefaultShellCallback callback = new DefaultShellCallback(overwrite);
          //创建 MBG
          MyBatisGenerator myBatisGenerator = new MyBatisGenerator(config, callback, warnings);
          //执行生成代码
          myBatisGenerator.generate(null);
          //输出警告信息
          for (String warning : warnings) {
              System.out.println(warning);
          }
      }
  }
  ```
7. 添加MyBatis的Java配置:
  + 用于配置需要动态生成的mapper接口的路径
    ```java
    package top.xieyun.mall.tiny.config;
    
    import org.mybatis.spring.annotation.MapperScan;
    import org.springframework.context.annotation.Configuration;
    
    /**
     * MyBatis配置类
     * Created by macro on 2019/4/8.
     */
    @Configuration
    @MapperScan("top.xieyun.mall.tiny.mbg.mapper")
    public class MyBatisConfig {
    }
    ```
8. 实现Controller中的接口(实现PmsBrand表中的添加、修改、删除及分页查询接口。):
  ```java
  package top.xieyun.mall.tiny.controller;
  
  import top.xieyun.mall.tiny.common.api.CommonPage;
  import top.xieyun.mall.tiny.common.api.CommonResult;
  import top.xieyun.mall.tiny.mbg.model.PmsBrand;
  import top.xieyun.mall.tiny.service.PmsBrandService;
  import org.slf4j.Logger;
  import org.slf4j.LoggerFactory;
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.stereotype.Controller;
  import org.springframework.validation.BindingResult;
  import org.springframework.web.bind.annotation.*;
  
  import java.util.List;
  
  
  /**
   * 品牌管理Controller
   * Created by macro on 2019/4/19.
   */
  @Controller
  @RequestMapping("/brand")
  public class PmsBrandController {
      @Autowired
      private PmsBrandService demoService;
  
      private static final Logger LOGGER = LoggerFactory.getLogger(PmsBrandController.class);
  
      @RequestMapping(value = "listAll", method = RequestMethod.GET)
      @ResponseBody
      public CommonResult<List<PmsBrand>> getBrandList() {
          return CommonResult.success(demoService.listAllBrand());
      }
  
      @RequestMapping(value = "/create", method = RequestMethod.POST)
      @ResponseBody
      public CommonResult createBrand(@RequestBody PmsBrand pmsBrand) {
          CommonResult commonResult;
          int count = demoService.createBrand(pmsBrand);
          if (count == 1) {
              commonResult = CommonResult.success(pmsBrand);
              LOGGER.debug("createBrand success:{}", pmsBrand);
          } else {
              commonResult = CommonResult.failed("操作失败");
              LOGGER.debug("createBrand failed:{}", pmsBrand);
          }
          return commonResult;
      }
  
      @RequestMapping(value = "/update/{id}", method = RequestMethod.POST)
      @ResponseBody
      public CommonResult updateBrand(@PathVariable("id") Long id, @RequestBody PmsBrand pmsBrandDto, BindingResult result) {
          CommonResult commonResult;
          int count = demoService.updateBrand(id, pmsBrandDto);
          if (count == 1) {
              commonResult = CommonResult.success(pmsBrandDto);
              LOGGER.debug("updateBrand success:{}", pmsBrandDto);
          } else {
              commonResult = CommonResult.failed("操作失败");
              LOGGER.debug("updateBrand failed:{}", pmsBrandDto);
          }
          return commonResult;
      }
  
      @RequestMapping(value = "/delete/{id}", method = RequestMethod.GET)
      @ResponseBody
      public CommonResult deleteBrand(@PathVariable("id") Long id) {
          int count = demoService.deleteBrand(id);
          if (count == 1) {
              LOGGER.debug("deleteBrand success :id={}", id);
              return CommonResult.success(null);
          } else {
              LOGGER.debug("deleteBrand failed :id={}", id);
              return CommonResult.failed("操作失败");
          }
      }
  
      @RequestMapping(value = "/list", method = RequestMethod.GET)
      @ResponseBody
      public CommonResult<CommonPage<PmsBrand>> listBrand(@RequestParam(value = "pageNum", defaultValue = "1") Integer pageNum,
                                                          @RequestParam(value = "pageSize", defaultValue = "3") Integer pageSize) {
          List<PmsBrand> brandList = demoService.listBrand(pageNum, pageSize);
          return CommonResult.success(CommonPage.restPage(brandList));
      }
  
      @RequestMapping(value = "/{id}", method = RequestMethod.GET)
      @ResponseBody
      public CommonResult<PmsBrand> brand(@PathVariable("id") Long id) {
          return CommonResult.success(demoService.getBrand(id));
      }
  }
  ```
9. 添加Service接口:
  ```java
  package top.xieyun.mall.tiny.service;
  import top.xieyun.mall.tiny.mbg.model.PmsBrand;
  import java.util.List;
  /**
   * PmsBrandService
   * Created by macro on 2019/4/19.
   */
  public interface PmsBrandService {
      List<PmsBrand> listAllBrand();
      int createBrand(PmsBrand brand);
      int updateBrand(Long id, PmsBrand brand);
      int deleteBrand(Long id);
      List<PmsBrand> listBrand(int pageNum, int pageSize);
      PmsBrand getBrand(Long id);
  }
  ```