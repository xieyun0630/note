### 通配符选择器 [ ](css_20200722073620457)

```css
/* 设置所有的元素为红色 */
* {
  color: red;
}
```

### 快速生成 HTML 结构语法 [ ](css_20200722073620459)

1. **生成标签**：{{c1::  直接输入标签名 按 tab 键即可 比如 div 然后 tab 键， 就可以生成 `<div></div>` }}
2. **生成多个相同标签**：{{c1::  加上 * 就可以了 比如 div*3 就可以快速生成 3 个 div }}
3. **父子级关系**：{{c1:: 的标签，可以用 > 比如 ul > li 就可以了 }}
4. **兄弟关系的**：{{c1:: 标签，用 + 就可以了 比如 div+p }}
5. **生成带有类名或者 id**：{{c1:: 名字的， 直接写 .demo 或者 #two tab 键就可以了 }}
6. **生成的 div 类名是有顺序的**：{{c1:: ， 可以用 自增符号 \$ }}
7. **想要在生成的标签内部写内容**：{{c1:: 可以用 { } 表示 }}
8. **w200 按 tab**：{{c1::  可以 生成 width: 200px; }}
9. **lh26px 按 tab**：{{c1::  可以生成 line-height: 26px;  }}

### 字体属性的简写方式 [ ](css_20200722073620461)

- 下面属性的简写方式：
  - `font-style: italic;`
  - `font-weight: 700;`
  - `font-size: 16px;`
  - `font-family: 'Microsoft yahei';`
- 简写方式：{{c1:: `font: italic 700 16px 'Microsoft yahei';` }}
- 最少简写：{{c1:: `font: 16px 'Microsoft yahei'` }}

### 外观属性： [ ](css_20200722073620463)

- 颜色:{{c1:: `color: rgb(255, 0, 255);` }}
- 文字对齐:{{c1:: `text-align: right;` }}
- 装饰文本:
  1. 删除线:{{c1:: `text-decoration: line-through;` }}
  2. 上划线:{{c1:: `text-decoration: overline;` }}
  3. 取消`<a>`默认的下划线:{{c1:: `text-decoration: none;` }}
- 文本缩进:{{c1:: `text-indent: 2em;  ` }}
- 行间距:{{c1:: `line-height: 12px;` }}

### CSS 的复合选择器 [ ](css_20200722073620464)

- 后代选择器：{{c1:: 符号是`空格` 例：`.nav a` }}
- 子代选择器：{{c1:: 符号是`>` 例：`.nav>p` }}
- 并集选择器：{{c1:: 符号是`,` 例：`.nav,.header` }}
- 链接伪类：
  1. {{c1:: `a:link` }}
  2. {{c1:: `a:visited` }}
  3. {{c1:: `a:hover` }}
  4. {{c1:: `a:active` }}
- 焦点伪类：{{c1:: `input:focus` }}

### 外部样式表声明 [ ](css_20200722073620466)

```xml
<!-- {{c1:: -->
 <link rel="stylesheet" href="style.css">
 <!-- }} -->
```

### 元素显示模式总结 [ ](css_20200722073620467)

| 元素模式   | 元素排列                | 设置样式                    | 默认宽度                 | 包含                        |
| ---------- | ----------------------- | --------------------------- | ------------------------ | --------------------------- |
| 块级元素   | {{c1:: 一行只能放一个}} | {{c1:: 可以设置宽度高度  }} | {{c1:: 容器的%100    }}  | {{c1:: 任何标签        }}   |
| 行内元素   | {{c1:: 一行可以放多  }} | {{c1:: 不可以设置宽度高度}} | {{c1:: 本身内容的宽度 }} | {{c1:: 文本或其他行内元素}} |
| 行内块元素 | {{c1:: 一行可以放多个}} | {{c1:: 可以设置宽度与高度}} | {{c1:: 本身内容的宽度 }} |                             |

### 元素显示模式的转换 [ ](css_20200722073620469)

- 转换为块元素：{{c1:: `display:block;`}}
- 转换为行内元素：{{c1:: `display:inline;`}}
- 转换为行内块：{{c1:: `display: inline-block;`}}

### css 实现小米侧边栏效果 [ ](css_20200722073620471)

- ![image-20200722145047450](css.assets/image-20200722145047450.png)
- CSS 主要代码：
  ```css
  /* {{c1:: */
  a {
    display: block;
    width: 230px;
    height: 40px;
    background-color: #55585a;
    font-size: 14px;
    color: #fff;
    text-decoration: none;
    text-indent: 2em;
    line-height: 40px;
  }
  a:hover {
    background-color: #ff6700;
  }
  /* }} */
  ```

### 背景 [ ](css_20200722073620473)

- 背景颜色：{{c1:: `background-color: pink;`}}
- 背景图片：{{c1:: `background-image: url(images/logo.png);`}}
- 背景平铺
  1. 背景图片不平铺:{{c1:: `background-repeat: no-repeat;`}}
  2. 默认的情况下,背景图片是平铺的:{{c1:: `background-repeat: repeat;`}}
  3. 沿着 x 轴平铺:{{c1:: `background-repeat: repeat-x;`}}
  4. 沿着 Y 轴平铺:{{c1:: `background-repeat: repeat-y;`}}
- 背景图像位置:
  - 语法： {{c1:: `background-position: x y;` }}
  - 参数代表意思：
    - 数值:{{c1:: 百分比/像素 }}
    - 方位名词: {{c1:: `top | center | bottom | left | center | right` 方位 }}
- 背景图像固定：{{c1:: `background-attachment : scroll | fixed`}}
- 背景属性复合写法: {{c1:: `background: black url(images/bg.jpg) no-repeat fixed center top;` }}
  - 注意：没有固定的顺序
- 背景颜色半透明：{{c1:: `background: rgba(0, 0, 0, .3);`}}

### CSS 背景使用综合案例：五彩导航 [ ](css_20200722073620475)

- 效果：![image-20200722164346692](css.assets/image-20200722164346692.png)
- 主要 CSS 代码：
  ```css
  /*{{c1::*/
  .nav a {
    display: inline-block;
    width: 120px;
    height: 58px;
    background-color: pink;
    text-align: center;
    line-height: 48px;
    color: #fff;
    text-decoration: none;
  }
  .nav .bg1 {
    background: url(images/bg1.png) no-repeat;
  }
  .nav .bg1:hover {
    background-image: url(images/bg11.png);
  }
  .nav .bg2 {
    background: url(images/bg2.png) no-repeat;
  }
  .nav .bg2:hover {
    background-image: url(images/bg22.png);
  }
  /* }} */
  ```

### CSS 的三大特性 [ ](css_20200722073620476)

1. 层叠性：
   1. 冲突：{{c1:: 就近原则，那个样式离结构近，就用哪个}}
   2. 不冲突：{{c1:: 不会层叠}}
2. 继承性： {{c1:: 子标签会继承父标签的某些样式，主要`text- font- line- color`}}
   1. 设置子元素的行高倍数：{{c1:: `font: 12px/1.5 'Microsoft YaHei';`}}
3. 优先性（根据权重）： `继承 或 *`  <`元素选择器` < `类选择器，伪类选择器` < `ID 选择器` < `行内样式` < `!important;`


### CSS 6种权重

 1. 继承 或 `*` :{{c1:: `0,0,0,0` }}
 2. 元素选择器:{{c1:: `0,0,0,1` }}
 3. 类选择器，伪类选择器:{{c1:: `0,0,1,0` }}
 4. ID 选择器：`0,1,0,0`
 5. 行内样式:{{c1:: `1,0,0,0` }}
 6. !important;:{{c1:: `无穷大` }}
- 注意：
  - {{c1:: 继承的样式的权重永远为 0}}
  - {{c1:: 权重叠加：复合选择器会权重叠加，但不会进位}}

### 盒子模型 [ ](css_20200722073620478)

- 边框 border
  - 语法：{{c1:: `border : border-width || border-style || border-color` }}
    - border-style 常用值：{{c1:: `none` `solid` `dashed` `dotted` }}
- 盒子模型组成图
  - {{c1:: ![image-20200722193002516](css.assets/image-20200722193002516.png) }}


### 通配符选择器 [ ](css_20200722073620457)
```css
/* {{c1:: */
/* 设置所有的元素为红色 */
* {
  color: red;
}
/* }} */
```

### 快速生成 HTML 结构语法 [ ](css_20200722073620459)

1. **生成标签**：{{c1::  直接输入标签名 按 tab 键即可 比如 div 然后 tab 键， 就可以生成 `<div></div>` }}
2. **生成多个相同标签**：{{c1::  加上 * 就可以了 比如 div*3 就可以快速生成 3 个 div }}
3. **父子级关系**：{{c1:: 的标签，可以用 > 比如 ul > li 就可以了 }}
4. **兄弟关系的**：{{c1:: 标签，用 + 就可以了 比如 div+p }}
5. **生成带有类名或者 id**：{{c1:: 名字的， 直接写 .demo 或者 #two tab 键就可以了 }}
6. **生成的 div 类名是有顺序的**：{{c1:: ， 可以用 自增符号 \$ }}
7. **想要在生成的标签内部写内容**：{{c1:: 可以用 { } 表示 }}
8. **w200 按 tab**：{{c1::  可以 生成 width: 200px; }}
9. **lh26px 按 tab**：{{c1::  可以生成 line-height: 26px;  }}

### 字体属性的简写方式 [ ](css_20200722073620461)

- 下面属性的简写方式：
  - `font-style: italic;`
  - `font-weight: 700;`
  - `font-size: 16px;`
  - `font-family: 'Microsoft yahei';`
- 简写方式：{{c1:: `font: italic 700 16px 'Microsoft yahei';` }}
- 最少简写：{{c1:: `font: 16px 'Microsoft yahei'` }}

### 外观属性： [ ](css_20200722073620463) 

- 颜色:{{c1:: `color: rgb(255, 0, 255);` }}
- 文字对齐:{{c1:: `text-align: right;` }}
- 装饰文本:
  1. 删除线:{{c1:: `text-decoration: line-through;` }}
  2. 上划线:{{c1:: `text-decoration: overline;` }}
  3. 取消`<a>`默认的下划线:{{c1:: `text-decoration: none;` }}
- 文本缩进:{{c1:: `text-indent: 2em;  ` }}
- 行间距:{{c1:: `line-height: 12px;` }}

### CSS 的复合选择器 [ ](css_20200722073620464)

- 后代选择器：{{c1:: 符号是`空格` 例：`.nav a` }}
- 子代选择器：{{c1:: 符号是`>` 例：`.nav>p` }}
- 并集选择器：{{c1:: 符号是`,` 例：`.nav,.header` }}
- 链接伪类：
  1. {{c1:: `a:link` }}
  2. {{c1:: `a:visited` }}
  3. {{c1:: `a:hover` }}
  4. {{c1:: `a:active` }}
- 焦点伪类：{{c1:: `input:focus` }}

### 外部样式表声明 [ ](css_20200722073620466) 

```xml
<!-- {{c1:: -->
 <link rel="stylesheet" href="style.css">
 <!-- }} -->
```

### 元素显示模式总结 [ ](css_20200722073620467) 

| 元素模式   | 元素排列                | 宽高设置                    | 默认宽度                 | 包含                        |
| ---------- | ----------------------- | --------------------------- | ------------------------ | --------------------------- |
| 块级元素   | {{c1:: 一行只能放一个}} | {{c1:: 可以设置宽度高度  }} | {{c1:: 容器的%100    }}  | {{c1:: 任何标签        }}   |
| 行内元素   | {{c1:: 一行可以放多  }} | {{c1:: 不可以设置宽度高度}} | {{c1:: 本身内容的宽度 }} | {{c1:: 文本或其他行内元素}} |
| 行内块元素 | {{c1:: 一行可以放多个}} | {{c1:: 可以设置宽度与高度}} | {{c1:: 本身内容的宽度 }} |                             |

### 元素显示模式的转换 [ ](css_20200722073620469) 

- 转换为块元素：{{c1:: `display:block;`}}
- 转换为行内元素：{{c1:: `display:inline;`}}
- 转换为行内块：{{c1:: `display: inline-block;`}}

### css 实现小米侧边栏效果 [ ](css_20200722073620471) 

- ![image-20200722145047450](css.assets/image-20200722145047450.png)
- CSS 主要代码：
  ```css
  /* {{c1:: */
  a {
    display: block;
    width: 230px;
    height: 40px;
    background-color: #55585a;
    font-size: 14px;
    color: #fff;
    text-decoration: none;
    text-indent: 2em;
    line-height: 40px;
  }
  a:hover {
    background-color: #ff6700;
  }
  /* }} */
  ```

### 背景 [ ](css_20200722073620473)

- 背景颜色：{{c1:: `background-color: pink;`}}
- 背景图片：{{c1:: `background-image: url(images/logo.png);`}}
- 背景平铺
  1. 背景图片不平铺:{{c1:: `background-repeat: no-repeat;`}}
  2. 默认的情况下,背景图片是平铺的:{{c1:: `background-repeat: repeat;`}}
  3. 沿着 x 轴平铺:{{c1:: `background-repeat: repeat-x;`}}
  4. 沿着 Y 轴平铺:{{c1:: `background-repeat: repeat-y;`}}
- 背景图像位置:
  - 语法： {{c1:: `background-position: x y;` }}
  - 参数代表意思：
    - 数值:{{c1:: 百分比/像素 }}
    - 方位名词: {{c1:: `top | center | bottom | left | center | right` 方位 }}
- 背景图像固定：{{c1:: `background-attachment : scroll | fixed`}}
- 背景属性复合写法: {{c1:: `background: black url(images/bg.jpg) no-repeat fixed center top;` }}
  - 注意：没有固定的顺序
- 背景颜色半透明：{{c1:: `background: rgba(0, 0, 0, .3);`}}

### CSS 背景使用综合案例：五彩导航 [ ](css_20200722073620475)

- 效果：![image-20200722164346692](css.assets/image-20200722164346692.png)
- 主要 CSS 代码：
  ```css
  /*{{c1::*/
  .nav a {
    display: inline-block;
    width: 120px;
    height: 58px;
    background-color: pink;
    text-align: center;
    line-height: 48px;
    color: #fff;
    text-decoration: none;
  }
  .nav .bg1 {
    background: url(images/bg1.png) no-repeat;
  }
  .nav .bg1:hover {
    background-image: url(images/bg11.png);
  }
  .nav .bg2 {
    background: url(images/bg2.png) no-repeat;
  }
  .nav .bg2:hover {
    background-image: url(images/bg22.png);
  }
  /* }} */
  ```

### CSS 的三大特性 [ ](css_20200722073620476) 

1. 层叠性：
   1. 冲突：{{c1:: 就近原则，那个样式离结构近，就用哪个}}
   2. 不冲突：{{c1:: 不会层叠}}
2. 继承性： {{c1:: 子标签会继承父标签的某些样式，主要`text- font- line- color`}}
   1. 设置子元素的行高倍数：{{c1:: `font: 12px/1.5 'Microsoft YaHei';`}}
3. 优先性：
   1. 继承 或 `*` :{{c1:: `0,0,0,0` }}
   2. 元素选择器:{{c1:: `0,0,0,1` }}
   3. 类选择器，伪类选择器:{{c1:: `0,0,1,0` }}
   4. ID 选择器：`0,1,0,0`
   5. 行内样式:{{c1:: `1,0,0,0` }}
   6. !important;:{{c1:: `无穷大` }}

- 注意：
  - {{c1:: 继承的样式的权重永远为 0}}
  - {{c1:: 权重叠加：复合选择器会权重叠加，但不会进位}}

### 盒子模型 [ ](css_20200722073620478) 

- 边框 border
  - 语法：{{c1:: `border : border-width || border-style || border-color` }}
    - border-style 常用值：{{c1:: `none` `solid` `dashed` `dotted` }}
- 盒子模型组成图
  - {{c1:: ![image-20200722193002516](css.assets/image-20200722193002516.png) }}

### 边框(border) [	](css_20200813094652545)
+ 语法：{{c1:: `border : border-width || border-style || border-color` }}
  + 边框样式可以设置如下值：
    + {{c1:: `none`：没有边框即忽略所有边框的宽度（默认值） }}
    + {{c1:: `solid`：边框为单实线(最为常用的)  }}
    + {{c1:: `dashed`：边框为虚线  }}
    + {{c1:: `dotted`：边框为点线 }}
+ 分开写法：
  1. {{c1:: `border-top: 5px solid pink;` }}
  2. {{c1:: `border-bottom: 10px dashed purple;` }}
  3. {{c1:: `border-left: 5px solid pink;` }}
  4. {{c1:: `border-right: 5px solid pink;` }}

### 控制表格中盒子的边框 [	](css_20200813094652547)

+ 合并表格中盒子的相邻边框：{{c1:: `border-collapse:collapse;`}}
+ 指定表格相邻边框的距离：{{c1:: `<table cellspacing="22"> ...`}}

### 内边距(padding)与外边距(margin) [	](css_20200813094652549)

+ `padding`与`margin`的写法基本一致。
+ 语法：`padding: 上 右 下 左`
+ 4种复合写法(重要)：
  1. {{c1::`padding: 5px`: 上右下左都是4}}
  2. {{c1::`padding: 5px 10px`:  上下:5px,左右：10px}}
  3. {{c1::`padding: 5px 10px 20px`: 上：5px,左右：10px,下：20px}}
  4. {{c1::`padding: 5px 10px 20px 30px`: 上：5px 右：10px 下：20px 左：30px}}
+ 分开写法：
  1. {{c1:: `padding-left : 1px ` }}
  2. {{c1:: `padding-right : 1px ` }}
  3. {{c1:: `padding-top : 1px ` }}
  4. {{c1:: `padding-bottom : 1px ` }}

### 给盒子指定`padding`的影响： [	](css_20200813094652551)

1. {{c1:: 内容和边框有了距离，添加了内边距。 }}
2. {{c1:: 如果盒子已经有了宽度和高度，此时再指定内边框，会撑大盒子。 }}
+ 好处：如果导航栏里面的字数不一样多,可以不用给每个盒子宽度了,直接给padding最合适.
  + 例子图：{{c1::![image-20200807230745979](css.assets/image-20200807230745979.png)}}

### 设置外边距使块级元素水平居中 [	](css_20200813094652553)

+ 必要条件：
  1. {{c1:: 盒子必须指定了宽度（width）。 }}
  2. {{c1:: 盒子左右的外边距都设置为 auto 。 }}
+ 常见写法：
  1. {{c1:: `margin-left: auto; margin-right: auto;` }}
  2. {{c1:: `margin: auto;` }}
  3. {{c1:: `margin: 0 auto;` }}
注意：{{c1:: 行内元素或者行内块元素水平居中给其父元素添加 `text-align:center` 即可。 }}

### 外边距合并 [	](css_20200813094652556)
1. 相邻块元素垂直外边距的合并(图)
  + ![image-20200808010026078](css.assets/image-20200808010026078.png)
  + 解决方法：{{c1:: 尽量只给一个盒子添加 margin 值 }}
2. 嵌套块元素垂直外边距的塌陷(图)
  + ![image-20200808010036816](css.assets/image-20200808010036816.png)
  + 解决方法：
    1. {{c1::可以为父元素定义上边框。 }}
    2. {{c1::可以为父元素定义上内边距。 }}
    3. {{c1::可以为父元素添加 overflow:hidden。 }}

### 清除浏览器默认内外边距 [	](css_20200813094652558)

```css
  /* {{c1:: */
  * {
  padding:0; /* 清除内边距 */
  margin:0; /* 清除外边距 */
  }
  /* }} */
```
### 去掉 li 前面的 项目符号(小圆点) [	](css_20200813094652561)

+ 语法 ：{{c1::`list-style: none;`}}

### CSS3圆角边框 [	](css_20200813094652563)

+ 语法：`border-radius:length;`
+ 4种复合写法(重要)：
  1. {{c1::`border-radius: 5px`: 上右下左都是4}}
  2. {{c1::`border-radius: 5px 10px`:  上下:5px,左右：10px}}
  3. {{c1::`border-radius: 5px 10px 20px`: 上：5px,左右：10px,下：20px}}
  4. {{c1::`border-radius: 5px 10px 20px 30px`: 上：5px 右：10px 下：20px 左：30px}}
+ 分开写法：
  1. {{c1:: `border-top-left-radius` }}
  2. {{c1:: `border-top-right-radius` }}
  3. {{c1:: `border-bottom-right-radius` }}
  4. {{c1:: `border-bottom-left-radius` }}

### 阴影 [	](css_20200813094652565)

+ 盒子阴影：
  + 语法：{{c1:: `box-shadow: h-shadow v-shadow blur spread color inset;` }}
  + 解释图：{{c1::![image-20200808011258490](css.assets/image-20200808011258490.png)}}
+ 文字阴影：
  + 语法：{{c1:: `text-shadow: h-shadow v-shadow blur color;` }}

### 传统网页布局的三种方式 [	](css_20200813094652569)

+ {{c1:: 普通流（标准流） }}
+ {{c1:: 浮动 }}
+ {{c1:: 定位 }}

### 浮动(float) [	](css_20200813094652571)

+ 什么是浮动：{{c1:: 浮动盒子将移动到左/右边，直到盒子的左/右边缘接触到包含块或者另一个浮动盒子的边缘。}}
+ 网页布局第一准则：{{c1:: 多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动。}}
+ 语法：{{c1:: `float:none/left/right` }}

### 浮动特性 [	](css_20200813094652573)

+ 脱标：
  1. {{c1:: 脱离标准普通流的控制（浮）移动到指定位置（动）}}
  2. {{c1:: 浮动的盒子不在保留原先的位置}}
+ 同一行浮动元素：
  + {{c1:: 顶部对齐}}
  + {{c1:: 浮动的元素是互相贴靠在一起的（不会有缝隙），如果父级宽度装不下这些浮动的盒子， 多出的盒子会另起一行对齐。}}
+ 浮动元素具有行内块元素的特性:
  + {{c1:: 不需要转换块级\行内块元素就可以直接给高度和宽度}}
+ 注意：{{c1:: 浮动元素的兄弟元素也要是浮动元素，以防引起问题。 }}


### 清除浮动： [	](css_20200813094652576)

+ 为什么需要清除浮动(图)？：{{c1:: ![image-20200809015603618](css.assets/image-20200809015603618.png) }}
+ 清除浮动方法:
  + 额外标签法:{{c1:: 在浮动元素末尾添加一个**空的块级元素**。例如 `<div style=”clear:both”></div>`}}
  + 父级添加:{{c1:: `overflow: hidden;` }}
+  伪元素法（了解）:
    1. {{c1:: 单伪元素,代表网站：小米、腾讯等 }}
    2. {{c1:: 双伪元素,代表网站： 百度、淘宝网、网易等 }}

### css定位
+ 定位 = 定位模式 + 边偏移 
+ 定位模式:{{c1:: `static` `relative` `absolute` `fixed`}}
+ 边偏移:{{c1:: `top` `bottom` `left` `right`}}

### 静态定位 static
+ 静态定位是元素的默认定位方式，无定位的意思
+ 语法：`选择器 { position: static; }`
+ 注意：静态定位按照标准流特性摆放位置，它没有边偏移

### 相对定位 relative


### 相对定位 VS 绝对定位

+ 相对定位的特点：
  1. {{c1:: 它是相对于自己原来的位置来移动的（移动位置的时候参照点是自己原来的位置）。}}
  2. {{c1:: 原来在标准流的位置继续占有，后面的盒子仍然以标准流的方式对待它（不脱标）。}}
+ 绝对定位的特点：
  1. {{c1:: 如果没有祖先元素或者祖先元素没有定位，则以浏览器为准定位（Document 文档）。}}
  2. {{c1:: 如果祖先元素有定位（相对、绝对、固定定位），则以最近一级的有定位祖先元素为参考点移动位置。}}
  3. {{c1:: 绝对定位不再占有原先的位置。（脱标）}}
  4. 子绝父相的由来:{{c1:: 因为父级需要占有位置，因此是相对定位，子盒子 不需要占有位置，则是绝对定位}}
+ 固定定位的特点：
  1. {{c1:: 以浏览器的可视窗口为参照点移动元素。  }}
    + {{c1:: 跟父元素没有任何关系 }}
    + {{c1:: 不随滚动条滚动。 }}
  2. {{c1:: 固定定位不占有原先的位置。 }}

### 固定定位小技巧： 固定在版心右侧位置
1. {{c1:: 让固定定位的盒子 left: 50%. 走到浏览器可视区（也可以看做版心） 的一半位置。}}
2. {{c1:: 让固定定位的盒子 margin-left: 版心宽度的一半距离。 多走 版心宽度的一半位置}}

### 粘性定位 sticky
+ 语法：{{c1:: `选择器 { position: sticky; top: 10px; }` }}
粘性定位的特点：
1. {{c1:: 以浏览器的可视窗口为参照点移动元素（固定定位特点） }}
2. {{c1:: 粘性定位占有原先的位置（相对定位特点） }}
3. {{c1:: 必须添加 top 、left、right、bottom 其中一个才有效 }}

### 定位总结

| 定位模式          | 是否脱标                  | 移动位置                    | 是否常用            |
| ----------------- | ------------------------- | --------------------------- | ------------------- |
| static 静态定位   | {{c1:: 否              }} | {{c1:: 不能使用边偏移    }} | {{c1:: 很少      }} |
| relative 相对定位 | {{c1:: 否 (占有位置)   }} | {{c1:: 相对于自身位置移动}} | {{c1:: 常用      }} |
| absolute绝对定位  | {{c1:: 是（不占有位置）}} | {{c1:: 带有定位的父级    }} | {{c1:: 常用      }} |
| fixed 固定定位    | {{c1:: 是（不占有位置）}} | {{c1:: 浏览器可视区      }} | {{c1:: 常用      }} |
| sticky 粘性定位   | {{c1:: 否 (占有位置)   }} | {{c1:: 浏览器可视区      }} | {{c1:: 当前阶段少}} |

 ### 定位叠放次序

+ 语法:选择器 { z-index: 1; }
+ 要注意的点：
  1. 取值范围：{{c1:: 是正整数、负整数或 0, 默认是 auto，数值越大，盒子越靠上 }}
  2. 如果属性值相同：{{c1:: 则按照书写顺序，后来居上 }}
  3. 无单位：{{c1:: 数字后面不能加单位 }}
  4. 存在必要条件：{{c1:: 只有定位的盒子才有 z-index 属性 }}

### 绝对定位的盒子居中方法

+ 原因：加了绝对定位的盒子不能通过 margin:0 auto 水平居中
+ 解决方法：
 1. {{c1:: left: 50%;：让盒子的左侧移动到父级元素的水平中心位置。 }}
 2. {{c1:: margin-left: -100px;：让盒子向左移动自身宽度的一半。}}

### 元素的显示与隐藏
1. `display`作用:{{c1:: 显示隐藏元素 但是不保留位置 }}
  + 常用值：{{c1:: `none` `block` }}
2. `visibility`作用:{{c1:: 显示隐藏元素 但是保留原来的位置 }}
  + 常用值：{{c1:: `visible` `hidden` }}
3. `overflow`作用:{{c1:: 溢出显示隐藏 但是只是对于溢出的部分处理 }}
  + 常用值：{{c1:: `visible` `hidden` `scroll` `auto` }}

## HTML5 与 CSS3 新特性

### HTML5 新增的语义化标签

+ `<header>`：{{c1:: 头部标签 }}
+ `<nav>`：{{c1:: 导航标签 }}
+ `<article>`：{{c1:: 内容标签 }}
+ `<section>`：{{c1:: 定义文档某个区域 }}
+ `<aside>`：{{c1:: 侧边栏标签 }}
+ `<footer>`：{{c1:: 尾部标签 }}
+ 注意：
  + 搜索引擎:{{c1:: 这种语义化标准主要是针对搜索引擎的  }}
  + 使用多次:{{c1:: 这些新标签页面中可以使用多次 }}
  + IE9兼容问题:{{c1:: 需要把这些元素转换为块级元素 }}
+ 图：{{c1:: ![image-20200819222058165](css.assets/image-20200819222058165.png) }}

### HTML5 视频`<video>`与音频`<audio>`使用语法
1. 视频:
  ```html
  <!-- {{c1:: -->
    <video width="320" height="240" controls>
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.ogg" type="video/ogg">
    您的浏览器不支持 HTML5 video 标签。
    </video>
  <!-- }} -->
  ```
2. 音频:
  ```html
  <!-- {{c1:: -->
    <audio controls="controls">
    <source src="happy.mp3" type="audio/mpeg">
    <source src="happy.ogg" type="audio/ogg">
    您的浏览器暂不支持<audio>标签。
    </audio>
  <!-- }} -->
  ```
### HTML5视频`<video>`——常见属性

| 属性      | 值                 | 描述                                                         |
| :-------- | :----------------- | :----------------------------------------------------------- |
| autoplay | {{c1:: autoplay }} | {{c1::如果出现该属性，则视频在就绪后马上播放。                    }} |
| controls | {{c1:: controls }} | {{c1::如果出现该属性，则向用户显示控件，比如播放按钮。            }} |
| width     | {{c1:: *pixels* }} | {{c1::设置视频播放器的宽度。                                      }} |
| height    | {{c1:: *pixels* }} | {{c1::设置视频播放器的高度。                                      }} |
| loop      | {{c1:: loop     }} | {{c1::如果出现该属性，则当媒介文件完成播放后再次开始播放。        }} |
| preload   | {{c1:: auto/none  }} | {{c1::如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。}} |
| src       | {{c1:: *url*    }} | {{c1::要播放的视频的 URL。                                        }} |
| poster       | {{c1:: *imgurl*    }} | {{c1::加载等待的画面图片                                    }} |
| muted       | {{c1:: *muted*    }} | {{c1::静音播放                                    }} |

### HTML5音频`<audio>`——常见属性

| 属性      | 值                 | 描述                                                         |
| :-------- | :----------------- | :----------------------------------------------------------- |
| src       | {{c1:: *url*    }} | {{c1::要播放的视频的 URL。                                        }} |
| autoplay | {{c1:: autoplay }} | {{c1::如果出现该属性，则视频在就绪后马上播放。                    }} |
| controls | {{c1:: controls }} | {{c1::如果出现该属性，则向用户显示控件，比如播放按钮。            }} |
| loop      | {{c1:: loop     }} | {{c1::如果出现该属性，则当媒介文件完成播放后再次开始播放。        }} |
| src       | {{c1:: *url*    }} | {{c1::要播放的视频的 URL。                                        }} |


### HTML5新添加的表单属性

+ 属性：
  + `requried`:{{c1:: 必填 }}
  + `placeholder`:{{c1:: 提示文本 }}
  + `autofocus`:{{c1:: 自动聚焦到指定表单 }}
  + `autocomplete`:{{c1:: off/on,浏览器基于之前填入过的值自动填入 }}
  + `multiple`:{{c1:: 可以多选文件提交 }}
+ 可以通过以下设置方式修改placeholder里面的字体颜色：
  ```css
  /* {{c1:: */
    input::placeholder {
    color: pink;
    }
  /* }} */
  ```

### CSS3 新增选择器:属性选择器

+ `E[att]`:{{c1:: 匹配**具有**属性attr的元素 }}
+ `E[att="val"]`:{{c1:: 匹配属性**等于**val的元素 }}
+ `E[att^="val"]`:{{c1:: 匹配属性以val**开头**的元素 }}
+ `E[att$="val"]`:{{c1:: 匹配属性以val**结尾**的元素 }}
+ `E[att*="val"]`:{{c1:: 匹配属性**包含**val字符串的元素 }}
+ 匹配多属性：{{c1:: `E[att1="val"][att2="val"]`}}
+ 权重：{{c1:: 类选择器、属性选择器、伪类选择器，权重为 10。 }}

### CSS3 新增选择器:结构伪类选择器

  + `E:first-child`:{{c1:: 匹配父元素中的第一个子元素E }}
  + `E:last-child`:{{c1:: 匹配父元素中最后一个E元素 }}
  + `E:nth-child(n)`:{{c1:: 匹配父元素中的第n个子元素E }}
  + `E:first-of-type`:{{c1:: 指定类型E的第一个 }}
  + `E:last-of-type`:{{c1:: 指定类型E的最后一个 }}
  + `E:nth-of-type(n)`:{{c1:: 指定类型E的第n个 }}
+ 权重：{{c1:: 类选择器、属性选择器、伪类选择器，权重为 10。 }}

### `nth-child（n）`选择器的使用技巧

+ n 可以是数字，关键字和公式
  + 数字: {{c1:: 选择第n个子元素 }}
  + 关键字：{{c1:: even 偶数，odd 奇数 }}
  + 公式：常见的公式如下
    + 偶数：{{c1:: `nth-child(2n)` }}
    + 奇数：{{c1:: `nth-child(2n+1)` }}
    + 5 10 15：{{c1:: `nth-child(5n)` }}
    + 从第五个元素开始：{{c1:: `nth-child(n+5)` }}
    + 选择前五个元素：{{c1:: `nth-child(-n+5)` }}

### CSS3 新增选择器:伪元素选择器

+ 作用：{{c1:: 利用CSS创建新标签**行内**元素，而不需要HTML标签，从而简化HTML结构。 }}
+ 选择符：
  + `::before`:{{c1:: 在元素内部的**前面**插入内容 }}
  + `::after`:{{c1:: 在元素内部的**后面**插入内容 }}
+ 权重：{{c1:: 伪元素选择器和标签选择器一样，权重为 1 }}
+ 语法： {{c1:: `element::before {}` }}
+ before 和 after 必须有 {{c1:: **content属性** }}

### 伪元素选择器使用场景3：伪元素清除浮动
+ 单伪元素清除浮动
  ```css
    /* {{c1:: */
    .clearfix:after {
      content: "";
      display: block;
      height: 0;
      clear: both;
      visibility: hidden;
    } 
    /* }} */
  ```
+ 双伪元素清除浮动
  ```css
    /* {{c1:: */
    .clearfix:before,.clearfix:after {
      content:"";
      display:table;
    }
    .clearfix:after {
      clear:both;
    }
    /* }} */
  ```

### CSS3 盒子模型
+ 可以分成两种情况：
  1. {{c1:: `box-sizing: content-box` 盒子大小为 width + padding + border （以前默认的） }}
  2. {{c1:: `box-sizing: border-box` 盒子大小为 width,  }}
区别：{{c1:: padding与border一个是撑大盒子，一个是挤压content盒子。 }}

### CSS3 滤镜与`calc()`

+ CSS3滤镜模糊处理:{{c1:: `filter: blur(5px); ` }}
+ `calc()函数`:{{c1:: `width: calc(100% - 80px);`括号里面可以使用 + - * / 来进行计算。 }}

###  CSS3 过渡

+ 语法： `transition: 要过渡的属性 花费时间 [运动曲线] [何时开始];`
1. 属性 ：{{c1::  想要变化的 css 属性， 宽度高度 背景颜色 内外边距都可以 。如果想要所有的属性都变化过渡， 写一个all 就可以。}}
2. 花费时间：{{c1::  单位是 秒（必须写单位） 比如 0.5s}}
3. 运动曲线：{{c1::  默认是 ease （可以省略）}}
4. 何时开始 ：{{c1:: 单位是 秒（必须写单位）可以设置延迟触发时间 默认是 0s （可以省略）}}
+ 使用口诀： 谁做过渡给谁加
+ 分开写语法：
  + {{c1:: `transition-property` }}
  + {{c1:: `transition-duration` }}
  + {{c1:: `transition-timing-function` }}
  + {{c1:: `transition-delay` }}

### 2D 转换之移动 translate
+ 语法:
  1. `transform: translate(x,y);`
  2. `transform: translateX(n);`
  3. `transform: translateY(n);`
+ 注意点：
  1. translate最大的优点：{{c1:: 不会影响到其他元素的位置 }}
  2. 百分比单位:{{c1:: translate中的百分比单位是相对于自身元素的 translate:(50%,50%); }}
  3. 行内标签:{{c1:: 对行内标签没有效果 }}
  

 ### 2D 转换之旋转 rotate
+ 语法：`transform:rotate(度数)`
+ 重点：
  + 跟度数：{{c1:: rotate里面跟度数， 单位是 deg 比如 rotate(45deg) }}
  + 正负值：{{c1:: 角度为正时，顺时针，负时，为逆时针 }}
  + 默认旋转的中心点:{{c1:: 是元素的中心点 }}
  + 中心点设置：{{c1:: transform-origin: x y; }}

### 2D 转换之旋转 rotate：使用盒子实现三角形
+ 效果图：![image-20200821162510182](css.assets/image-20200821162510182.png)
+ 实现：
  ```css
  /* {{c1:: */
    p::before {
      content: '';
      position: absolute;
      right: 20px;
      top: 10px;
      width: 10px;
      height: 10px;
      border-right: 1px solid #000;
      border-bottom: 1px solid #000;
      transform: rotate(45deg);
    }
  /* }} */
  ```
### 2D 转换之缩放scale
+ 4种语法：
  + `transform:scale(1,1) `：{{c1:: 宽和高都放大一倍，相对于没有放大}}
  + `transform:scale(2,2) `：{{c1:: 宽和高都放大了2倍}}
  + `transform:scale(2) `：{{c1:: 只写一个参数，第二个参数则和第一个参数一样，相当于 }}scale(2,2)
  + `transform:scale(0.5,0.5)`：{{c1:: 缩小}}
+ 中心点设置：{{c1:: transform-origin: x y; }}

### 2D 转换综合写法

+ 格式为：{{c1:: `transform: translate() rotate() scale() ..` }}
+ 注意：{{c1:: 记得要将位移放到最前 }}

### CSS动画

1. 定义动画:
  ```css
  /* {{c1:: */
    @keyframes 动画名称 {
        0%{
          width:100px;
        }
        100%{
          width:200px;
        }
    }
  /* }} */
  ```
2. 声明使用：`animation: name duration timing-function delay iteration-count direction fill-mode;`
   + 各属性常见取值：
     + timing-function：{{c1:: 速度曲线 }}
     + delay：{{c1:: 什么时候开始 }}
     + iteration-count：{{c1:: 1/infinite }}
     + direction：{{c1:: normal/reverse }}
     + fill-mode：{{c1:: forwards/backwards 指定结束的状态 }}

### CSS过渡与动画的常见速度曲线函数

+ `linear`：{{c1:: 动画从头到尾的速度是相同的。匀速 }}
+ `ease`：{{c1:: 默认。动画以低速开始，然后加快，在结束前变慢。 }}
+ `ease-in`：{{c1:: 动画以低速开始。  }}
+ `ease-out`：{{c1:: 动画以低速结束。 }}
+ `ease-in-out`：{{c1:: 动画以低速开始和结束。  }}
+ `steps()`：{{c1:: 指定了时间函数中的间隔数量（步长）  }}












### css3使用精灵图核心总结：

1. {{c1:: 精灵图主要针对于小的背景图片使用。 }}
2. {{c1:: 主要借助于背景位置来实现---background-position 。 }}
3. {{c1:: 一般情况下精灵图都是负值。 }}

### 2个字体图标推荐下载网站：

1. 国外： {{c1:: http://icomoon.io  }}
2. 国内： {{c1:: http://www.iconfont.cn/  }}

### 字体图标的使用:

1. {{c1:: 下载字体文件夹 }}
2. {{c1:: 从文件夹复制字体声明：`@font-face {...}` }}
3. {{c1:: 使用图标的元素字体样式要与字体声明一致 }}
+ 注意图标codo使用转义：`&#xb1234`

### CSS画三角形
  ```css
      /* {{c1:: */
      border: 50px solid transparent;
      border-left-color: pink;
      /* }} */
  ```

### CSS 用户界面样式

+ 去掉表单默认的蓝色边框：{{c1:: `input {outline: none; }` 或 `input {outline: 0; }` }}
+ 防止拖拽文本域：{{c1::`textarea{ resize: none;}`}}
+ 鼠标样式
  + 默认:{{c1:: `cursor: default;` }}
  + 小手:{{c1:: `cursor: pointer;` }}
  + 移动:{{c1:: `cursor: move;` }}
  + 文本:{{c1:: `cursor: text;` }}
  + 禁止:{{c1:: `cursor: not-allowed;` }}

### vertical-align 属性应用

+ 语法：{{c1:: `vertical-align : baseline | top | middle | bottom ` }}
+ 作用：{{c1:: 用于设置图片或者表单(行内块元素）和文字垂直对齐 }}
+ 注意：
  1. {{c1:: 默认基线对齐 }}
  2. {{c1:: 是一行内的多个元素同时基于一种line对齐。 }}
+ 四种线图示：
  + {{c1:: ![image-20200821144121455](css.assets/image-20200821144121455.png) }}

### 解决图片底部默认空白缝隙问题

+ 主要解决方法有两种：
  1. {{c1:: 给图片添加 vertical-align:middle | top| bottom 等。 （提倡使用的） }}
  2. {{c1:: 把图片转换为块级元素 display: block; }}

### 溢出的文字省略号显示

+ 单行文本溢出显示省略号--必须满足三个条件
  1. 先强制一行内显示文本:{{c1::`white-space: nowrap; （ 默认 normal 自动换行）`}}
  2. 超出的部分隐藏:{{c1::`overflow: hidden;`}}
  3. 文字用省略号替代超出的部分:{{c1::`text-overflow: ellipsis;`}}
+ 多行文本溢出显示省略号:
  1. 超出的部分隐藏overflow:{{c1:: ` hidden;` }}
  2. 文字用省略号替代超出的部分:{{c1:: `text-overflow: ellipsis;` }}
  3. 弹性伸缩盒子模型显示:{{c1:: `display: -webkit-box;` }}
  4. 限制在一个块元素显示的文本的行数:{{c1:: `-webkit-line-clamp: 2;` }}
  5. 设置或检索伸缩盒对象的子元素的排列方式:{{c1:: `-webkit-box-orient: vertical;` }}
