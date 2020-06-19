## 模块化
### 模块化进化史
1. 全局function模式
    + 例子：
    ```js
        //{{c1::
        let data2 = 'other data'
        function foo() {  //与另一个模块中的函数冲突了
        console.log(`foo() ${data2}`)
        }
        //}}
    ```
    + 特点： {{c1:: 将不同的功能封装成不同的全局函数 }}
    + 缺点： {{c1:: Global被污染，容易命名冲突 }}

2. namespace模式
    + 例子：
    ```js
        //{{c1::
        let myModule2 = {
            data: 'atguigu.com2222',
            foo() {
                console.log(`foo() ${this.data}`)
            },
            bar() {
                console.log(`bar() ${this.data}`)
            }
        }
        //}}
    ```
    + 特点： {{c1:: 简单对象封装 }}
    + 缺点： {{c1:: 不能隐藏模块中的细节 }}
3. IIFE模式
    + IIFE全称:immediately-invoked function expression(立即调用函数表达式)
    + 例子：
    ```js
        //{{c1::
        (function (window, $) {
            //数据
            let data = 'atguigu.com'
            //操作数据的函数
            function foo() { //用于暴露有函数
                console.log(`foo() ${data}`)
                $('body').css('background', 'red')
            }
            function bar() {//用于暴露有函数
                console.log(`bar() ${data}`)
                otherFun() //内部调用
            }
            function otherFun() { //内部私有的函数
                console.log('otherFun()')
            }
            //暴露行为
            window.myModule = {foo, bar}
        })(window, jQuery)
        //}}
    ```
    + 特点： {{c1:: 现代模块实现的基础。 }}
    + 缺点： {{c1:: 页面需要加载多个js文件导致请求过多，难以维护依赖关系 }}

### CommonJS规范：Nodejs端的模块化

+ 项目目录结构:
    {{c1::
    ```
    |-modules
        |-module1.js
        |-module2.js
        |-module3.js
    |-app.js
    |-package.json
    ```
    }}
+ 定义暴露模块：
    1.  {{c1:: `module.exports = value;` }}
    2.  {{c1:: `exports.xxx = value;` }}
+ 引入模块:
    1. {{c1:: `var module = require(模块名或模块路径);` }}

### CommonJS规范：浏览器端模块化

+ npm安装编译工具：
  + 全局: {{c1:: npm install browserify -g }}
  + 局部: {{c1:: npm install browserify --save-dev }}
+ 项目目录结构:
    {{c1::
    ```js
        |-js
            |-dist //打包生成文件的目录
            |-src //源码所在的目录
            |-module1.js
            |-module2.js
            |-module3.js
            |-app.js //应用主源文件
        |-index.html
        |-package.json
    ```
    }}
+ 定义暴露模块：
    1. {{c1:: `module.exports = value;` }}
    2. {{c1:: `exports.xxx = value;` }}
+ 引入模块:
    1. {{c1:: `var module = require(模块名或模块路径);` }}
+ 编译：
    1. browserify `js/src/app.js -o js/dist/bundle.js`
+ 页面使用引入:
    1. `<script type="text/javascript" src="js/dist/bundle.js"></script>`

