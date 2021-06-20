## 基础

### jeecg项目启动命令相关

+ 后端启动类：{{c1::`JeecgSystemApplication.main()`}}
+ 前端启动命令
  ```bash
  #{{c1::
  # 安装yarn
  npm install -g yarn

  # 下载依赖
  yarn install

  # 启动
  yarn run serve

  # 编译项目
  yarn run build

  # Lints and fixes files
  yarn run lint
  #}}
  ```

### jeecg中数据库配置(连接和账号密码)

+ application-dev.yml文件下
```yaml
  #{{c1::
      datasource:
        master:
          url: jdbc:mysql://127.0.0.1:3306/jeecg-boot?characterEncoding=UTF-8&useUnicode=true&useSSL=false&tinyInt1isBit=false&allowPublicKeyRetrieval=true&serverTimezone=Asia/Shanghai
          username: root
          password: 123456
          driver-class-name: com.mysql.cj.jdbc.Driver
  #}}
```

### jeecg中redis 配置

+ application-dev.yml文件
```yaml
  #redis 配置
  #{{c1::
  redis:
    database: 0
    host: 127.0.0.1
    lettuce:
      pool:
        max-active: 8   #最大连接数据库连接数,设 0 为没有限制
        max-idle: 8     #最大等待连接中的数量,设 0 为没有限制
        max-wait: -1ms  #最大建立连接等待时间。如果超过此时间将接到异常。设为-1表示无限制。
        min-idle: 0     #最小等待连接中的数量,设 0 为没有限制
      shutdown-timeout: 100ms
    password: ''
    port: 6379
  #}}
```

### jeecg基本开发步骤
+ 后端
  + 添加demo请求到：JeecgDemoController
    ```java
    //{{c1::
    @RestController
    @RequestMapping("/test/jeecgDemo")
    @Slf4j
    public class JeecgDemoController {
    	/**
    	 * hello world
    	 * 
    	 * @param id
    	 * @return
    	 */
    	@GetMapping(value = "/hello")
    	public Result<String> hello() {
    		Result<String> result = new Result<String>();
    		result.setResult("Hello World!");
    		result.setSuccess(true);
    		return result;
    	}
    }
    //}}
    ```
  + 配置下shiro拦截器ShiroConfig排除。
    ```
    #{{c1::
    配置文件：jeecg-boot-base/jeecg-boot-base-core/org.jeecg.config.shiro.ShiroConfig
    加入配置：filterChainDefinitionMap.put("/test/jeecgDemo/hello", "anon");
    #}}
    ```
+ 前端
  + 创建vue页面src/views/jeecg/helloworld.vue
    ```vue
    <!-- {{c1:: -->
    <template>
      <div>
        {{ msg }}
      </div>
    </template>
    
    <script>
      import {getAction} from '@/api/manage'
      export default {
        data () {
          return {
            msg: ""
          }
        },
        methods: {
          hello () {
            var url = "/test/jeecgDemo/hello"
            getAction(url).then((res) => {
              if (res.success) {
                this.msg = res.result;
              }
            })
          }
        },
        created() {
          this.hello();
        }
      }
    </script>
    <!-- }} -->
    ```
+ 配置菜单：
  + 配置hello菜单【系统管理】-【菜单管理】
    + 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210618095123.png)}}
    + 其中前端组件配置相对src/views/目录下的 目录名+文件名：{{c1::例如页面src/views/jeecg/helloworld.vue 前端组件配置 jeecg/helloworld}}
+ 用户角色授权【系统管理】-【角色管理】-授权

