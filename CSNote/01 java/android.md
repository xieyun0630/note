## 第二章 活动

### 活动
+ 定义：活动( Activity)是最容易吸引用户的地方，它是一种可以包含用户界面的组件，主要用于和用户进行交互。

### 手动创建活动过程

1. 创建`add no Activity` 空项目

2. 添加第一个Activity,注意不要生成layout，设置主Activity.

3. 在`app/src/main/res`下添加`layout/first_layout.xml`布局文件。

   ```xml
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:orientation="vertical" android:layout_width="match_parent"
       android:layout_height="match_parent">
       <Button
    android:id="@+id/start_normal_activity"
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:text="start normal activity" />
   </LinearLayout>
   ```

4. 在对应Activity中添加相应关联:
   ```java
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_test);
       ((Button) findViewById(R.id.start_normal_activity)).setOnClickListener(event ->{
           Intent intent = new Intent(ActivityTest.this, NormalActivity.class);
           startActivity(intent);
       });
   }
   ```
   + 注意：{{c1::项目中添加的任何资源都会在R文件中生成一个相应的资源id}}

5. 在 `Android Manifest`文件中注册:
   ```xml
   <activity android:name=".ActivityTest"></activity>
   ```

6. 配置主活动:
   ```xml
   <activity android:name=".DialogActivity" android:theme="@android:style/Theme.Dialog"></activity>
   <activity android:name=".NormalActivity" />
   ```

### 安卓Toast的使用

```java
Toast.makeText(Firstactivity.this,"You clicked Button 1",Toast.LENGTH_SHORT).show()
```
+ 第一个参数：{{c1::是 Context,也就是 Toast要求的上下文，由于活动本身就是一个 Context对象，因此这里直 接传人 `Firstactivity.this`即可。}}
+ 第二个参数：{{c1::是 Toast显示的文本内容}}
+ 第三个参数：{{c1::是 Toast 显示的时长}}

### 在活动中使用Menu

1. 创建`res/menu/main.xml`文件
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <menu xmlns:android="http://schemas.android.com/apk/res/android">
       <item
           android:id="@+id/add_item"
           android:title="Add"/>
       <item
           android:id="@+id/remove_item"
           android:title="Remove"/>
   </menu>
   ```
2. 在Activity重写`onOptionsItemSelected`方法
   ```java
   @Override
   public boolean onOptionsItemSelected(MenuItem item) {
       switch (item.getItemId()) {
           case R.id.add_item:
               Toast.makeText(this, "You clicked Add", Toast.LENGTH_SHORT).show();
               break;
           case R.id.remove_item:
               Toast.makeText(this, "You clicked Remove", Toast.LENGTH_SHORT).show();
               break;
           default:
       }
       return true;
   }
   ```
+ 理解：{{c1::标签}}


### 销毁一个安卓活动
+ 图示：{{c1::![image-20210401192805190](D:\books\note\CSNote\01 java\android.assets\image-20210401192805190.png)}}



### Android中Intent概述

+ 作用：{{c1::启动其他Activity或者Service，包含要启动对象所需信息。}}
+ 显式Intent:
  + 作用：{{c1::直接指定需要启动的目标活动。}}
  + 使用示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401195618.png)}}
+ 隐式Intent:
  + 作用：{{c1:: 指定一系列更为抽象的`actlon`和`category`等信息，然后交由系统去分析这个`Intent`,并帮我们找出合适的活动去启动。 }}
  + 配置活动以响应**隐式Intent**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401201644.png)}}
  + 启动Intent:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401201657.png)}}

### Intent启动其他程序的活动

+ Intent创建：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401202150.png)}}
+ Intent的Data属性:
  + 作用：{{c1::`<activity>`的`<intent-filter>`标签中可以再配置一个`<data>`标签，只有`<data>`标签中指定的内容和`Intent`中携带的`Data`完全一致时，当前活动才能够响应。}}
  + `<data>`标签主要内容：
    + `android:scheme`：{{c1::用于指定数据的协议部分}}
    + `android:host`：{{c1::用于指定数据的主机名部分，如上例中的www.baidu.com部分。}}
    + `android:port`：{{c1::用于指定数据的端口部分，一般紧随在主机名之后。}}
    + `android:path`：{{c1::用于指定主机名和端口之后的部分，如一段网址中跟在域名之后的内容。}}
    + `android:mimetype`：{{c1::用于指定可以处理的数据类型，允许使用通配符的方式进行指定。}}
    + 示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401202629.png)}}
+ 除了http协议外，我们还可以指定很多其他协议，比如geo表示显示地理位置、tel表示拨打电话:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401202840.png)}}

### 向Intent的目标活动传递数据
+ 主要思路：{{c1::`Intent`中提供了一系列`putExtra()`方法的重载，可以把我们想要传递的数据暂存在`Intent`中}}
+ 放数据示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401203125.png)}}
+ 取数据示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401203139.png)}}

### 返回数据给上一个活动
+ 主要思路:  {{c1:: FirstActivity使用`startActivityForResult()`启动SecondActivity,SecondActivity通过无意图Intent返回数据，FirstActivity再使用OnActivityResult接受数据。}}
+ 示例：
  + 启动SecondActivity：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401204624.png)}}
  + 返回到FirstActivity:
    + 主动返回：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401204641.png)}}
    + 返回键返回：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401211351.png)}}
  + FirstActivity接收数据：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401205039.png)}}

### 活动的生命周期
+ 返回栈：{{c1::Android是使用任务(Task)来管理活动的，一个任务就是一组存放在栈里的活动的集合}}
+ 活动的4种状态：
  + **运行状态**：{{c1::当一个活动**位于**返回栈的**栈顶**时，这时活动就处于运行状态}}
  + **暂停状态**：{{c1::当一个活动**不再处于栈顶**位置，但**仍然可见**时，这时活动就进入了暂停状态。}}
  + **停止状态**：{{c1::当一个活动**不再处于栈顶位置**，并且**完全不可见**的时候，就进入了停止状态}}
  + **销毁状态**：{{c1::当一个活动**从返回栈中移除后**就变成了销毁状态。}}
+ 活动的3种生存期：
  + **完整生存期**：{{c1::活动在 `onCreate()`方法和 `onDestroy()`方法之间所经历的，就是完整生存周期。个活动会在 `onCreate()`方法中完成各种初始化操作，而在`onDestroy()`方法中完成释放内存的操作。}}
  + **可见生存期**：{{c1::活动在 `onStart()`方法和`onStop()`方法之间所经历的，就是可见生存期。}}
  + **前台生存期**：{{c1::活动在 `onResume()`方法和 `onPause()`方法之间所经历的就是前台生存期。在前台生存期内，活动总是处于运行状态的，此时的活动是可以和用户进行交互的，我们平时看到和接触最多的也就是这个状态下的活动。}}
+ 活动的生命周期：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401211901.png)}}

### 活动被垃圾回收，可能造成的数据丢失情况处理

+ 原因：{{c1::活动进入到了停止状态，是有可能被系统回收的}}
+ `OnSaveInstanceState()`：{{c1::Activity方法，保证在活动被回收之前一定会被调用，因此我们可以通过这个方法来解决活动被回收时临时数据得不到保存的问题。}}
+ 使用示例：
  + 保持临时数据：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401213058.png)}}
  + 恢复数据：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401213217.png)}}

### 活动的4种启动模式
+ 指定启动模式配置：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402085244.png)}}
+ `standard`：{{c1::standard是活动默认的启动模式，系统不会在乎这个活动是否已经在返回栈中存在，每次启动都会创建该活动的一个新的实例。}}
  + 示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402084132.png)}}
+ `singleTop`：{{c1:: 在启动活动时如果发现返回栈的栈顶已经是该活动，则认为可以直接使用它，不会再创建新的活动实例。 }}
  + 示意图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402084722.png)}}
+ `singleTask`：{{c1::每次启动该活动时系统首先会在返回栈中检査是否存在该活动的实例，如果发现已经存在则直接使用该实例，并把在这个活动之上的所有活动统统出栈，如果没有发现就会创建一个新的活动实例。}}
+ `singleInstance`:{{c1::不管是哪个应用程序来访问这个活动，都共用的同一个返回栈，也就解决了共享活动实例的问题。}}
  + 示意图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402090745.png)}}

### 活动最佳实践
+ 知晓当前是在哪一个活动：
  + 主要思路：{{c1:: 创建一个BaseActivity基类 }}
  + 示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402093117.png) }}
+ 随时随地退出程序：
  + 主要思路：{{c1::创建一个ActivityController容器类}}
  + 示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402093248.png) }}
+ 启动活动的最佳写法：
  + 主要思路：{{c1:: 在目标活动中，创建静态启动方法，通过Context反向创建Intent }}
  + 示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402093445.png) }}

## 第三章 界面

### android控件常用属性
+ `layout width`: {{c1:: 组件的宽度 }}
+ `layout height`: {{c1:: 组件的高度 }}
+ `id`: {{c1:: 为`Text View`设置一个组件id }}
+ `text`: {{c1:: 设置显示的文本内容 }}
+ `textcolor`: {{c1:: 设置字体颜色 }}
+ `textstyle`: {{c1:: 设置字体风格，三个可选值： normal无效果），bold(加粗，italic（斜体） }}
+ `textSize`: {{c1:: 字体大小，单位一般是用sp }}
+ `background`: {{c1:: 控件的背景颜色，可以理解为填充整个控件的颜色，可以是图片 }}
+ `gravity`: {{c1:: 设置控件中内容的对齐方向， Textview中是文字， Image View中是图片等等。 }}
+ `textallcaps`: {{c1:: 系统会对 Button中的所有英文字母自动进行大写转换，可以设置`false`关闭}}
+ 控件使用规律：{{c1::给控件定义一个id,再指定控件的宽度和高度，然后再适当加入一些控件特有的属性就差不多了。}}
+ `hint`: {{c1:: `EditText`的属性，类似`html` `placeholder`属性。 }}
+ `maxLines`：{{c1:: `EditText`的属性，设置最大行数。 }}

### android注册监听器的2种方法
+ 匿名类注册:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402112654.png)}}
+ 实现接口方式:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402112717.png)}}


### 示例：通过点击按钮来获取EditText中输入的内容
+ 代码：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402115335.png)}}
+ 效果：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402115408.png)

### `ProgressBar`的使用

+ 是否可见设置：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402184734.png)}}
+ 动态进度条使用：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402184836.png)}}

### Dialog

+ `AlertDialog`
  + 主要作用：{{c1:: `AlertDialog`可以在当前的界面弹出一个对话框，这个对话框是**置顶于所有界面元素之上**的， 能够屏蔽掉其他控件的交互能力，因此 `AlertDialog`一般都是用于提示一些**非常重要**的内容或者警告信息。 }}
  + 使用示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402185141.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402185311.png) }}
+ `ProgressDialog`
  + 主要作用：{{c1:: `ProgressDialog`会在对话框中显示一个进度条，一般用于表示当前操作比较耗时，让用户耐心地等待。 }}
  + 使用示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402185555.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402185623.png)}}

### android线性布局：layout_gravity属性示例
+ 效果图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402194956.png)
+ 代码：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402195027.png)}}

### android线性布局：layout_weight属性示例
+ `layout_weight`作用：{{c1::`layout_weight`属性允许我们使用比例的方式来指定控件的大小}}
+ 效果图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402195245.png)
+ 代码：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402195352.png) }}
+ 效果图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402195245.png)
+ 代码：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402195807.png) }}

### android相对布局:相对于父布局定位示例
+ 效果图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402200151.png)
+ 代码：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402200233.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402200317.png) }}


### android相对布局:相对于控件定位的效果示例
+ 效果图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402201028.png)
+ 代码：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402200918.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402200951.png) }}


### android百分比布局示例
+ 效果图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402202838.png)
+ 代码：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402203354.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402203416.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402203424.png)}}

### 控件和布局的继承结构
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402204104.png)}}

### 引入布局：引入自定义标题栏布局示例
+ 定义标题栏布局文件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402205120.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402205131.png)}}
+ 引入标题栏布局文件：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402205234.png) }}
+ 将系统自带的标题栏隐藏掉:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402205303.png)}}

### 自定义控件:自定义标题栏控件示例
+ 自定义控件主要解决的问题：{{c1::引入布局的技巧确实解决了重复编写布局代码的问题，但是如果布局中有一些控件要求能够响应事件，我们还是需要在每个活动中为这些控件单独编写一次事件注册的代码。}}
+ `LayoutInflater.from(context).inflate(R.layout.title, this);`解释：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402211455.png)
+ 定义标题栏布局文件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402205120.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402205131.png)}}
+ 定义自定义控件类：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402211157.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402211208.png)}}
+ 布局文件中添加控件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402211237.png)}}

### Listview使用实例

+ MainActivity核心代码
  ```java
  @Override
  protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);
      initFruits(); // 初始化数据
      FruitAdapter adapter = new FruitAdapter(MainActivity.this, R.layout.fruit_item, fruitList);
      ListView listView = (ListView) findViewById(R.id.list_view);
      listView.setAdapter(adapter);
      listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
          @Override
          public void onItemClick(AdapterView<?> parent, View view,
                                  int position, long id) {
              Fruit fruit = fruitList.get(position);
              Toast.makeText(MainActivity.this, fruit.getName(), Toast.LENGTH_SHORT).show();
          }
      });
  }
  ```
+ FruitAdapter核心代码
  ```java
  @Override
  public View getView(int position, View convertView, ViewGroup parent) {
      Fruit fruit = getItem(position); // 获取当前项的Fruit实例
      View view;
      ViewHolder viewHolder;
      if (convertView == null) {
          view = LayoutInflater.from(getContext()).inflate(resourceId, parent, false);
          viewHolder = new ViewHolder();
          viewHolder.fruitImage = (ImageView) view.findViewById (R.id.fruit_image);
          viewHolder.fruitName = (TextView) view.findViewById (R.id.fruit_name);
          view.setTag(viewHolder); // 将ViewHolder存储在View中
      } else {
          view = convertView;
          viewHolder = (ViewHolder) view.getTag(); // 重新获取ViewHolder
      }
      viewHolder.fruitImage.setImageResource(fruit.getImageId());
      viewHolder.fruitName.setText(fruit.getName());
      return view;
  }
  ```
+ 提升 Listview的运行效率主要思路：{{c1::`getView()`方法中还有一个 `convertView`参数，这个参数用于将之前加载好的布局进行缓存，以便之后可以进行重用}}

