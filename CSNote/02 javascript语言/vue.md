### 声明式绑定,条件与循环 [	](vue_20200703080524558)

+ 绑定元素文本：{{c1::  `{{ message }}` }}
+ 绑定元素attribute指令:{{c1::  `<span v-bind:title="message"></span>` }}
+ 条件绑定指令：{{c1:: `<p v-if="seen">现在你看到我了</p>` }}
+ 循环绑定指令：{{c1:: `v-for="todo in todos"` }}
    + 元素声明:
    ```html
    <!-- {{c1:: -->
        <li v-for="todo in todos">
            {{ todo.text }}
        </li>
    <!-- }} -->
    ```
    + 传入数据:
    ```js
    //{{c1::
    var app4 = new Vue({
        el: '#app-4',
        data: {
            todos: [
            { text: '学习 JavaScript' },
            { text: '学习 Vue' },
            { text: '整个牛项目' }
            ]
        }
    })
    //}} 
    ```

### 常用指令 [	](vue_20200703080524559)

+ `v-on:click`
    + 作用：{{c1:: 指定一个在vue选项对象methods属性中的方法作为监听器 }}
    + 用法：{{c1:: `v-on:click="reverseMessage"` }}
+ `v-model`
    + 作用：{{c1:: 将某个表单对象的值**双向绑定**到指定`data`属性。 }}
    + 用法：{{c1:: `<input v-model="message">` }}
+ `v-once`
    + 作用：执行一次性地插值，当数据改变时，插值处的内容不会更新。
    + 用法：{{c1:: `<span v-once>这个将不会改变: {{ msg }}</span>` }}
+ `v-html`
    + 作用：输出真正的 HTML，`{{ msg }}`会将数据解释为普通文本
    + 用法: `<span v-html="rawHtml"></span>`
+ `v-bind`
    + 作用：{{c1::将`HTML attribute`绑定到**某个**data属性}}
    + 用法: {{c1::`<button v-bind:disabled="isButtonDisabled">Button</button>`}}
        + 注意：{{c1::如果 `isButtonDisabled` 的值是 `null`、`undefined` 或 `false`，则 `disabled` `attribute` 甚至不会被包含在渲染出来的 `<button>` 元素中。}}

### 组件化例子：列表 [	](vue_20200703080524561)

- 自定义组件实现下面效果：
    ![image-20200703145722275](vue.assets/image-20200703145722275.png)
- 组件使用：
  ```html
  <!-- {{c1:: -->
      <todo-item
        v-for="item in groceryList"
        v-bind:todo="item"
        v-bind:key="item.id"
      ></todo-item>
  <!-- }} -->
  ```
+ JS定义:
  ```js
  //{{c1::
  Vue.component('todo-item', {
    props: ['todo'],
    template: '<li>{{ todo.text }}</li>'
  })
  
  var app7 = new Vue({
    el: '#app-7',
    data: {
      groceryList: [
        { id: 0, text: '蔬菜' },
        { id: 1, text: '奶酪' },
        { id: 2, text: '随便其它什么人吃的东西' }
      ]
    }
  })
  //}}
  ```

### 生命周期钩子 [	](vue_20200703080524562)

+ created 钩子可以用来在一个实例被创建之后执行代码：
    ```js
    new Vue({
        //{{c1::
        data: {
            a: 1
        },
        created: function () {
            // `this` 指向 vm 实例
            console.log('a is: ' + this.a)
        }
        //}}
    })
    ```
+ 也有一些其它的钩子，在实例生命周期的不同阶段被调用，如 `mounted`、`updated` 和 `destroyed`

## 模板语法 [	](vue_20200703080524563)

### 对于所有的数据绑定，Vue.js 都提供了完全的 JavaScript 表达式支持 [	](vue_20200703080524564)
```js
    //{{c1::
    {{ number + 1 }}
    {{ ok ? 'YES' : 'NO' }}
    {{ message.split('').reverse().join('') }}
    <div v-bind:id="'list-' + id"></div>
    //}}
```

### 指令 [	](vue_20200703080524565)
+ 意义: {{c1:: 指令 (`Directives`) 是带有 `v-` 前缀的特殊 `attribute`。 }}
+ 作用: {{c1:: 当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。 }}
+ 参数: {{c1:: 一些指令能够接收一个“参数”，在指令名称之后以冒号表示。`<a v-bind:href="url">...</a>` }}
+ 动态参数:
    + {{c1:: `<a v-bind:[attributeName]="url"> ... </a>`}}
        1. {{c1:: 这里的 attributeName 会被作为一个 JavaScript 表达式进行动态求值，求得的值将会作为最终的参数来使用。}}
        2. {{c1:: 如果你的 Vue 实例有一个 data property attributeName，其值为 "href"，那么这个绑定将等价于 v-bind:href。}}
    + 约束: {{c1:: 某些字符，如空格和引号，放在 HTML attribute 名里是无效的 }}
    + 注意：{{c1:: 直接在一个 HTML 文件里撰写模板时，避免使用大写字符来命名键名 }}
+ 修饰符：{{c1:: `<form v-on:submit.prevent="onSubmit">...</form>` }}

### 指令缩写 [	](vue_20200703080524566)
+ `v-bind` 缩写
    ```html
    <!-- 完整语法 -->
    <a v-bind:href="url">...</a>
    <!-- 缩写 -->
    <!-- {{c1:: -->
    <a :href="url">...</a>
    <!-- }} -->
    <!-- 动态参数的缩写 (2.6.0+) -->
    <!-- {{c1:: -->
    <a :[key]="url"> ... </a>
    <!-- }} -->
    ```
+ `v-on` 缩写
    ```html
    <!-- 完整语法 -->
    <a v-on:click="doSomething">...</a>
    <!-- 缩写 -->
    <!-- {{c1:: -->
    <a @click="doSomething">...</a>
    <!-- }} -->
    <!-- 动态参数的缩写 (2.6.0+) -->
    <!-- {{c1:: -->
    <a @[event]="doSomething"> ... </a>
    <!-- }} -->
    ```
### vue中的计算属性 [	](vue_20200703080524567)
+ 基础例子
    + html对应元素
    ```html
    <div id="example">
        <p>Original message: "{{ message }}"</p>
        <p>Computed reversed message: "{{ reversedMessage }}"</p>
    </div>
    ```
    + 对应的Vue代码
    ```js
    //{{c1::
    var vm = new Vue({
        el: '#example',
        data: {
        message: 'Hello'
        },
        computed: {
        // 计算属性的 getter
        reversedMessage: function () {
            // `this` 指向 vm 实例
            return this.message.split('').reverse().join('')
        }
        }
    })
    //}}
    ```
+ 计算属性缓存 vs 方法
    + {{c1::计算属性是基于它们的响应式依赖进行缓存的。}}
    + {{c1::调用方法将总会再次执行函数。}}

## 计算属性与监听器 [	](vue_20200703080524568)

### 计算属性的 setter [	](vue_20200703080524569)
```js
// ...
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    //{{c1::
    set: function (newValue) {
        var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
    //}}
  }
}
// ...
```
+ 现在再运行 vm.fullName = 'John Doe' 时，setter 会被调用，vm.firstName 和 vm.lastName 也会相应地被更新。

### 侦听器：vatch选项 [	](vue_20200703080524570)

```js
var watchExampleVM = new Vue({
  el: '#watch-example',
  data: {
    question: '',
    answer: 'I cannot give you an answer until you ask a question!'
  },
  watch: {
    // 如果 `question` 发生改变，这个函数就会运行
    //{{c1::
    question: function (newQuestion, oldQuestion) {
        this.answer = 'Waiting for you to stop typing...'
    }
    //}}
  })
```

## 绑定HTML Class [	](vue_20200703080524571)

### 绑定HTML Class:对象语法 [	](vue_20200703080524572)
+ 3种`v-bind:class`的调用方式
  1. 基本语法：{{c1:: `<div v-bind:class="{ active: isActive }"></div>`}}
  2. 与已有class属性混合：{{c1:: `<div class="static" v-bind:class="{ active: isActive, 'text-danger': hasError }"></div>`}}
  3. 属性对象：{{c1:: `<div v-bind:class="classObject"></div>`}}

+ 与计算属性结合返回对象
  ```js
        data: {
        isActive: true,
        error: null
        },
        computed: {
            classObject: function () {
                return {
                active: this.isActive && !this.error,
                'text-danger': this.error && this.error.type === 'fatal'
                }
            }
        }
  ```
### 绑定HTML Class:数组语法 [	](vue_20200703080524573)

  + 基本语法：{{c1:: `<div v-bind:class="[activeClass, errorClass]"></div>` }}
  + 使用三元表达式:{{c1:: `<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>` }}
  + 数组中使用对象：{{c1::  `<div v-bind:class="[{ active: isActive }, errorClass]"></div>` }}

### 绑定HTML Class:组件上的`v-bind:class` [	](vue_20200703080524574)

+ 如果你声明了这个组件：
    ```js
        Vue.component('my-component', {
        template: '<p class="foo bar">Hi</p>'
        })
    ```
+ 对于带数据绑定 class ：
    ```html
    <my-component v-bind:class="{ active: isActive }"></my-component>
    ```
+ 当 isActive 为true时，HTML 将被渲染成为：{{c1:: `<p class="foo bar active">Hi</p>` }}

### 绑定内联样式 [	](vue_20200703080524575)

+ 对象语法：{{c1:: `<div v-bind:style="styleObject"></div>`}}
+ 数组语法：{{c1:: `<div v-bind:style="[baseStyles, overridingStyles]"></div>`}}
+ 自动添加前缀：{{c1:: 当使用类似`transform`的样式时自动添加前缀}}
+ 多重值：{{c1:: `<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>`}}
  + {{c1:: 只会渲染数组中最后一个被浏览器支持的值}}
