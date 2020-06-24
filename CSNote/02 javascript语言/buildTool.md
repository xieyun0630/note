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



# webPack

### npm install 本地安装与全局安装的区别
+ 本地安装:{{c1:: `npm install grunt`  }}
+ 全局安装:{{c1:: `npm install -g grunt-cli`  }}
+ 要区别在于（后面通过具体的例子来说明）：
+ 本地安装
    1. {{c1:: 将安装包放在 ./node_modules 下（运行npm时所在的目录） }}
    2. {{c1:: 可以通过 require() 来引入本地安装的包 }}
+ 全局安装
    1. {{c1:: 将安装包放在 ~\AppData\Roaming\npm 下 }}
    2. {{c1:: 可以直接在命令行里使用 }}

### npm 中`--save-dev`与`--save`的区别
+ `npm install vue –save `：{{c1:: 依赖会保存到dependencies下，运行时依赖，开发完成后还会用到。}}
+ `npm install webpack –save-dev` ：{{c1:: 依赖会保存到devDependencies下，开发时依赖。}}

### webpack开发环境与生产环境的打包的区别

+ 开发环境打包：{{c1:: `webpack ./src/index.js -o ./build/built.js --mode=development` }}
+ 生产环境打包：{{c1::` }}
+ 区别
    1. {{c1:: 生产环境和开发环境将ES6模块化编译成浏览器能识别的模块化~ }}
    2. {{c1:: 生产环境比开发环境多一个压缩js代码。 }}

### webpack基本配置

+ 目录结构
    + {{c1::`./src/index.js`}}
    + {{c1::`./webpack.config.js`}}
+ 配置文件中基本配置：
    ```js
        //{{c1::
        const { resolve } = require('path');
        const HtmlWebpackPlugin = require('html-webpack-plugin');

        module.exports = {
        entry: './src/index.js',
        output: {
            filename: 'built.js',
            path: resolve(__dirname, 'build')
        },
        module: {
            rules: [
            {
                test: /\.css$/,
                use: [
                'style-loader',
                'css-loader'
                ]
            }
            ]
        },
        plugins: [
            new HtmlWebpackPlugin({
            template: './src/index.html'
            })
        ],
        mode: 'development'
        };
        //}}
    ```

### 打包样式资源配置
```js
module: {
    rules: [
    //{{c1::
      {
        test: /\.css$/,
        use: [
          'style-loader',
          'css-loader'
        ]
      },
      {
        test: /\.less$/,
        use: [
          'style-loader',
          'css-loader',
          'less-loader'
        ]
      }
    //}}
    ]
  }
```


### 打包html资源
+ 需要插件： `HtmlWebpackPlugin`
+ 功能：默认会创建一个空的HTML，自动引入打包输出的所有资源（JS/CSS）
+ 基本配置：
    ```js
        //{{c1::
        new HtmlWebpackPlugin({
        // 复制 './src/index.html' 文件，并自动引入打包输出的所有资源（JS/CSS）
        template: './src/index.html'
        })
        //}}
    ```