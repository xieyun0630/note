## 第二章 活动 [ ](android_20210425024133088)

### 活动 [ ](android_20210425024133091)
+ 定义：{{c1::活动( Activity)是最容易吸引用户的地方，它是一种可以包含用户界面的组件，主要用于和用户进行交互。}}

### 手动创建活动过程 [ ](android_20210425024133094)

1. 创建`add no Activity` 空项目
2. 添加第一个Activity,注意不要生成layout，设置主Activity.
3. 在`app/src/main/res`下添加`layout/first_layout.xml`布局文件。
   ```xml
   <!-- {{c1:: -->
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:orientation="vertical" android:layout_width="match_parent"
       android:layout_height="match_parent">
       <Button
    android:id="@+id/start_normal_activity"
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:text="start normal activity" />
   </LinearLayout>
   <!-- }} -->
   ```
4. 在对应Activity中添加相应关联:
   ```java
   //{{c1::
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_test);
       ((Button) findViewById(R.id.start_normal_activity)).setOnClickListener(event ->{
           Intent intent = new Intent(ActivityTest.this, NormalActivity.class);
           startActivity(intent);
       });
   }
   //}}
   ```
   + 注意：{{c1::项目中添加的任何资源都会在R文件中生成一个相应的资源id}}
5. 在 `Android Manifest`文件中注册:
   ```xml
   <!-- {{c1:: -->
   <activity android:name=".ActivityTest"></activity>
   <!-- }} -->
   ```
6. 配置主活动:
   ```xml
   <!-- {{c1:: -->
    <activity android:name=".ActivityTest">
      <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
      </intent-filter>
    </activity>
   <!-- }} -->
   ```

### 安卓Toast的使用 [ ](android_20210425024133096)

```java
//{{c1::
Toast.makeText(Firstactivity.this,"You clicked Button 1",Toast.LENGTH_SHORT).show()
//}}
```
+ 第一个参数：{{c1::是 Context,也就是 Toast要求的上下文，由于活动本身就是一个 Context对象，因此这里直 接传人 `Firstactivity.this`即可。}}
+ 第二个参数：{{c1::是 Toast显示的文本内容}}
+ 第三个参数：{{c1::是 Toast 显示的时长}}

### 在活动中使用Menu [ ](android_20210425024133098)

1. 创建`res/menu/main.xml`文件
   ```xml
   <!-- {{c1:: -->
   <?xml version="1.0" encoding="utf-8"?>
   <menu xmlns:android="http://schemas.android.com/apk/res/android">
       <item
           android:id="@+id/add_item"
           android:title="Add"/>
       <item
           android:id="@+id/remove_item"
           android:title="Remove"/>
   </menu>
   <!-- }} -->
   ```
2. 在Activity重写`onOptionsItemSelected`方法
   ```java
   //{{c1::
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
   //}}
   ```
+ 理解：{{c1::标签}}


### 销毁一个安卓活动 [ ](android_20210425024133100)
+ 图示：{{c1::![image-20210401192805190](D:\books\note\CSNote\01 java\android.assets\image-20210401192805190.png)}}



### Android中Intent概述 [ ](android_20210425024133103)

+ 作用：{{c1::启动其他Activity或者Service，包含要启动对象所需信息。}}
+ 显式Intent:
  + 作用：{{c1::直接指定需要启动的目标活动。}}
  + 使用示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401195618.png)}}
+ 隐式Intent:
  + 作用：{{c1:: 指定一系列更为抽象的`actlon`和`category`等信息，然后交由系统去分析这个`Intent`,并帮我们找出合适的活动去启动。 }}
  + 配置活动以响应**隐式Intent**:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401201644.png)}}
  + 启动Intent:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401201657.png)}}

### Intent启动其他程序的活动 [ ](android_20210425024133106)

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

### 向Intent的目标活动传递数据 [ ](android_20210425024133109)
+ 主要思路：{{c1::`Intent`中提供了一系列`putExtra()`方法的重载，可以把我们想要传递的数据暂存在`Intent`中}}
+ 放数据示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401203125.png)}}
+ 取数据示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401203139.png)}}

### 返回数据给上一个活动 [ ](android_20210425024133112)
+ 主要思路:  {{c1:: FirstActivity使用`startActivityForResult()`启动SecondActivity,SecondActivity通过无意图Intent返回数据，FirstActivity再使用OnActivityResult接受数据。}}
+ 示例：
  + 启动SecondActivity：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401204624.png)}}
  + 返回到FirstActivity:
    + 主动返回：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401204641.png)}}
    + 返回键返回：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401211351.png)}}
  + FirstActivity接收数据：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401205039.png)}}

### 活动的生命周期 [ ](android_20210425024133116)
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

### 活动被垃圾回收，可能造成的数据丢失情况处理 [ ](android_20210425024133120)

+ 原因：{{c1::活动进入到了停止状态，是有可能被系统回收的}}
+ `OnSaveInstanceState()`：{{c1::Activity方法，保证在活动被回收之前一定会被调用，因此我们可以通过这个方法来解决活动被回收时临时数据得不到保存的问题。}}
+ 使用示例：
  + 保持临时数据：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401213058.png)}}
  + 恢复数据：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210401213217.png)}}

### 活动的4种启动模式 [ ](android_20210425024133123)
+ 指定启动模式配置：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402085244.png)}}
+ `standard`：{{c1::standard是活动默认的启动模式，系统不会在乎这个活动是否已经在返回栈中存在，每次启动都会创建该活动的一个新的实例。}}
  + 示例：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402084132.png)}}
+ `singleTop`：{{c1:: 在启动活动时如果发现返回栈的栈顶已经是该活动，则认为可以直接使用它，不会再创建新的活动实例。 }}
  + 示意图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402084722.png)}}
+ `singleTask`：{{c1::每次启动该活动时系统首先会在返回栈中检査是否存在该活动的实例，如果发现已经存在则直接使用该实例，并把在这个活动之上的所有活动统统出栈，如果没有发现就会创建一个新的活动实例。}}
+ `singleInstance`:{{c1::不管是哪个应用程序来访问这个活动，都共用的同一个返回栈，也就解决了共享活动实例的问题。}}
  + 示意图：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402090745.png)}}

### 活动最佳实践 [ ](android_20210425024133126)
+ 知晓当前是在哪一个活动：
  + 主要思路：{{c1:: 创建一个BaseActivity基类 }}
  + 示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402093117.png) }}
+ 随时随地退出程序：
  + 主要思路：{{c1::创建一个ActivityController容器类}}
  + 示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402093248.png) }}
+ 启动活动的最佳写法：
  + 主要思路：{{c1:: 在目标活动中，创建静态启动方法，通过Context反向创建Intent }}
  + 示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402093445.png) }}

## 第三章 界面 [ ](android_20210425024133128)

### android控件常用属性 [ ](android_20210425024133131)
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

### android注册监听器的2种方法 [ ](android_20210425024133135)
+ 匿名类注册:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402112654.png)}}
+ 实现接口方式:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402112717.png)}}


### 示例：通过点击按钮来获取EditText中输入的内容 [ ](android_20210425024133137)
+ 代码：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402115335.png)}}
+ 效果：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402115408.png)

### `ProgressBar`的使用 [ ](android_20210425024133139)

+ 是否可见设置：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402184734.png)}}
+ 动态进度条使用：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402184836.png)}}

### Dialog [ ](android_20210425024133141)

+ `AlertDialog`
  + 主要作用：{{c1:: `AlertDialog`可以在当前的界面弹出一个对话框，这个对话框是**置顶于所有界面元素之上**的， 能够屏蔽掉其他控件的交互能力，因此 `AlertDialog`一般都是用于提示一些**非常重要**的内容或者警告信息。 }}
  + 使用示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402185141.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402185311.png) }}
+ `ProgressDialog`
  + 主要作用：{{c1:: `ProgressDialog`会在对话框中显示一个进度条，一般用于表示当前操作比较耗时，让用户耐心地等待。 }}
  + 使用示例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402185555.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402185623.png)}}

### android线性布局：layout_gravity属性示例 [ ](android_20210425024133144)
+ 效果图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402194956.png)
+ 代码：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402195027.png)}}

### android线性布局：layout_weight属性示例 [ ](android_20210425024133147)
+ `layout_weight`作用：{{c1::`layout_weight`属性允许我们使用比例的方式来指定控件的大小}}
+ 效果图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402195245.png)
+ 代码：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402195352.png) }}
+ 效果图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402195245.png)
+ 代码：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402195807.png) }}

### android相对布局:相对于父布局定位示例 [ ](android_20210425024133151)
+ 效果图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402200151.png)
+ 代码：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402200233.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402200317.png) }}


### android相对布局:相对于控件定位的效果示例 [ ](android_20210425024133153)
+ 效果图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402201028.png)
+ 代码：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402200918.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402200951.png) }}


### android百分比布局示例 [ ](android_20210425024133155)
+ 效果图：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402202838.png)
+ 代码：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402203354.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402203416.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402203424.png)}}

### 控件和布局的继承结构 [ ](android_20210425024133157)
+ 图示：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402204104.png)}}

### 引入布局：引入自定义标题栏布局示例 [ ](android_20210425024133160)
+ 定义标题栏布局文件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402205120.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402205131.png)}}
+ 引入标题栏布局文件：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402205234.png) }}
+ 将系统自带的标题栏隐藏掉:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402205303.png)}}

### 自定义控件:自定义标题栏控件示例 [ ](android_20210425024133162)
+ 自定义控件主要解决的问题：{{c1::引入布局的技巧确实解决了重复编写布局代码的问题，但是如果布局中有一些控件要求能够响应事件，我们还是需要在每个活动中为这些控件单独编写一次事件注册的代码。}}
+ `LayoutInflater.from(context).inflate(R.layout.title, this);`解释：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402211455.png)
+ 定义标题栏布局文件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402205120.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402205131.png)}}
+ 定义自定义控件类：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402211157.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402211208.png)}}
+ 布局文件中添加控件：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210402211237.png)}}

### Listview使用实例 [ ](android_20210425024133165)

+ MainActivity核心代码
  ```java
  //{{c1::
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
  //}}
  ```
+ FruitAdapter核心代码
  ```java
  //{{c1::
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
  //}}
  ```
+ 提升 Listview的运行效率主要思路：{{c1::`getView()`方法中还有一个 `convertView`参数，这个参数用于将之前加载好的布局进行缓存，以便之后可以进行重用}}

### RecyclerView使用 [ ](android_20210425024133169)
+ 导入依赖：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407083331.png)
+ 在layout中声明：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407083420.png)
+ 定义Adapter步骤：
  1. 继承对应Adapter:{{c1::`RecyclerView.Adapter<FruitAdapter.ViewHolder>`}}
  2. 重写`onCreateViewHolder(ViewGroup parent, int viewType)`：{{c1::用于创建 Viewholder实例的，我们在这个方法中将布局加载进来，然后创建一个 `ViewHolder`实例，并把加载出来的布局传入到构造函数当中，最后将`Viewholder`的实例返回。相应**点击事件**也在该方法内定义}}
  3. 重写`onBindViewHolder(ViewHolder holder, int position)`：{{c1::会在每个子项被滚动到屏幕内的时候执行，这里我们通过 position参数得到当前项的 Fruit实例，然后再将数据设置到 Viewholder的 Image View和 Text View当中即可。}}
  4. 重写`getItemCount()`：{{c1::它用于告诉 Recycler Viewー共有多少子项，直接返回数据源的长度就可以了。}}
  + Adapter实例：
    ```java
    //{{c1::
    public class FruitAdapter extends RecyclerView.Adapter<FruitAdapter.ViewHolder>{

        private List<Fruit> mFruitList;

        static class ViewHolder extends RecyclerView.ViewHolder {
            View fruitView;
            ImageView fruitImage;
            TextView fruitName;

            public ViewHolder(View view) {
                super(view);
                fruitView = view;
                fruitImage = (ImageView) view.findViewById(R.id.fruit_image);
                fruitName = (TextView) view.findViewById(R.id.fruit_name);
            }
        }

        public FruitAdapter(List<Fruit> fruitList) {
            mFruitList = fruitList;
        }

        @Override
        public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
            View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.fruit_item, parent, false);
            final ViewHolder holder = new ViewHolder(view);
            holder.fruitView.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    int position = holder.getAdapterPosition();
                    Fruit fruit = mFruitList.get(position);
                    Toast.makeText(v.getContext(), "you clicked view " + fruit.getName(), Toast.LENGTH_SHORT).show();
                }
            });
            holder.fruitImage.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    int position = holder.getAdapterPosition();
                    Fruit fruit = mFruitList.get(position);
                    Toast.makeText(v.getContext(), "you clicked image " + fruit.getName(), Toast.LENGTH_SHORT).show();
                }
            });
            return holder;
        }

        @Override
        public void onBindViewHolder(ViewHolder holder, int position) {
            Fruit fruit = mFruitList.get(position);
            holder.fruitImage.setImageResource(fruit.getImageId());
            holder.fruitName.setText(fruit.getName());
        }

        @Override
        public int getItemCount() {
            return mFruitList.size();
        }
    }
    //}}
    ```
+ 在Activity中调用：
  ```java
  //{{c1::
  @Override
  protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);
      initFruits();
      RecyclerView recyclerView = (RecyclerView) findViewById(R.id.recycler_view);
      // 注意有多种布局管理器
      StaggeredGridLayoutManager layoutManager = new
              StaggeredGridLayoutManager(3, StaggeredGridLayoutManager.VERTICAL);
      recyclerView.setLayoutManager(layoutManager);
      FruitAdapter adapter = new FruitAdapter(fruitList);
      recyclerView.setAdapter(adapter);
  }
  //}}
  ```

## 第4章 碎片 [ ](android_20210425024133172)

### 简单使用碎片 [ ](android_20210425024133174)
+ 运行效果：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407093552.png)}}
+ activity_main.xml声明碎片：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407093331.png)}}
+ 定义对应的碎片类：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407093423.png)}}
+ 定义碎片类的布局文件：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407093526.png)}}


### 动态添加碎片 [ ](android_20210425024133176)
+ 新建碎片类，在活动中声明FrameLayout：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407094909.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407094210.png)}}
+ 修改活动代码，在FrameLayout中添加内容：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407094732.png)}}
  + 动态添加碎片主要分为5步：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407094832.png)}}
+ 在碎片中模拟返回栈：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407100425.png)}}
  + 注意：{{c1:: `addtobackstack()`方法，可以用于将一个事务添加到返回栈中}}

### 碎片和活动之间进行通信 [ ](android_20210425024133178)

+ 在活动中调用碎片的方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407101101.png)}}
+ 在碎片中调用活动的方法：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407101201.png)}}

### 碎片的生命周期 [ ](android_20210425024133180)

+ 碎片附加的回调方法：
  + `onAttach()`：{{c1::当碎片和活动建立关联的时候调用。}}
  + `onCreateView()`：{{c1::为碎片创建视图（加载布局）时调用。}}
  + `onActivityCreated()`：{{c1::确保与碎片相关联的活动一定已经创建完毕的时候调用。}}
  + `ondDestroyView()`：{{c1::当与碎片关联的视图被移除的时候调用。}}
  + `onDetach()`：{{c1::当碎片和活动解除关联的时候调用。}}
+ 碎片的生命周期示意图:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407102915.png)}}

### 动态加载布局的技巧 [ ](android_20210425024133183)

+ 使用限定词：
  + `res/layout-large/activity_main.xml`
  + `res/layout/activity_main.xml`
  + 注意：{{c1:: 其中large为限定词，程序自动判断读取哪个文件夹的布局。}}
+ 常见限定词：
  + {{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407105328.png)![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407105339.png)}}
+ 最小宽度限定词：{{c1::`res/layout-sw600dp/activity_main.xml`}}
  + 解释：{{c1:: 当程序运行在屏幕宽度大于600dp的设备上时，会加载 `res/layout-sw600dp/activity_main.xml`布局，当程序运行在屏幕宽度小于600dp的设备上时，则仍然加载默认的 `layout/activityMain`布局。}}

## 第五章 广播 [ ](android_20210425024133185)

### 接收系统广播：动态注册 [ ](android_20210425024133189)
+ AndroidManifest.xml中声明网络权限:{{c1::
  ```xml
     <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
  ​```}}
  ```
+ 动态**注册**监听网络变化:{{c1::
  ```java
  public class MainActivity extends AppCompatActivity {
     private IntentFilter intentFilter;
     private NetworkChangeReceiver networkChangeReceiver;

      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
          intentFilter = new IntentFilter();
          intentFilter.addAction("android.net.conn.CONNECTIVITY_CHANGE");
          networkChangeReceiver = new NetworkChangeReceiver();
          //注册
          registerReceiver(networkChangeReceiver,intentFilter);
      }

      @Override
      protected void onDestroy() {
          super.onDestroy();
          //取消注册
          unregisterReceiver(networkChangeReceiver);
      }

     class NetworkChangeReceiver extends BroadcastReceiver {
         @Override
         public void onReceive(Context context, Intent intent) {
             ConnectivityManager connectionManager = (ConnectivityManager)
                     getSystemService(Context.CONNECTIVITY_SERVICE);
             NetworkInfo networkInfo = connectionManager.getActiveNetworkInfo();
             if (networkInfo != null && networkInfo.isAvailable()) {
                 Toast.makeText(context, "network is available",
                         Toast.LENGTH_SHORT).show();
             } else {
                 Toast.makeText(context, "network is unavailable",
                         Toast.LENGTH_SHORT).show();
             }
         }
     }
  }
  ​```}}
  ```


### 接收系统广播：静态注册 [ ](android_20210425024133192)

+ 在AndroidManifest.xml进行**静态注册**以及**权限配置**：
  ```xml
  <!-- {{c1:: -->
    <!-- .... -->
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
    <!-- .... -->
        <receiver
            android:name=".BootCompleteReceiver"
            android:enabled="true"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
            </intent-filter>
        </receiver>
    <!-- .... -->
  <!-- }} -->
  ```
+ 广播接受器类定义：
  ```java
  //{{c1::
  public class BootCompleteReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        Toast.makeText(context, "Boot Complete", Toast.LENGTH_LONG).show();
    }
  }
  //}}
  ```

### 自定义广播：发送标准广播 [ ](android_20210425024133195)
+ `AndroidManifest.xml`中定义广播接收器：{{c1::
  ```xml
  <receiver
      android:name=".MyBroadcastReceiver"
      android:enabled="true"
      android:exported="true">
      <intent-filter android:priority="100">
          <action android:name="com.example.broadcasttest.MY_BROADCAST"/>
      </intent-filter>
  </receiver>
  ```
  }}
+ 定义接收器类：{{c1::
  ```java
  public class MyBroadcastReceiver extends BroadcastReceiver {
      @Override
      public void onReceive(Context context, Intent intent) {
          Toast.makeText(context, "received in MyBroadcastReceiver", Toast.LENGTH_SHORT).show();
          abortBroadcast();
      }
  }
  ```
  }}
+ 在活动中发送广播：{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407143942.png)}}

### 自定义广播：发送有序广播 [ ](android_20210425024133197)
+ Activity中发送有序广播:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407144941.png)}}
+ 利用优先级定义接受广播的顺序:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407145034.png)}}
+ 在广播接受器中戒断广播:{{c1::![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210407145128.png)}}

### 自定义广播：发送本地广播 [ ](android_20210425024133199)
+ 使用LocalBroadcastManager对广播进行管理
  ```java
  //{{c1::
  public class MainActivity extends AppCompatActivity {
      private IntentFilter intentFilter;
      private LocalReceiver localReceiver;
      private LocalBroadcastManager localBroadcastManager;
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
          localBroadcastManager = LocalBroadcastManager.getInstance(this); // 获取实例
          Button button = (Button) findViewById(R.id.button);
          button.setOnClickListener(new View.OnClickListener() {
              @Override
              public void onClick(View v) {
                  Intent intent = new Intent("com.example.broadcasttest.LOCAL_BROADCAST");
                  localBroadcastManager.sendBroadcast(intent); // 发送本地广播
              }
          });
          intentFilter = new IntentFilter();
          intentFilter.addAction("com.example.broadcasttest.LOCAL_BROADCAST");
          localReceiver = new LocalReceiver();
          localBroadcastManager.registerReceiver(localReceiver, intentFilter); // 注册本地广播监听器
      }
      @Override
      protected void onDestroy() {
          super.onDestroy();
          localBroadcastManager.unregisterReceiver(localReceiver);
      }
      class LocalReceiver extends BroadcastReceiver {
          @Override
          public void onReceive(Context context, Intent intent) {
              Toast.makeText(context, "received local broadcast", Toast.LENGTH_SHORT).show();
          }
      }
  }
  //}}
  ```

## 第六章 持久化技术 [ ](android_20210425024133201)

### 文件存储 [ ](android_20210425024133203)
+ `Context`类`openFileOutput()`方法
  + 作用：可以用于将数据存储到指定的文件中。
  + 第一个参数：{{c1:: 指定文件创建时的名称，可以不保护路径，默认路径为`/data/data/<package-name>/files/` }}
  + 第二个参数：{{c1:: 文件操作模式，`MODE_PRIMARY`模式，文件已存在覆盖文件， `MODE_APPEND`文件已存在时，在末尾追加文件。}}
