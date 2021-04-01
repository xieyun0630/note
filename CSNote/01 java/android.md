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

   + 注意：项目中添加的任何资源都会在R文件中生成一个相应的资源id

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

+ 第一个参数：是 Context,也就是 Toast要求的上下文，由于活动本身就是一个 Context对象，因此这里直 接传人 `Firstactivity.this`即可。
+ 第二个参数：是 Toast显示的文本内容
+ 第三个参数：是 Toast 显示的时长

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

### 销毁一个安卓活动

+ 图示：{{c1::![image-20210401192805190](D:\books\note\CSNote\01 java\android.assets\image-20210401192805190.png)}}



### Android中Intent概述

+ 作用：{{c1::启动其他Activity或者Service，包含要启动对象所需信息。}}
+ 显式Intent:
  + 作用：直接指定需要启动的目标活动。
  + 使用示例：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401195618.png)
+ 隐式Intent:
  + 作用：{{c1:: 指定一系列更为抽象的`actlon`和`category`等信息，然后交由系统去分析这个`Intent`,并帮我们找出合适的活动去启动。 }}
  + 配置活动以响应**隐式Intent**:![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401201644.png)
  + 启动Intent:![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401201657.png)

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

### 活动的启动模式