### SpringSecurity常用过滤器
+ `SecurityContextPersistenceFilter`:{{c1::  首当其冲的一个过滤器，作用之重要，自不必多言。SecurityContextPersistenceFilter主要是使用SecurityContextRepository在session中保存或更新一个`:{{c1::  SecurityContext，并将SecurityContext给以后的过滤器使用，来为后续filter建立所需的上下文。`:{{c1::  SecurityContext中存储了当前用户的认证以及权限信息。}}
+ `WebAsyncManagerIntegrationFilter`:{{c1::  此过滤器用于集成SecurityContext到Spring异步执行机制中的WebAsyncManager}}
+ `HeaderWriterFilter`:{{c1:: 向请求的Header中添加相应的信息,可在http标签内部使用security`:{{c1:: headers来控制}}
+ `CsrfFilter`:{{c1:: csrf又称跨域请求伪造，SpringSecurity会对所有post请求验证是否包含系统生成的csrf的token信息，如果不包含，则报错。起到防止csrf攻击的效果。}}
+ `LogoutFilter`:{{c1:: 匹配 URL为/logout的请求，实现用户退出,清除认证信息。}}
+ `UsernamePasswordAuthenticationFilter`:{{c1:: 认证操作全靠这个过滤器，默认匹配URL为/login且必须为POST请求。}}
+ `DefaultLoginPageGeneratingFilter`:{{c1:: 如果没有在配置文件中指定认证页面，则由该过滤器生成一个默认认证页面。}}
+ `DefaultLogoutPageGeneratingFilter`:{{c1::  由此过滤器可以生产一个默认的退出登录页面}}
+ `BasicAuthenticationFilter`:{{c1:: 此过滤器会自动解析HTTP请求中头部名字为Authentication，且以Basic开头的头信息。}}
+ `RequestCacheAwareFilter`:{{c1:: 通过HttpSessionRequestCache内部维护了一个RequestCache，用于缓存HttpServletRequest}}
+ `SecurityContextHolderAwareRequestFilter`:{{c1:: 对ServletRequest进行了一次包装，使得request具有更加丰富的API}}
+ `AnonymousAuthenticationFilter`:{{c1:: SecurityContextHolder中认证信息为空,则会创建一个匿名用户存入到SecurityContextHolder中。spring security为了兼容未登录的访问，也走了一套认证流程，只不过是一个匿名的身份。}}
+ `SessionManagementFilter`:{{c1:: ecurityContextRepository限制同一用户开启多个会话的数量}}
+ `FilterSecurityInterceptor`:{{c1:: 取所配置资源访问的授权信息，根据SecurityContextHolder中存储的用户信息来决定其是否有权限。}}
### Spring Security XML基本配置
1. 添加依赖:{{c1::
    ```xml
    <dependency>
        <groupId>org.springframework.security</groupId>
        <artifactId>spring-security-config</artifactId>
        <version>5.1.5.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.security</groupId>
        <artifactId>spring-security-taglibs</artifactId>
        <version>5.1.5.RELEASE</version>
    </dependency>
    ```
    }}
    
2. Security核心过滤器配置:{{c1::
    ```xml
        <!--SpringSecurity核心过滤器链-->
        <!--springSecurityFilterChain名词不能修改-->
        <filter>
            <filter-name>springSecurityFilterChain</filter-name>
            <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
        </filter>
        <filter-mapping>
            <filter-name>springSecurityFilterChain</filter-name>
            <url-pattern>/*</url-pattern>
        </filter-mapping>
    ```
    }}

3. 添加Security约束：{{c1::
   ```xml
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:security="http://www.springframework.org/schema/security"
          xsi:schemaLocation="http://www.springframework.org/schema/security
                   http://www.springframework.org/schema/security/spring-security.xsd">
   ```
   }}

4. 拦截所有请求，检查是否有基本权限：{{c1::
   ```xml
    <!--配置springSecurity-->
    <!--
    auto-config="true"  表示自动加载springsecurity的配置文件
    use-expressions="true" 表示使用spring的el表达式来配置springsecurity
    -->
    <security:http auto-config="true" use-expressions="true">
        <!--拦截资源-->
        <!--
        pattern="/**" 表示拦截所有资源
        access="hasAnyRole('ROLE_USER')" 表示只有ROLE_USER角色才能访问资源
        -->
        <security:intercept-url pattern="/**" access="hasAnyRole('ROLE_USER')"/>
    </security:http>
   ```
   }}

5. 内存中模拟2个临时用户：{{c1::
   ```xml
    <!--设置Spring Security认证用户信息的来源-->
    <!--springsecurity默认的认证必须是加密的，加上{noop}表示不加密认证。-->
    <security:authentication-manager>
        <security:authentication-provider>
            <security:user-service>
                <security:user name="user" password ="{noop}user" authorities="ROLE_USER" />
                <security:user name="admin" password ="{noop}admin" authorities="ROLE_ADMIN" />
            </security:user-service>
        </security:authentication-provider>
    </security:authentication-manager>
   ```
   }}

6. 在父容器中加载springSecurity配置文件:{{c1::
   ```xml
    <import resource="classpath:SpringSecurity.xml" />
   ```
   }}

### 配置SpringSecurity使用自定义认证页面
1. 配置认证信息:{{c1::
    ```xml
       <security:form-login login-page="/login.jsp"
                            login-processing-url="/login"
                            default-target-url="/index.jsp"
                            authentication-failure-url="/failer.jsp"/>
    ```
    }}
2. 配置注销信息：{{c1::
   ```xml
   <!--配置退出登录信息-->
   <security:logout logout-url="/logout" logout-success-url="/login.jsp"/>
   ```
   }}
   + 注意注销操作的csrf处理:{{c1::
     ```xml
     <!-- 一旦开启了csrf防护功能， logout处理器便只支持POST请求方式了！-->
     <form action="${pageContext.request.contextPath}/logout" method="post">
         <security:csrfInput/>
         <input type="submit" value="注销">
     </form>
     ```
     }}
3. 禁用csrf拦截：{{c1::
   ```xml
   <!--去掉csrf拦截的过滤器-->
   <security:csrf disabled="true"/>
   ```
   }}

4. 为jsp添加csrf拦截表单项：{{c1::
  ```xml
  <!--引用标签库-->
  <%@taglib uri="http://www.springframework.org/security/tags" prefix="security"%>
  
  <!-- 使用标签 -->
  <security:csrfInput/>
  ```
  }}

5. 放行静态资源：{{c1::
   ```xml
   <!--释放静态资源-->
   <security:http pattern="/css/**" security="none"/>
   <security:http pattern="/img/**" security="none"/>
   <security:http pattern="/plugins/**" security="none"/>
   <security:http pattern="/failer.jsp" security="none"/>
   ```
   }}

6. 让认证页面可以匿名访问：{{c1::
   ```xml
   <security:intercept-url pattern="/login.jsp" access="permitAll()"/>
   ```
   }}


### 自定义SpringSecurity认证信息来源

+ 实现UserDetailsService接口：{{c1::
  ```java
  public interface UserService extends UserDetailsService {
      public void save(SysUser user);
      public List<SysUser> findAll();
      public Map<String, Object> toAddRolePage(Integer id);
      public void addRoleToUser(Integer userId, Integer[] ids);
  }
  ```
  }}
+ 具体认证信息来源实现类：{{c1::
  ```java
  @Service
  @Transactional
  public class UserServiceImpl implements UserService {
      @Autowired
      private UserDao userDao;
      @Autowired
      private RoleService roleService;
      @Autowired
      private BCryptPasswordEncoder passwordEncoder;
  
      //关于User表的crud操作，略...
      @Override
      public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
          try {
              //根据用户名做查询
              SysUser sysUser = userDao.findByName(username);
              if(sysUser==null){
                  return null;
              }
              List<SimpleGrantedAuthority> authorities = new ArrayList<>();
              List<SysRole> roles = sysUser.getRoles();
              for (SysRole role : roles) {
                  authorities.add(new SimpleGrantedAuthority(role.getRoleName()));
              }
              //{noop}后面的密码，springsecurity会认为是原文。
              // enabled：是否可用
              // accountnonexpired：账户是否失效
              // credentialsnonexpired：密码是否失效
              // accountnonlocked：账户是否锁定
              UserDetails userDetails = new User(sysUser.getUsername(),
                      sysUser.getPassword(),
                      sysUser.getStatus() == 1,
                      true,
                      true,
                      true,
                      authorities);
              return userDetails;
          }catch (Exception e){
              e.printStackTrace();
              //认证失败！
              return null;
          }
      }
  }
  ```
  }}

+ 配置认证信息来源实现类：{{c1::
  ```xml
  <!--把加密对象放入的IOC容器中-->
  <bean id="passwordEncoder" class="org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder"/>
  <!--设置Spring Security认证用户信息的来源-->
  <!--springsecurity默认的认证必须是加密的，加上{noop}表示不加密认证。-->
  <security:authentication-manager>
      <security:authentication-provider user-service-ref="userServiceImpl">
          <security:password-encoder ref="passwordEncoder"/>
      </security:authentication-provider>
  </security:authentication-manager>
  ```
  }}


### RememberMe功能开启

- 主要原理：{{c1::开启rememberMe后，每次登录成功会调用PersistentTokenBasedRememberMeServices的onLoginSuccess方法，该方法会将Token作为Coockie写入到浏览器。}}
1. 开启过滤器：
   + 说明：{{c1::RememberMeAuthenticationFiltert中功能非常简单，会在打开浏览器时，自动判断是否认证，如果没有则调用 autologin进行自动认证。}}
   ```xml
   <!--开启remember me过滤器，设置token存储时间为60秒-->
   <security:remember-me
       data-source-ref="dataSource"
       token-validity-seconds="60"
       remember-me-parameter="remember-me"/>
   ```

2. 持久化rememberMe信息，创建固定的表格式：{{c1::
   ```sql
   CREATE TABLE `persistent_logins` (
   	`username` VARCHAR (64) NOT NULL,
   	`series` VARCHAR (64) NOT NULL,
   	`token` VARCHAR (64) NOT NULL,
   	`last_used` TIMESTAMP NOT NULL,
   	PRIMARY KEY (`series`)
   ) ENGINE = INNODB DEFAULT CHARSET = utf8
   ```
   }}
   + 注意：
     + 数据源的注入。
     + 表格式是spring内部固定的，不可以有修改。

### SpringSecurity登录后获取用户名,控制页面菜单

+ 通过后台API：
  ```java
  //2种方式
  //{{c1::
  SecurityContextHolder.getContext().getAuthentication().getName();
  String username = ((SysUser) SecurityContextHolder.getContext().getAuthentication().getPrincipal()).getUsername();
  //}}
  ```
+ 通过jsp标签库：{{c1::
  ```jsp
  <!--引入库->
  <%@taglib uri="http://www.springframework.org/security/tags" prefix="security"%>
  <!--2种方式-->
  <security:authentication property="principal.username" />
  <security:authentication property="name" />
  ```
  }}
+ 控制jsp页面菜单显示与隐藏：{{c1::
  ```jsp
  <ul class="treeview-menu">
      <security:authorize access="hasAnyRole('ROLE_PRODUCT', 'ROLE_ADMIN')">
      <li id="system-setting">
          <a href="${pageContext.request.contextPath}/product/findAll">
          <i class="fa fa-circle-o"></i>产品管理</a>
      </li>
      </security:authorize>
      <security:authorize access="hasAnyRole('ROLE_PRODUCT', 'ROLE_ADMIN')">
          <li id="system-setting">
              <a href="${pageContext.request.contextPath}/product/findAll">
              <i class="fa fa-circle-o"></i>订单管理</a>
          </li>
      </security:authorize>
  </ul>
  ```
   }}


### SpringSecurity权限控制

+ IOC容器结构说明：{{c1::![image-20210919114621055](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20210919114621055.png)}}
+ 开启动态权限注解支持：{{c1::
  ```xml
  <!--
      开启权限控制的注解支持
      secured-annotations="enabled"     springSecurity内部的权限控制注解开关
      pre-post-annotations="enabled"     spring指定的权限控制的注解开关
      jsr250-annotations="enabled"      开启java250注解支持
      -->
  <security:global-method-security
          secured-annotations="enabled"
          pre-post-annotations="enabled"
          jsr250-annotations="enabled"/>
  ```
  }}
  + 注意：{{c1::该注解需要放在spring-mvc.xml中，原因如上所述。}}

+ 3种权限注解说明：{{c1::
  ```java
      @Secured({"ROLE_PRODUCT","ROLE_ADMIN"})//springSecurity内部制定的注解
      @RequestMapping("/findAll")
      public String findAll1(){
          return "product-list";
      }
          
      @PreAuthorize("hasAnyAuthority('ROLE_PRODUCT','ROLE_ADMIN')")//spring的el表达式注解
      @RequestMapping("/findAll")
      public String findAll2(){
          return "product-list";
      }
  
      @RolesAllowed({"ROLE_PRODUCT","ROLE_ADMIN"}) //jsr250注解
      @RequestMapping("/findAll")
      public String findAll3(){
          return "product-list";
      }
  ```
  }}

### SpringSecurity异常处理几种方式：

+ SpringSecurity自带异常处理方式：{{c1::
  ```xml
  <security:access-denied-handler error-page="/403.jsp"/>
  ```
  }}
+ web.xml中配置对应相应码：{{c1::
  ```
  <!--处理403异常-->
  <error-page>
      <error-code>403</error-code>
      <location>/403.jsp</location>
  </error-page>-->
  
  <!--处理404异常-->
  <error-page>
      <error-code>404</error-code>
      <location>/404.jsp</location>
  </error-page>
  ```
  }}

+ 实现HandlerExceptionResolver接口：{{c1::
  ```java
  @Component
  public class HandlerControllerException implements HandlerExceptionResolver {
      /**
       * @param httpServletRequest
       * @param httpServletResponse
       * @param o  出现异常的对象
       * @param e  出现的异常信息
       * @return   ModelAndView
       */
      @Override
      public ModelAndView resolveException(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) {
          ModelAndView mv = new ModelAndView();
          //将异常信息放入request域中，基本不用
          mv.addObject("errorMsg", e.getMessage());
          //指定不同异常跳转的页面
          if(e instanceof AccessDeniedException){
              mv.setViewName("redirect:/403.jsp");
          }else {
              mv.setViewName("redirect:/500.jsp");
          }
          return mv;
      }
  }
  ```
  }}

+ 使用异常处理注解：{{c1::
  ```java
  @ControllerAdvice
  public class HandlerControllerAdvice{
      @ExceptionHandler(AccessDeniedException.class)
      public String handlerException(){
          return "redirect:/403.jsp";
      }
      @ExceptionHandler(RuntimeException.class)
      public String runtimeHandlerException(){
          return "redirect:/500.jsp";
      }
  }
  ```
  }}

  

### SpringBoot下SpringSecurity工程

+ 导入SpringBoot依赖:{{c1::
  ```xml
  <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.1.3.RELEASE</version>
      <relativePath/>
  </parent>
  <dependencies>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-security</artifactId>
          </dependency>
  </dependencies>
  ```
  }}

+ 创建启动类：{{c1::
  ```java
  @SpringBootApplication
  public class SpringSecurityApplication {
      public static void main(String[] args) {
          SpringApplication.run(SpringSecurityApplication.class, args);
      }
  }
  ```
  }}

+ 创建基本控制器：{{c1::
  ```java
  @Controller
  public class HelloController {
      @RequestMapping("/hello")
      @ResponseBody
      public String hello(){
          return "success";
      }
  }
  ```
  }}
+ SpringBoot下会默认产生一个user用户，{{c1::密码在tomcat启动时初始化(`Using generated security password: xxxx-xxxx-...`)。}}
+ SpringBoot下编写SpringSecurity配置类:{{c1::
    ```java
    @Configuration
    @EnableWebSecurity
    @EnableGlobalMethodSecurity(securedEnabled=true)
    public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

        @Autowired
        private UserService userService;

        //注意，指定加密类后，密码会自动与加密后密码比较
        @Bean
        public BCryptPasswordEncoder passwordEncoder(){
            return new BCryptPasswordEncoder();
        }

        //指定认证对象的来源
        public void configure(AuthenticationManagerBuilder auth) throws Exception {
            auth.userDetailsService(userService).passwordEncoder(passwordEncoder());
            //使用内存配置
            //auth.inMemoryAuthentication()
            //.withUser("user")
            //.password("{noop}123456")
            //.roles("USER");
        }
        //SpringSecurity配置信息
        public void configure(HttpSecurity http) throws Exception {
            http.authorizeRequests()
                    .antMatchers("/login.jsp", "failer.jsp", "/css/**", "/img/**", "/plugins/**").permitAll()
                    .antMatchers("/product").hasAnyRole("USER")
                    .anyRequest().authenticated()
                    .and()
                    .formLogin()
                    .loginPage("/login.jsp")
                    .loginProcessingUrl("/login")
                    .successForwardUrl("/index.jsp")
                    .failureForwardUrl("/failer.jsp")
                    .and()
                    .logout()
                    .logoutSuccessUrl("/logout")
                    .invalidateHttpSession(true)
                    .logoutSuccessUrl("/login.jsp")
                    .and()
                    .csrf()
                    .disable();
        }
    }
    ```
    }}


### SpringBoot整合JSP

+ 添加依赖：{{c1::
  ```xml
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
  </dependency>
  <dependency>
      <groupId>org.apache.tomcat.embed</groupId>
      <artifactId>tomcat-embed-jasper</artifactId>
  </dependency>
  ```
  }}

+ 修改打包方式：{{c1::
  ```xml
  <groupId>com.itheima</groupId>
  <artifactId>springboot_security_jsp</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>
  ```
  }}
+ 配置视图解析器：{{c1::
  ```yml
  spring:
    mvc:
      view:
        prefix: /pages/
        suffix: .jsp
  ```
  }}

+ 添加webapp目录并添加静态资源
+ 添加SpringBoot插件依赖运行run目标:{{c1::
  ```xml
  <plugins>
      <plugin>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-maven-plugin</artifactId>
      </plugin>
  </plugins>
  ```
  }}

### SpringBoot加入通用mapper
+ 添加依赖：{{c1::
  ```xml
  <dependency>
      <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
      <version>5.1.47</version>
  </dependency>
  <dependency>
      <groupId>tk.mybatis</groupId>
      <artifactId>mapper-spring-boot-starter</artifactId>
      <version>2.1.5</version>
  </dependency>
  ```
  }}
+ 配置数据源：{{c1::
  ```yml
  spring:
    datasource:
      driver-class-name: com.mysql.jdbc.Driver
      url: jdbc:mysql:///security_authority
      username: root
      password: root
  mybatis:
    type-aliases-package: com.itheima.domain
    configuration:
      map-underscore-to-camel-case: true
  logging:
    level:
      com.itheima: debug
  ```
  }}
+ 自动扫码加入容器：{{c1::
  ```java
  package com.itheima;
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  import tk.mybatis.spring.annotation.MapperScan;
  @SpringBootApplication
  @MapperScan("com.itheima.mapper")
  public class SpringSecurityApplication {
      public static void main(String[] args) {
          SpringApplication.run(SpringSecurityApplication.class, args);
      }
  }
  ```
  }}

  ### SpringBoot下配置Security自定义认证信息来源

  + 实现UserDetails接口:{{c1::
    ```java
    
    @Data
    public class SysUser implements UserDetails {
    
        private Integer id;
        private String username;
        private String password;
        private Integer status;
        //用户角色一对多关系	
        private List<SysRole> roles;
    
        @JsonIgnore
        @Override
        public Collection<? extends GrantedAuthority> getAuthorities() {
            return roles;
        }
    
        @Override
        public String getPassword() {
            return password;
        }
    
        @Override
        public String getUsername() {
            return username;
        }
    
        @JsonIgnore
        @Override
        public boolean isAccountNonExpired() {
            return true;
        }
    
        @JsonIgnore
        @Override
        public boolean isAccountNonLocked() {
            return true;
        }
    
        @JsonIgnore
        @Override
        public boolean isCredentialsNonExpired() {
            return true;
        }
    
        @JsonIgnore
        @Override
        public boolean isEnabled() {
            return true;
        }
    }
    ```
    }}
  + 实现GrantedAuthority接口:{{c1::
    ```java
    @Data
    public class SysRole implements GrantedAuthority {
    
        private Integer id;
        private String roleName;
        private String roleDesc;
    
        @JsonIgnore
        @Override
        public String getAuthority() {
            return roleName;
        }
    }
    ```
    }}
  + 实现UserService:{{c1::
    ```java
    public interface UserMapper extends Mapper<SysUser> {
    
        @Select("select * from sys_user where username = #{username}")
        @Results({
                @Result(id = true, property = "id", column = "id"),
                @Result(property = "roles", column = "id", javaType = List.class,
                    many = @Many(select = "com.itheima.mapper.RoleMapper.findByUid"))
        })
        public SysUser findByName(String username);
    }
    
    @Service
    @Transactional
    public class UserServiceImpl implements UserService {
    
        @Autowired
        private UserMapper userMapper;
    
        @Override
        public UserDetails loadUserByUsername(String s) throws UsernameNotFoundException {
            return userMapper.findByName(s);
        }
    }
    
    
    public interface UserService extends UserDetailsService {
    }
    ```
    }}

  + 配置认证对象来源：{{c1::
    ```java
    @Configuration
    @EnableWebSecurity
    @EnableGlobalMethodSecurity(securedEnabled=true)
    public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
    
        @Autowired
        private UserService userService;
        @Bean
        public BCryptPasswordEncoder passwordEncoder(){
            return new BCryptPasswordEncoder();
        }
        //指定认证对象的来源
        public void configure(AuthenticationManagerBuilder auth) throws Exception {
            auth.userDetailsService(userService).passwordEncoder(passwordEncoder());
        }
        
        //SpringSecurity配置信息
    	//...
    }
    ```
    }}

### SpringBoot Security权限配置

+ 开启权限注解：{{c1::
  ```java
  @Configuration
  @EnableWebSecurity
  @EnableGlobalMethodSecurity(securedEnabled=true)
  public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
  	//...
  }
  ```
  }}
+ 标记权限：{{c1::
  ```java
  @Controller
  @RequestMapping("/product")
  public class ProductController {
      @Secured("ROLE_PRODUCT")
      @RequestMapping("/findAll")
      public String findAll(){
          return "product-list";
      }
  }
  ```
  }}

+ 异常处理：{{c1::
  ```java
  @ControllerAdvice
  public class HandlerControllerException {
  
      @ExceptionHandler(RuntimeException.class)
      public String handException(RuntimeException e){
          if(e instanceof AccessDeniedException){
              return "redirect:/403.jsp";
          }
          return "redirect:/500.jsp";
      }
  }
  ```
  }}
  


