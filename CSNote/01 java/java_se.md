# java FX [	](java_se_20191219101334709)

## Java FX程序的基本结构 [	](java_se_20191219101334711)

### 一个最基本结构java FX程序 [	](java_se_20191219101334713)

图：

![image-20191216221654589](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191216221654589.png)

```java
public class MyJavaFX extends Application {
  //{{c1::
  @Override
  public void start(Stage primaryStage) {
    // Create a button and place it in the scene
    Button btOK = new Button("OK");
    Scene scene = new Scene(btOK, 200, 250);
    primaryStage.setTitle("MyJavaFX"); // Set the stage title
    primaryStage.setScene(scene); // Place the scene in the stage
    primaryStage.show(); // Display the stage
  }
	//在IDE中需显式调用
  public static void main(String[] args) { 
    Application.launch(args);
  }
  //}}
}
```

命令行执行javaFX程序时会自动{{c1::调用`AppliApplication.launch(args);`方法。}}

### 一个javaFX程序显示多个舞台 [	](java_se_20191219101334714)

![image-20191216221951820](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191216221951820.png)

核心代码：

```java
//{{c1::
	  Stage newStage = new Stage();
    newStage.setTitle("Second Stage");
    newStage.setScene(new Scene(new Button("New Stage"), 100, 100));
    newStage.show();
//}}
```

+ **stage.setResizable(false)**方法：{{c1:禁止改变舞台大小}}

### 使用javaFX类库在一个面版中央显示圆： [	](java_se_20191219101334715)

{{c1::

```java
    public void start(Stage primaryStage) throws Exception {
        Pane pane = new Pane();
        pane.setMaxWidth(200);
        pane.setMaxHeight(200);

        Circle circle = new Circle();
        circle.centerXProperty().bind(pane.widthProperty().divide(2));
        circle.centerYProperty().bind(pane.heightProperty().divide(2));
        circle.setRadius(30);
        circle.setStroke(Color.RED);
        circle.setFill(Color.BLUE);
        pane.getChildren().add(circle);

        primaryStage.setScene(new Scene(pane,200,200));
        primaryStage.setTitle("showCircle");
        primaryStage.show();
    }
```

}}

### javaFX中各个类的关系。 [	](java_se_20191219101334717)

+ Stage组合{{c1::Scene}}
+ Scene组合{{c1::Parent}},因此Scenne不能直接{{c1::包含Shape与ImageView}}
+ {{c1::Shape}}与{{c1::ImageView}}继承自Node
+ {{c1::Control}}与{{c1::Pane}}继承自Parent

{{c1::![image-20191216224429952](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191216224429952.png)}}

### Java FX的绑定属性 [	](java_se_20191219101334719)

+ 例：{{c1:: `targetProperty.bind(source)`}}

+ 对于 double/float/1ong/int/boolean 类型的值，它的绑定属性类型是{{c1::DoubleProperty/FloatProperty/LongProperty/IntegerProperty/BooleanProperty。}}

+ 数值类绑定属性提供了{{c1:: 常用的运算方法}}

+ DoubleProperty等基本绑定属性为{{c1:: 抽象类}},需要使用{{c1:: 对应的实现类SimpleDoubleProperty等}}创建实例.

+ 方法签名{{c1::
  ```java
  /**
    * 为当前绑定属性对象设置单向绑定。 绑定的对象必须先实现ObservableValue接口
    */
  void bind(ObservableValue<? extends T> observable);
  ```
  
  }}

### 绑定属性应该具有的3个方法 [	](java_se_20191219101334721)

{{c1::

+ getter与setter方法
+ `public propertyType xProperty()`

}}

### java FX中Node类的通用方法 [	](java_se_20191219101334722)

+ ` setStyle(String value)`:{{c1:: 设置css样式}}
+ `setRotate()`:{{c1:: 可以设置旋转的角度}}

```java
//黑边 红色填充
//{{c1:: 
bt.setStyle("-fx-stroke: black; -fx-fill: red;");
//}}
//旋转角度顺时针80
//{{c1::
b.setRotate(80);
//}}
```

### java FX中Color类用法 [	](java_se_20191219101334724)

+ 使用构造方法:

{{c1::

```java
public Color(double r, double g ,double b double opacity);
```

}}

+ 使用{{c1::Color.RED之类的标准颜色}}

### java FX中Font类用法 [	](java_se_20191219101334725)

![image-20191217210937741](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191217210937741.png)

核心代码：{{c1::

```java
// FontDemo类
//使用字体类
Label label = new Label("JavaFX");
label.setFont(Font.font("Times New Roman", 
                        FontWeight.BOLD, FontPosture.ITALIC, 20));
pane.getChildren().add(label);
```

}}

### 一个图像通过面版中的三个图像视图显示 [	](java_se_20191219101334727)

![image-20191217213019505](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191217213019505.png)

`ShowImage`类核心代码：

{{c1::

```java
    Pane pane = new HBox(10);
    pane.setPadding(new Insets(5, 5, 5, 5));
    Image image = new Image("m2.jpg");
    pane.getChildren().add(new ImageView(image));
    
    ImageView imageView2 = new ImageView(image);
    imageView2.setFitHeight(100);
    imageView2.setFitWidth(100);
    pane.getChildren().add(imageView2);   

    ImageView imageView3 = new ImageView(image);
    imageView3.setRotate(90);
    pane.getChildren().add(imageView3);     
```

}}

### GridPane的用法 [	](java_se_20191219101334729)

图示：

![image-20191217214418469](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191217214418469.png)

`ShowGridPane`核心代码：

{{c1::

```java
    GridPane pane = new GridPane();
    pane.setAlignment(Pos.CENTER);
    pane.setPadding(new Insets(11.5, 12.5, 13.5, 14.5));
    pane.setHgap(5.5);
    pane.setVgap(5.5);
    
    // Place nodes in the pane
    pane.add(new Label("First Name:"), 0, 0);
    pane.add(new TextField(), 1, 0);
    pane.add(new Label("MI:"), 0, 1); 
    pane.add(new TextField(), 1, 1);
    pane.add(new Label("Last Name:"), 0, 2);
    pane.add(new TextField(), 1, 2);
    Button btAdd = new Button("Add Name");
    pane.add(btAdd, 1, 3);
    GridPane.setHalignment(btAdd, HPos.RIGHT);
```

}}

### JavaFx中布局面板 [	](java_se_20191219101334731)

|    Pane    | {{c1::布局面板的基类.getChildren方法来返回面板中的节点列表}} |
| :--------: | ------------------------------------------------------------ |
| StackPane  | {{c1::节点放置在面板中央.并且畳加在其他节点之上}}            |
|  FlowPane  | {{c1::节点以**水平方式**（`Orientation.HORIZONTAL`）一行一行放,或者**垂直方式**一列一列放}} |
|  CridPane  | {{c1::节点放置在一个二维网格的单元格中}}                     |
| BorderPane | {{c1::将节点放置在頂部、右边、底鄙、左边以及中间区域}}       |
|    HBox    | {{c1::节点放在単行中}}                                       |
|    VBox    | {{c1::节点放在单列中}}                                       |

## javaFX事件 [	](java_se_20191219101334732)

### 事件与事件源 [	](java_se_20191219101334733)

+ java中的事件类的根类是{{c1::`java.util.EventObject`}}
+ javaFX中的事件类的根类是{{c1::`javafx.event.Event`}}
+ 可以通过事件类的{{c1::`getSoource()`}}方法来确定一个事件的源对象。

### JavaFx中为一个按钮注册处理器与处理事件 [	](java_se_20191219101334735)

{{c1::

```java
// Create and register the 
btn.setOnAction(new EnlargeHandler());

class EnlargeHandler implements EventHandler<ActionEvent> {
  @Override // Override the handle method
  public void handle(ActionEvent e) {
    circlePane.enlarge();
  }
}
```

}}

lambda表达式版版：{{c1::

```java
btn.setOnAction(event -> circlePane.enlarge());
```

}}

### `MouseEvent`鼠标事件 [	](java_se_20191219101334737)

![image-20191217225338016](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191217225338016.png)

{{c1::![image-20191217225333086](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191217225333086.png)}}

### 键盘事件 [	](java_se_20191219101334741)

![image-20191217225457041](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191217225457041.png)

{{c1::![image-20191217225448723](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191217225448723.png)}}


### javafx.animation.Animation类 [	](java_se_20191219101334760)

![image-20191217234145104](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191217234145104.png)

{{c1::![image-20191217234138105](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191217234138105.png)}}

### javafx.animation.PathTransition类的使用 [	](java_se_20191219101334761)

![image-20191217234638494](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191217234638494.png)

PathTransitionDemo类核心代码：

```java
// Create a circle
Circle circle = new Circle(125, 100, 50);
circle.setFill(Color.WHITE);
circle.setStroke(Color.BLACK);

// Add circle and rectangle to the pane
pane.getChildren().add(circle);
pane.getChildren().add(rectangle);
//{{c1::
// Create a path transition 
PathTransition pt = new PathTransition();
pt.setDuration(Duration.millis(4000));
pt.setPath(circle);
pt.setNode(rectangle);
pt.setOrientation(PathTransition.OrientationType.ORTHOGONAL_TO_TANGENT );
pt.setCycleCount(Timeline.INDEFINITE);
pt.setAutoReverse(true);
pt.play(); // Start animation 
//}}
```

### javafx.animation.FadeTransition类的使用 [	](java_se_20191219101334763)

![image-20191217235155820](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191217235155820.png)

FadeTransitionDemo核心代码：

```java
// Place an ellipse to the pane
Pane pane = new Pane();
Ellipse ellipse = new Ellipse(10, 10, 100, 50);
ellipse.setFill(Color.RED); 
ellipse.setStroke(Color.BLACK);
ellipse.centerXProperty().bind(pane.widthProperty().divide(2));
ellipse.centerYProperty().bind(pane.heightProperty().divide(2));    
ellipse.radiusXProperty().bind(
  pane.widthProperty().multiply(0.4));    
ellipse.radiusYProperty().bind(
  pane.heightProperty().multiply(0.4)); 
pane.getChildren().add(ellipse);

// {{c1::
FadeTransition ft = 
  new FadeTransition(Duration.millis(3000), ellipse);
ft.setFromValue(1.0);
ft.setToValue(0.1);
ft.setCycleCount(Timeline.INDEFINITE);
ft.setAutoReverse(true);
ft.play();
//}}
// Control animation
ellipse.setOnMousePressed(e -> ft.pause());
ellipse.setOnMouseReleased(e -> ft.play());
```

###  javafx.animation.Timeline的使用 [	](java_se_20191219101334765)

+ PathTransition 和 FadeTransition 定义了特定的动画。Timeline 类可以用于通过使用一个或者更多的 KeyFrame (关键帧）来编写任意动画。每个 KeyFrame 在一个给定的时间间隔内顺序执行。Timeline 继承自 Animation。
+ ![image-20191218203918151](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218203918151.png)

核心代码：

```java
// Create a handler for changing text
EventHandler<ActionEvent> eventHandler = e -> {
  if (text.getText().length() != 0) {
    text.setText("");
  }
  else {
    text.setText("Programming is fun");
  }
};
//{{c1::
// Create an animation for alternating text
Timeline animation = new Timeline(new KeyFrame(Duration.millis(500), eventHandler));
animation.setCycleCount(Timeline.INDEFINITE);
animation.play(); 
// }}
```

## Java FX类库 [	](java_se_20201026014023074)

### Labeled类与Label类 [	](java_se_20191219101334772)

![image-20191218205717224](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218205717224.png)

Label类的构造方法：{{c1::`public Label(String text, Node graphic)`}}

{{c1::



![image-20191218205636656](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218205636656.png)

![image-20191218205747071](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218205747071.png)

}}

### Button的使用 [	](java_se_20191219101334774)

![image-20191218210431437](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218210431437.png)

核心代码：{{c1::

```java
Button btLeft = new Button("Left", new ImageView("image/left.gif"));
Button btRight = new Button("Right", new ImageView("image/right.gif"));   
```

}}

### RadioButtion与CheckBox的使用例子 [	](java_se_20191219101334775)

![image-20191218211531355](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218211531355.png)

CheckBox核心代码：

{{c1::

```java
//定义元素
CheckBox chkBold = new CheckBox("Bold");
CheckBox chkItalic = new CheckBox("Italic");

//定义事件处理器
EventHandler<ActionEvent> handler = e -> { 
  if (chkBold.isSelected() && chkItalic.isSelected()) {
    text.setFont(fontBoldItalic); // Both check boxes checked
  }
  else if (chkBold.isSelected()) {
    text.setFont(fontBold); // The Bold check box checked
  }
  else if (chkItalic.isSelected()) {
    text.setFont(fontItalic); // The Italic check box checked
  }      
  else {
    text.setFont(fontNormal); // Both check boxes unchecked
  }
};
//祖册事件
chkBold.setOnAction(handler);
chkItalic.setOnAction(handler);
```

}}

RadioButtonDemo核心代码：

{{c1::

```java
//定义元素
RadioButton rbRed = new RadioButton("Red");
RadioButton rbGreen = new RadioButton("Green");
RadioButton rbBlue = new RadioButton("Blue");
//设置组
ToggleGroup group = new ToggleGroup();
rbRed.setToggleGroup(group);
rbGreen.setToggleGroup(group);
rbBlue.setToggleGroup(group);
//设置事件
rbRed.setOnAction(e -> {
  if (rbRed.isSelected()) {
    text.setFill(Color.RED);
  }
});
```

}}

### TextField类与PasswordField类的使用 [	](java_se_20191219101334776)

TextFiled类与PasswordFiled类区别在于：{{c1::PasswordFiled显示***隐藏了文本。}}

基本使用代码：{{c1::

```java
TextField textField=new TextField();
PasswordField passwordField=new PasswordField();

textFiled.setActionEvent(c -> textField.getText());
passwordField.setActionEvent(c -> passwordField.getText());
```

}}

### TextArea类 [	](java_se_20191219101334778)

+ prefColumnCount绑定属性：{{c1::指定文本的优先列数}}
+ prefRowCount绑定属性：{{c1::指定文本的优先列数}}
+ wrapText绑定属性：{{c1::指定文本是否折到下一行}}
+ 添加滚动功能：{{c1::`ScrollPane scrollPane=new ScrollPane(textArea);`}}

### TextArea与ScrollPane 例子 [	](java_se_20191219101334780)

![image-20191218222600951](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218222600951.png)

核心代码：

{{c1::

```java
Label label = new Label();
TextArea textArea = new TextArea();
// Center the icon and text and place the text under the icon
label.setContentDisplay(ContentDisplay.TOP);
label.setPrefSize(200,  100);

// Set the font in the label and the text field
label.setFont(new Font("SansSerif", 16));
textArea.setFont(new Font("Serif", 14));
//  taDescription.setWrapText(true);
//  taDescription.setEditable(false);
ScrollPane scrollPane = new ScrollPane(textArea);

setLeft(label);
setCenter(scrollPane);
setPadding(new Insets(5, 5, 5, 5));
```

}}

### 下拉框 [	](java_se_20191219101334782)

JavaFX 提供了⼀个静态⽅法{{c1::` FXCollections.observableArrayList ( arrayOfElements )`}}来从⼀个元素数组中创建⼀个ObservableList。

例子：![image-20191218223804555](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218223804555.png)

核心代码：{{c1::

```java
ComboBox<String> cbo = new ComboBox<>(); 
cbo.setPrefWidth(400);
cbo.setValue("Canada");
ObservableList<String> items = 
  FXCollections.observableArrayList(flagTitles);
cbo.getItems().addAll(items); 
// Display the selected country
cbo.setOnAction(e -> setDisplay(items.indexOf(cbo.getValue())));
```

}}

### ListViewDemo例子： [	](java_se_20191219101334784)

![image-20191218224831187](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218224831187.png)

核心代码：{{c1::

```java
ListView<String> lv = new ListView<>
  (FXCollections.observableArrayList(flagTitles));
lv.setPrefSize(400, 400);
lv.getSelectionModel().setSelectionMode(SelectionMode.MULTIPLE);

FlowPane imagePane = new FlowPane(10, 10);
BorderPane pane = new BorderPane();
pane.setLeft(new ScrollPane(lv));   
pane.setCenter(imagePane);

lv.getSelectionModel().selectedItemProperty().addListener(
  ov -> { 
    imagePane.getChildren().clear();
    for (Integer i: lv.getSelectionModel().getSelectedIndices()) {
      imagePane.getChildren().add(ImageViews[i]);
    }
  });
```

}}

### ScrollBar类 [	](java_se_20191219101334785)

![image-20191218225024959](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218225024959.png)

{{c1::![image-20191218225018747](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218225018747.png)}}

### ScrollBar类使用实例 [	](java_se_20191219101334786)

![image-20191218225150780](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218225150780.png)

ScrollBarDemo核心代码{{c1::

```java
Text text = new Text(20, 20, "JavaFX Programming");

ScrollBar hScrollBar = new ScrollBar();
ScrollBar vScrollBar = new ScrollBar();
vScrollBar.setOrientation(Orientation.VERTICAL);

    // 可以使用绑定属性的bind方法替换下列代码
    hScrollBar.valueProperty().addListener(ov ->
      text.setX(hScrollBar.getValue() * paneForText.getWidth() /
        hScrollBar.getMax()));
    
    // 可以使用绑定属性的bind方法替换下列代码
    vScrollBar.valueProperty().addListener(ov ->
      text.setY(vScrollBar.getValue() * paneForText.getHeight() /
        vScrollBar.getMax()));
```

}}


### Media类 [	](java_se_20191219101334791)

![image-20191218231926055](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218231926055.png)

{{c1::

![image-20191218231919537](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218231919537.png)}}

### MediaPlayer类 [	](java_se_20191219101334792)

![image-20191218232016072](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218232016072.png)

{{c1::![image-20191218232010780](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218232010780.png)}}

### MediaView类 [	](java_se_20191219101334793)

![image-20191218232054298](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218232054298.png)

{{c1::![image-20191218232045835](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218232045835.png)}}

### Media MediaPlayer  MediaView之间的关系 [	](java_se_20191219101334795)

{{c1::

![image-20191218232335953](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218232335953.png)

}}

### javaFX视频与音频的例子： [	](java_se_20191219101334797)

![image-20191218232438407](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191218232438407.png)

核心代码：

{{c1::

```java
String MEDIA_URL = "http://cs.armstrong.edu/liang/common/sample.mp4";
Media media = new Media(MEDIA_URL);
MediaPlayer mediaPlayer = new MediaPlayer(media);
MediaView mediaView = new MediaView(mediaPlayer);
```

}}

# 正则表达式 [	](java_se_20200604111131317)

### 元字符 [	](java_se_20200510104820590)

| 元字符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| .      | {{c1:: 句号匹配任意单个字符除了换行符。}}                    |
| [ ]    | {{c1:: 字符种类。匹配方括号内的任意字符。}}                  |
| [^ ]   | {{c1:: 否定的字符种类。匹配除了方括号里的任意字符}}          |
| *      | {{c1:: 匹配>=0个重复的在*号之前的字符。}}                    |
| +      | {{c1:: 匹配>=1个重复的+号前的字符。}}                        |
| ?      | {{c1:: 标记?之前的字符为可选.}}                              |
| {n,m}  | {{c1:: 匹配num个大括号之前的字符或字符集 (n <= num <= m).}}  |
| (xyz)  | {{c1:: 字符集，匹配与 xyz 完全相等的字符串.}}                |
| \|     | {{c1:: 或运算符，匹配符号前或后的字符.}}                     |
| \      | {{c1:: 转义字符,用于匹配一些保留的字符 `[ ] ( ) { } . * + ? ^ $ \ |`}} |
| ^      | {{c1:: 从开始行开始匹配.}}                                   |
| $      | {{c1:: 从末端开始匹配.}}                                     |
| \b     | {{c1:: 可以匹配一个单词的边界，边界是指位于 \w 和 \W 之间的位置 }} |

### 简写字符集 [	](java_se_20200510104820593)

| 简写 | 描述                                                        |
| ---- | ----------------------------------------------------------- |
| .    | {{c1:: 除换行符外的所有字符}}                               |
| \w   | {{c1:: 匹配所有字母数字，等同于 `[a-zA-Z0-9_]`}}            |
| \W   | {{c1:: 匹配所有非字母数字，即符号，等同于： `[^\w]`}}       |
| \d   | {{c1:: 匹配数字： `[0-9]`}}                                 |
| \D   | {{c1:: 匹配非数字： `[^\d]`}}                               |
| \s   | {{c1:: 匹配所有空格字符，等同于： `[\t\n\f\r\p{Z}]`}}       |
| \S   | {{c1:: 匹配所有非空格字符： `[^\s]`}}                       |
| \f   | {{c1:: 匹配一个换页符}}                                     |
| \n   | {{c1:: 匹配一个换行符}}                                     |
| \r   | {{c1:: 匹配一个回车符}}                                     |
| \t   | {{c1:: 匹配一个制表符}}                                     |
| \v   | {{c1:: 匹配一个垂直制表符}}                                 |
| \p   | {{c1:: 匹配 CR/LF（等同于 `\r\n`），用来匹配 DOS 行终止符}} |

### 前后查找 [	](java_se_20200510104820595)
| 符号 | 描述                     |
| ---- | ------------------------ |
| 正则串后虚匹配-存在 | {{c1:: `?=`  }} |
| 正则串后虚匹配-排除 | {{c1:: `?!`  }} |
| 正则串前虚匹配-存在 | {{c1:: `?<=` }} |
| 正则串前虚匹配-排除 | {{c1:: `?<!` }} |

**正则表达式**

```
\w+(?=@)
```

**结果**

**abc** @qq.com

### 回溯引用条件 [	](java_se_20200510104820597)

**正则表达式**:`(\()?abc(?(1)\))`

**字符串**:

1. (abc)
2. abc
3. (abc

**结果：**

{{c1:: 

1. **(abc)**
2. **abc**
3. (abc

}}

### 前后查找条件 [	](java_se_20200510104820600)

**正则表达式**:`\d{5}(?(?=-)-\d{4})`

**字符串**

1. 11111
2. 22222-
3. 33333-4444

**结果**

{{c1::

1. **11111**
2. 22222-
3. **33333-4444**

}}

### 回溯引用 [	](java_se_20200510104820602)

**正则表达式**:`<(h[1-6])>\w*?<\/\1>`

**字符串**

```
<h1>x</h1>
<h2>x</h2>
<h3>x</h1>
```

**结果**

{{c1::

```
<h1>x</h1> 选中
<h2>x</h2> 选中
<h3>x</h1>
```

}}

### 正则表达式替换 [	](java_se_20200510104820603)

**文本**

313-555-1234

**查找正则表达式**:{{c1::`(\d{3})(-)(\d{3})(-)(\d{4})`}}

**替换正则表达式**：{{c1:: `($1) $3-$5`}}

**结果**

(313) 555-1234

# 面向对象 [	](java_se_20201224023254138)

## 内部类 [	](java_se_20191219101334767)

### 内部类的特征： [	](java_se_20191219101334768)

+ 一个内部类被编译成{{c1::一个名为`OuterClassName$InnerClassName.class`的类}}
+ 一个内部类可以引用{{c1::定义在它所在的外部类中的数据和方法。}}
+ 和类中成员相同,内部类可以使用{{c1:可见性修饰符所定义。}}

+ 可以被定义成{{c1::static}}

### 创建一个内部类 [	](java_se_20191219101334769)

```java
//对象.new语法{{c1::
OuterClass.InnerClass innerObject = outerObject.new InnerClass();
//}}
//如果内部类是静态的，使用以下语法{{c1::
OuterClass.InnerClass innerObject = new OuterObject.InnerClass();
//}}
```

### 匿名内部类 [	](java_se_20191219101334771)

+ 匿名内部类一步实现定义内部类以及创建一个内部类实例。

+ 语法:{{c1::

  ```java 
  new SuperClassName/InterfaceName(){
    //...
  }
  //}}
  ```

+ 匿名内部类别编译成名为`OuterClassName$n.class`的类

# 多线程 [	](java_se_20200604111131318)

### 线程与进程概念 [	](java_se_20200604111131319)
+ 进程的特征：{{c1:: 独立性，动态性，并发性。}}
+ 并发性：{{c1:: 同一时刻，有多条指令在多个处理器上同时执行。}}
+ 并行性：{{c1:: 同一时刻只有一条指令执行，多个进程快速轮流执行}}
+ 多线程的优点：{{c1:: 共享内存。创建线程代价小，java内置。}}

### 有三种使用线程的方法： [	](java_se_20200604111131320)

1. {{c1:: 实现 Runnable 接口； }}
2. {{c1:: 实现 Callable 接口； }}
3. {{c1:: 继承 Thread 类。 }}

### 实现 Runnable 接口 [	](java_se_20200604111131321)

+ 需要实现接口中的 run() 方法。
  ```java
  //{{c1::
  public class MyRunnable implements Runnable {
    @Override
      public void run() {
        // ...
      }
  }
  //}}
  ```
+ 使用 Runnable 实例再创建一个 Thread 实例，然后调用 Thread 实例的 start() 方法来启动线程。
  ```java
  //{{c1::
  }}
  public static void main(String[] args) {
      MyRunnable instance = new MyRunnable();
      Thread thread = new Thread(instance);
      thread.start();
  }
  //}}
  ```

### 实现 Callable 接口 [	](java_se_20200604111131323)

+ 与 Runnable 相比，Callable 可以有返回值，返回值通过 `FutureTask` 进行封装。
  ```java
  //{{c1::
  public class MyCallable implements Callable<Integer> {
      public Integer call() {
          return 123;
      }
  }
  //}}
  ```

+ 调用

  ```java
  //{{c1::
  public static void main(String[] args) throws ExecutionException, InterruptedException {
      MyCallable mc = new MyCallable();
      FutureTask<Integer> ft = new FutureTask<>(mc);
      Thread thread = new Thread(ft);
      thread.start();
      System.out.println(ft.get());
  //}}
  }
  ```

### 获取线程名字的2个方法 [	](java_se_20200604111131324)
1. `Thread.currentThread()`:{{c1:: 总是返回当前正在执行的线程。 }}
2. `getName()`:{{c1:: Thread类的实例方法，常用于继承 Thread 类的线程。 }}

### 多线程：`Callable`接口与`Runnable`接口区别 [	](java_se_20200604111131325)
1. 返回值:{{c1:: `call()`方法可以有返回值。}}
2. 异常:{{c1:: `call()`方法可以声明抛出异常。}}

### Future接口 [	](java_se_20200604111131326)

+ `boolean cancel(boolean mayInterruptIfRunning)`：{{c1:: 试图取消关联的callable任务 }}
+ `boolean isCancelled()`：{{c1:: 判断Callable任务是否取消 }}
+ `boolean isDone()`：{{c1:: 判断Callable任务是否结束 }}
+ `V get()`：{{c1:: 返回Callable任务中的返回值 }}
+ `V get(long timeout, TimeUnit unit)`：{{c1:: 指定时间内，返回Callable任务中的返回值 }}

### 线程状态 [	](java_se_20200604111131327)

+ `isAlive()`：{{c1:: 当线程处于新建与死亡状态时，返回false }}
+ 对死亡的线程调用`start()`方法,会引发{{c1:: `IllegalThreadStateException` }}异常
+ 五种线程状态转换图
  {{c1:: ![image-20200603230326712](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200603230326712.png) }}

### 线程之间的协助 [	](java_se_20200604111131328)

+ join()：{{c1:: Thread实例方法，在线程中调用另一个线程的 join() 方法，会将当前线程挂起，而不是忙等待，直到目标线程结束。 }}
+ `wait() notify() notifyAll()`：
  1. {{c1:: Object的实例方法}}
  2. {{c1:: 只能用在同步方法或者同步控制块中使用}}
  3. {{c1:: 使用 wait() 挂起期间，线程会释放锁。这是因为，如果没有释放锁，那么其它线程就无法进入对象的同步方法或者同步控制块中，那么就无法执行 notify() 或者 notifyAll() 来唤醒挂起的线程，造成死锁。}}

### `wait() notify() notifyAll()`使用例子`before after` [	](java_se_20200604111131329)

```java
public class WaitNotifyExample {
//{{c1:: 
    public synchronized void before() {
      System.out.println("before");
        notifyAll();
    }

    public synchronized void after() {
      try {
        wait();
        } catch (InterruptedException e) {
          e.printStackTrace();
        }
        System.out.println("after");
    }
//}}
}
public static void main(String[] args) {
    ExecutorService executorService = Executors.newCachedThreadPool();
    WaitNotifyExample example = new WaitNotifyExample();
    executorService.execute(() -> example.after());
    executorService.execute(() -> example.before());
}
```

### wait() 和 sleep() 的区别 [	](java_se_20200604111131330)

1. {{c1:: wait() 是 Object 的方法，而 sleep() 是 Thread 的静态方法。}}
2. {{c1:: wait() 会释放锁，sleep() 不会。}}

### 后台线程 [	](java_se_20200604111131331)

+ 特征：{{c1:: 如何前台线程都死亡，后台线程自动死亡 }}
+ 设置指定线程成后台线程：{{c1:: Thread对象的`setDaemon(true)`方法 }}

### sleep()方法与yield()方法的区别 [	](java_se_20200604111131333)

1. 优先级：{{c1:: sleep()不理会线程的优先级 }}
2. 状态转换：{{c1:: sleep()会进入阻塞状态，yield直接进入就绪状态 }}
3. 异常：{{c1:: sleep会抛出`InterruptedException`异常，yield没有抛出异常。 }}
4. 可移植性：{{c1:: sleep()比yield()要好。 }}

### 线程的优先级设置 [	](java_se_20200604111131334)
+ Thread类提供了{{c1:: `SetPriority(int newPriority)`}}方法设置优先级。
+ Thread包含3个优先级静态常量：
    1. {{c1:: MAX_PRIORITY:值为10}}
    2. {{c1:: MIN_PRIORITY:值为1}}
    3. {{c1:: NORM_PRIORITY:值为5}}

### Java 提供了两种锁机制来控制多个线程对共享资源的互斥访问 [	](java_se_20200604111131335)

1. {{c1:: JVM 实现的 ` synchronized`。 }}
2. {{c1:: JDK 实现的 `ReentrantLock`。 }}

### synchronized同步方式 [	](java_se_20200604111131337)

1. 同步一个代码块：
    {{c1::
  ```java
  public void func() {
    synchronized (this) {
      // ...
      }
  }
  ```
  }}
2. 同步一个方法：
    {{c1::
  ```java
  public synchronized void func () {
    // ...
  }
  ```
  }}
3. 同步一个类：
    {{c1::
  ```java
  public void func() {
    synchronized (SynchronizedExample.class) {
      // ...
      }
  }
  ```
  }}
4. 同步一个静态方法：
    {{c1::
```java
  public synchronized static void fun() {
    // ...
  }
```
  }}
### `ReentrantLock`同步方式 [	](java_se_20200604111131338)
```java
//{{c1::
public class LockExample {
  private Lock lock = new ReentrantLock();
    int count;
    public void func() {
      lock.lock();
        try {
          for (int i = 0; i < 10; i++) {
            System.out.println(Thread.currentThread().getName()+":"+(++count));
            }
        } finally {
          lock.unlock(); // 确保释放锁，从而避免发生死锁。
        }
    }
}
//}}
```


### 线程不会释放同步监视器的情况 [	](java_se_20200604111131339)

1. {{c1:: 程序调用`Thread.sleep()`方法时 }}
2. {{c1:: 程序调用`Thread.yield()`方法时   }}
3. {{c1:: 调用了线程的`suspend()`方法 }}

### 使用`Conditon`控制线程通信 [	](java_se_20200604111131340)

+ 实例创建：{{c1:: `Conditoin`实例被绑定在一个Lock对象上，调用Lock对象的`newCondition()`方法即可。 }}

+ Condition类提供了3个线程通信方法
  1. {{c1:: `await()`:类似于同步监视器上的`wait()`方法，只是监视器对象变成了Lock对象。 }}
  2. {{c1:: `signal()`:类似与`notify()` }}
  3. {{c1:: `signalAll()`:类似于`notifyAll()` }}

### 使用`ReentrantLock`与`Conditon`的生产者消费者模式(实践) [	](java_se_20200604111131342)

```java
public class Account {
	// 显示定义Lock对象
	private final Lock lock = new ReentrantLock();
	// 获得指定Lock对象对应的条件变量
	private final Condition cond = lock.newCondition();
	// 账户编号
	private String accountNo;
	// 余额
	private double balance;

	// 标识账户中是否已经存款的旗标
	private boolean flag = false;

	public void draw(double drawAmount) {
    // {{c1::
		// 加锁
		lock.lock();
		try {
			// 如果账户中还没有存入存款，该线程等待
			if (!flag) {
				cond.await();
			} else {
				// 执行取钱操作
				System.out.println(Thread.currentThread().getName() + " 取钱:" + drawAmount);
				balance -= drawAmount;
				System.out.println("账户余额为：" + balance);
				// 将标识是否成功存入存款的旗标设为false
				flag = false;
				// 唤醒该Lock对象对应的其他线程
				cond.signalAll();
			}
		} catch (InterruptedException ex) {
			ex.printStackTrace();
		}
		// 使用finally块来确保释放锁
		finally {
			lock.unlock();
    }
    // }}
	}

	public void deposit(double depositAmount) {
    // {{c1::
		lock.lock();
		try {
			// 如果账户中已经存入了存款，该线程等待
			if (flag) {
				cond.await();
			} else {
				// 执行存款操作
				System.out.println(Thread.currentThread().getName() + " 存款:" + depositAmount);
				balance += depositAmount;
				System.out.println("账户余额为：" + balance);
				// 将标识是否成功存入存款的旗标设为true
				flag = true;
				// 唤醒该Lock对象对应的其他线程
				cond.signalAll();
			}
		} catch (InterruptedException ex) {
			ex.printStackTrace();
		}
		// 使用finally块来确保释放锁
		finally {
			lock.unlock();
    }
    //}}
	}
}
```

### `BlockingQueue`接口包含的方法之间的对应关系 [	](java_se_20200604111131343)

| 失败时，         | 抛出异常           | 返回false         | 阻塞线程        | 指定超时时长            |
| ---------------- | ------------------ | ----------------- | --------------- | ----------------------- |
| 队尾插入元素     | {{c1:: add(e) }}   | {{c1:: offer(e)}} | {{c1:: put(e)}} | offer(e,time,unit)}}    |
| 队头删除元素     | {{c1:: remove()}}  | {{c1:: poll()}}   | {{c1:: take()}} | {{c1::poll(time,unit)}} |
| 获取、不删除元素 | {{c1:: element()}} | {{c1:: peek()}}   | {{c1:: 无}}     | {{c1:: 无}}             |

### `BlockingQueue`接口具有的实现类 [	](java_se_20200604111131344)
+ {{c1:: `ArrayBlockingQueue` }}
+ {{c1:: `LinkedBlockingQueue`  }}
+ {{c1:: `PriorityBlockingQueue`  }}
+ {{c1:: `DelayQueue` }}
+ {{c1:: `SynchronousQueue` }}

{{c1:: ![image-20200604222338200](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20200604222338200.png) }}

### 线程组 [	](java_se_20200615060135980)

+ 作用：{{c1:: **可以批量管理线程或线程组对象，有效地对线程或线程组对象进行组织**。}}
+ 概念图:
	{{c1:: ![img](https://images2015.cnblogs.com/blog/801753/201510/801753-20151005180622909-789401754.png)}}

### 线程组的相关API [	](java_se_20200615060135982)

+ `Tread`类提供的构造器，设置新创建的线程属于哪个线程组
  + `Thread(ThreadGroup group, Runnable target)`
  + `Thread(ThreadGroup group, Runnable target, String name)`
  + `Thread(ThreadGroup group, String name)`
  + 参数：
    + `ThreadGroup group`:{{c1:: 指定线程组}}
    + `Runnable target`:{{c1:: 线程类}}
    + `String name`:{{c1:: 线程名称}}
  + 注意：{{c1:: 线程一旦加入指定线程组后，中途不能改变该线程所属组。  }}
+ `ThreadGroup`类
  + 构造器
    + `ThreadGroup(String name) `
    + `ThreadGroup(ThreadGroup parent, String name) `
    + 参数：
      + ThreadGroup parent：{{c1:: 父线程组 }}
      + String name：{{c1:: 线程组名称 }}
  + 方法：
    + `int activeCount()`：{{c1:: 活动线程的数目 }}
    + `void interrupt()`：{{c1:: 中断线程组中所有线程 }}
    + `boolean isDaemon()`：{{c1:: 是否后台线程组 }}
    + `void setDaemon(boolean daemon)`：{{c1:: 设置为后台线程组 }}
    + `void setMaxPriority(int pri)`：{{c1:: 设置线程组的最高优先级 }}

### Thread提供了两个方法来自定义（未处理的）异常处理： [	](java_se_20200615060135983)

+ `static setDefaultUncaughtExceptionHandler(UncaughtExceptionHandler eh)`:{{c1::  为线程类的所有实例设置默认的异常处理器}}
+ `setUncaughtExceptionHandler(UncaughtExceptionHandler eh)`:{{c1:: 为指定线程实例设置异常处理器}}
+ 自定义异常处理器
  ```java
    public class ExHandler
    {
      public static void main(String[] args) 
      {
        //{{c1::
        Thread.currentThread().setUncaughtExceptionHandler(
            (t,e)->{
                System.out.println(t + " 线程出现了异常：" + e);
            });
        int a = 5 / 0;
        //}}
      }
    }
  ```

## JDBC [	](java_se_20201026014023077)

### JDBC使用最简示例 [	](java_se_20201026014023079)

```java
    //加载驱动1.不灵活 不推荐，会与mysqlapi耦合，{{c1::
    //DriverManager.registerDriver(new com.mysql.jdbc.Driver());}}

    //加载驱动2{{c1::
    Class.forName("com.mysql.jdbc.Driver");
    //}}

    //获取与数据库连接的对象-Connetcion{{c1::
    connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/zhongfucheng", "root", "root");
    //}}
Druid
    //获取执行sql语句的statement对象{{c1::
    statement = connection.createStatement();
    //}}

    //执行sql语句,拿到结果集{{c1::
    resultSet = statement.executeQuery("SELECT * FROM users");
    //}}

    //遍历结果集，得到数据{{c1::
    while (resultSet.next()) {
      System.out.println(resultSet.getString(1));
        System.out.println(resultSet.getString(2));
    }
    //}}

```


### Connection对象 [	](java_se_20201026014023081)

+ 作用:{{c1:: 客户端与数据库所有的交互都是通过Connection来完成的。 }}
| 常用方法                            | 说明                                             |
| :---------------------------------- | :----------------------------------------------- |
| `createStatement()`           | {{c1:: 创建向数据库发送sql的statement对象。            }} |
| `prepareStatement(sql)`             | {{c1:: 创建向数据库发送预编译sql的PrepareSatement对象。}} |
| `prepareCall(sql)`                  | {{c1:: 创建执行存储过程的callableStatement对象         }} |
| `setAutoCommit(boolean autoCommit)` | {{c1:: 设置事务自动提交                                }} |
| `commit()`                          | {{c1:: 提交事务                                        }} |
| `rollback()`                        | {{c1:: 回滚事务                                        }} |

### Statement对象 [	](java_se_20201026014023083)

+ 作用：{{c1:: `Statement对象用于向数据库发送Sql语句，对数据库的增删改查都可以通过此对象发送sql语句完成。` }}
+ | 常用方法                    | 说明                                               |
  | :-------------------------- | :------------------------------------------------- |
  | `executeQuery(String sql)`  | {{c1:: 查询 }}                                     |
  | `executeUpdate(String sql)` | {{c1:: 增删改 }}                                   |
  | `execute(String sql)`       | {c1:: 任意sql语句都可以，但是目标不明确，很少用 }} |
  | `addBatch(String sql)`      | {{c1:: 把多条的sql语句放进同一个批处理中 }}        |
  | `executeBatch()`            | {{c1:: 向数据库发送一批sql语句执行 }}              |

### ResultSet对象 [	](java_se_20201026014023085)
+ 作用：{{c1:: ResultSet对象代表Sql语句的执行结果ResultSet对象维护了一个数据行的游标【简单理解成指针】，调用ResultSet.next()方法，可以让游标指向具体的数据行，进行获取该行的数据}}
+ | 返回类型 | 方法               | 功能描述                                                     |
  | -------- | ------------------ | ------------------------------------------------------------ |
  | `boolean`  | `next()`             | {{c1:: 将光标从当前位置向下移动一行,也就是读取下一行               }} |
  | `boolean`  | `previous()`         | {{c1:: 将光标从当前位置向上移动一行,也就是读取上一行               }} |
  | `void`     | `close()`            | {{c1:: 关闭ResultSet对象                                           }} |
  | `int`      | `getInt(int)`        | {{c1:: 以int的形式获取结果集,以当前行指定序号的值,以列的编号或者列的名字}} |
  | `int`      | `getInt(String)`     | {{c1:: 其他类型以此类推                                      }} |
  | `int`      | `getRow()`           | {{c1:: 得到光标当前所指定的行号                                    }} |
  | `boolean`  | `absolute(int row)`  | {{c1:: 光标移动到row指定的行                                       }} |
  | `boolean`  | `relative(int rows)` | {{c1:: 光标移动到相对于当前行的指定行,上下使用+和-表示             }} |

### 为什么要用PreparedStatement。 [	](java_se_20201026014023087)

1. 占位符: {{c1:: Statement对象编译SQL语句时，如果SQL语句有变量，就需要使用分隔符来隔开，如果变量非常多，就会使SQL变得非常复杂。**PreparedStatement可以使用占位符，简化sql的编写** }}
2. 预编译: {{c1:: Statement会频繁编译SQL。**PreparedStatement可对SQL进行预编译，提高效率，预编译的SQL存储在PreparedStatement对象中** }}
3. SQL注入: {{c1:: **PreparedStatement防止SQL注入**。(Statement通过分隔符`'++'`,编写永等式，可以不需要密码就进入数据库) }}

### Oracle和MySQL实现分页 [	](java_se_20201026014023089)

+ MySQL实现分页: {{c1:: `SELECT * FROM 表名  LIMIT [START], length;` }}
+ Oracle实现分页
  ```SQL
      /*
      {{c1::
        Oracle分页语法：
          @pageSize---每页显示数据行数
          @currentPage----当前所在页
      */
      SELECT *FROM (
          SELECT 列名,列名,ROWNUM rn
          FROM 表名
          WHERE ROWNUM<=(currentPage*pageSize)) temp
      WHERE temp.rn>(currentPage-1)*pageSize;
      /*}}*/
  ```
### JDBC批处理 [	](java_se_20201026050823603)
+ 作用：当需要向数据库发送一批SQL语句执行时，应避免向数据库一条条发送执行
+ Statement方式实现批处理：{{c1:: 可以发送不同类型的SQL }}
  ```java
    //{{c1::
    statement.addBatch(sql1);
    statement.addBatch(sql2);
    statement.executeBatch();
    //}}
  ```
+ PreparedStatement方式实现批处理:{{c1:: 只能发送同一句的SQL语句 }}
  ```java
    //{{c1::
    String sql = "INSERT INTO test(id,name) VALUES (?,?)";
    for (int i = 1; i <= 205; i++) {
        preparedStatement.setInt(1, i);
        preparedStatement.setString(2, (i + "zhongfucheng"));
        preparedStatement.addBatch();

        if (i %2 ==100) {
            preparedStatement.executeBatch();
            preparedStatement.clearBatch();
        }
    }
    //不是所有的%2==100，剩下的再执行一次批处理
    preparedStatement.executeBatch();
    //再清空
    preparedStatement.clearBatch();
    //}}
  ```

### JDBC处理MYSQL大文本和二进制数据 [	](java_se_20201026050823605)
+ MYSQL数据库：
  + 插入大文本：{{c1:: `preparedStatement.setCharacterStream(1, fileReader, (int) file.length());` }}
  + 读取大文本：{{c1:: ` Reader reader = resultSet.getCharacterStream("bigTest");` }}
  + 插入二进制数据：{{c1:: `preparedStatement.setBinaryStream(1, new FileInputStream(path), (int)file.length());` }}
  + 获取二进制数据：{{c1:: `InputStream inputStream = resultSet.getBinaryStream("blobtest");` }}

### JDBC获取数据库的自动主键列 [	](java_se_20201026050823607)

```java
    // {{c1::
    //获取到自动主键列的值
    resultSet = preparedStatement.getGeneratedKeys();
    if (resultSet.next()) {
        int id = resultSet.getInt(1);
        System.out.println(id);
    }
    // }}
```

### 调用数据库的存储过程 [	](java_se_20201026050823610)
+ 调用存储过程的语法：{{c1:: `{call <procedure-name>[(<arg1>,<arg2>, ...)]}` }}
+ 调用函数的语法：{{c1:: `{?= call <procedure-name>[(<arg1>,<arg2>, ...)]}` }}
+ JDBC调用：
  ```java
        //{{c1::
        connection = JdbcUtils.getConnection();
        callableStatement = connection.prepareCall("{call demoSp(?,?)}");
        callableStatement.setString(1, "nihaoa");
        //注册第2个参数,类型是VARCHAR
        callableStatement.registerOutParameter(2, Types.VARCHAR);
        callableStatement.execute();
        //获取传出参数[获取存储过程里的值]
        String result = callableStatement.getString(2);
        System.out.println(result);
        //}}
  ```
+ 如果是Output类型的：{{c1:: 那么在JDBC调用的时候是要注册的 }}

### JDBC元数据 [	](java_se_20201026050823612)

+ 是什么：{{c1:: 元数据其实就是数据库，表，列的定义信息 }}
+ 元数据对象：
  1. {{c1:: `ParameterMetaData`   --参数的元数据 }}
  2. {{c1:: `ResultSetMetaData`      --结果集的元数据 }}
  3. {{c1:: `DataBaseMetaData`      --数据库的元数据 }}

## 基本概念 [ ](java_se_20201227010951439)

### Java语言的特点 [ ](java_se_20201227010951441)

+ 特点一：面向对象
  + 两个基本概念：{{c1:: 类、对象 }}
  + 三大特性：{{c1:: 封装、继承、多态 }}
+ 特点二：健壮性
  + 内存管理机制:{{c1:: 吸收了C/C++语言的优点，但去掉了其影响程序健壮性的部分（如指针、内存的申请与释放等），提供了一个相对安全的**内存管理和访问机制** }}
+ 特点三：跨平台性
  + 跨平台性：{{c1:: 通过Java语言编写的应用程序在不同的系统平台上都可以运行。“Writeonce , Run Anywhere” }}
  + 原理：{{c1:: 只要在需要运行 java 应用程序的操作系统上，先安装一个Java虚拟机 (JVM JavaVirtual Machine) 即可。由JVM来负责Java程序在该系统中的运行。 }}

### 什么是JDK，JRE [ ](java_se_20201227010951443)
+ **JDK**: {{c1:: (Java Development Kit Java开发工具包)JDK是提供给Java开发人员使用的，其中包含了java的开发工具，也包括了JRE。所以**安装了JDK，就不用在单独安装JRE**了。 其中的开发工具：编译工具(javac.exe) 打包工具(jar.exe)等 }}
+ **JRE**: {{c1:: (Java Runtime Environment Java运行环境)包括Java虚拟机(JVM Java Virtual Machine)和Java程序所需的核心类库等，如果想要运行一个开发好的Java程序，计算机中只需要安装JRE即可。}}
+ **JDK、JRE、JVM关系图**:{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201225151034.png) }}
+ 概况：{{c1:: 使用JDK的开发工具完成的java程序，交给JRE去运行。 }}


### 注释(comment) [ ](java_se_20201227010951446)
+ Java中的注释类型：
  + 单行注释： {{c1:: `//注释文字` }}
  + 多行注释： {{c1:: `/* 注释文字 */` }}
  + 文档注释(java特有):
    + 语法：
      ```java
      //{{c1::
      /**
      @author 指定java程序的作者
      @version 指定源文件的版本
      */
      //}}
      ```
    + 作用：{{c1:: 注释内容可以被JDK提供的工具 javadoc 所解，生成一套以网页文件形式体现的该程序的说明文档。 }}

### java命令行参数
- 命令行参数类型是{{c1:: `String[]`数组； }}
- 命令行参数由JVM{{c1:: 接收用户输入并传给`main`方法； }}
- 如何解析命令行参数需要由程序自己实现。{{c1::
  ```java
  // java Main -version
  public class Main {
      public static void main(String[] args) {
          for (String arg : args) {
              if ("-version".equals(arg)) {
                  System.out.println("v 1.0");
                  break;
              }
          }
      }
  }
  ```
  }}

### classpath和jar

+ `classpath`：{{c1：： JVM通过环境变量`classpath`决定搜索`class`的路径和顺序； }}
+ 设置系统环境变量`classpath`替代方案：{{c1：： 始终建议通过`-cp`命令传入； `java -cp ./hello.jar abc.xyz.Hello` }}
+ jar包：{{c1：： jar包相当于目录，可以包含很多`.class`文件，方便下载和使用； }}
+ `MANIFEST.MF文件`：{{c1：： `MANIFEST.MF`文件可以提供jar包的信息，如`Main-Class`，这样可以直接运行jar包。 }}

## java9新特性

### 模块

+ 出现原因：{{c1:: jar只是用于存放class的容器，它并不关心class之间的依赖。 }}

+ 作用：{{c1:: 如果`a.jar`必须依赖另一个`b.jar`才能运行，那我们应该给`a.jar`加点说明啥的，让程序在编译和运行的时候能自动定位到`b.jar`，这种自带“依赖关系”的class容器就是模块。 }}

+ `java.base`模块：{{c1:: 所有的模块都直接或间接地依赖`java.base`模块，只有`java.base`模块不依赖任何模块，它可以被看作是“根模块” }}

+ 模块中的目录结构：{{c1::
  ```
  oop-module
  ├── bin
  ├── build.sh
  └── src
      ├── com
      │   └── itranswarp
      │       └── sample
      │           ├── Greeting.java
      │           └── Main.java
      └── module-info.java
  ```
  }}
  
+ 创建模块
  1. 切换到`oop-module`，在当前目录下编译所有的`.java`文件，并存放到`bin`目录下:{{c1::
    ```shell
    javac -d bin src/module-info.java src/com/itranswarp/sample/*.java
    ```
    }}
  
  2. 把bin目录下的所有class文件先打包成jar：{{c1::
    ```
    jar --create --file hello.jar --main-class com.itranswarp.sample.Main -C bin .
    ```
    }}
  3. 使用JDK自带的jmod命令把一个jar包转换成模块：{{c1::
    ```
    jmod create --class-path hello.jar hello.jmod
    ```
    }}
  
  4. 运行模块:{{c1:: `java --module-path hello.jar --module hello.world` }}
  
+ `module-info.java`文件格式：{{c1::
    ```java
    module hello.world {
      requires java.base; // 可省略
      requires java.xml;
    }
    ```
   }}

### 打包JRE

1. `jlink`命令：{{c1:: `jlink --module-path hello.jmod --add-modules java.base,java.xml,hello.world --output jre/` }}
    + 参数：
      1. {{c1::`--module-path`: 指定自己的模块 }}
      2. {{c1::`--add-modules`: 指定了我们用到的JDK模块模块 }}
      3. {{c1::`--output`: 指定输出目录 }}
2. 完成后，直接运行JRE: {{c1:: `jre/bin/java --module hello.world` }}

### 模块中类的访问权限声明
+ 如果需要使用到模块`java.xml`的一个类`javax.xml.XMLConstants`那么：{{c1:: `java.xml`的`module-info.java`中必须声明：
  ```
  module java.xml {
      exports java.xml;
      exports javax.xml.catalog;
      exports javax.xml.datatype;
      ...
  }
  ```
  }}



## 基本类型 [ ](java_se_20201227010951449)

### java变量的分类 [ ](java_se_20201227010951452)
+ 按数据类型分类：
  + 注意：{{c1:: 8种基本类型，3种引用类型 }}
  + 分类示意图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201225153202.png) }}
+ 按声明位置分类：
  + 注意：{{c1:: 成员变量 局部变量 }}
  + 分类示意图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201225153428.png) }}
  + 初始化区别：{{c1:: 局部变量除形参外，需显式初始化 }}

### java基本类型特点 [ ](java_se_20201227010951454)
+ 整数类型特点：{{c1:: Java各整数类型有固定的**表数范围**和**字段长度** }}
+ 默认浮点型常量的类型: {{c1:: Java的浮点型常量默认为double型，声明float型常量，须后加‘f’或‘F’。}}
+ 默认整型常量的类型：{{c1:: java的整型常量默认为int型，声明long型常量须后加‘l’或‘L’}}
+ char类型的运算：{{c1:: `char+char`，`char+int`——类型均提升为int，附值char变量后，输出字符编码表中对应的字符，超出范围则报错}}
+ boolean类型数据特点：{{c1:: 只允许取值true和false，在编译之后都使用java虚拟机中的int数据类型来代替 }}

### java字符型(`char`)变量的三种字面量形式： [ ](java_se_20201227010951456)
+ 字符常量:{{c1:: `'a'` }}
+ 转义字符:{{c1:: `'\n'` }}
+ Unicode值字符型常量：{{c1:: `'\uXXXX'` }}

### java基本数据类型的转换 [ ](java_se_20201227010951458)
+ 数据类型按容量大小排序为：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201225160947.png)}}
+ 自动类型转换：{{c1:: 容量小的类型自动转换为容量大的数据类型}}
+ 强制类型转换:{{c1:: 大转小时，加上强制转换符：()，但可能造成精度降低或溢出,格外要注意。 }}
+ `+=`或者`++`运算符会执行隐式类型转换：{{c1:: `s1 += 1;`相当于`s1 = (short) (s1 + 1);` }}
+ 多种类型混合运算时的转换：{{c1:: 系统首先自动将所有数据转换成容量最大的那种数据类型，然后再进行计算。 }}
+ `byte,short,char`之间:{{c1:: 不会相互转换，他们三者在计算时首先转换为int类型。}}
+ `boolean`类型:{{c1:: 不能与其它数据类型运算。}}

### 自动装箱与拆箱 [ ](java_se_20210106110103440)
+ 概念: {{c1:: **基本类型都有**对应的**包装类型**，基本类型与其对应的包装类型之间的赋值使用自动装箱与拆箱完成。 }}
+ 装箱: {{c1:: `Integer x = 2;// 装箱 调用了 Integer.valueOf(2)` }}
+ 拆箱: {{c1:: `int y = x; // 拆箱 调用了 X.intValue()` }}

### Differences between `new Integer(123)`, `Integer.valueOf(123)` and `just 123` [ ](java_se_20210106110103443)

+ `new Integer(123)`与`Integer.valueOf(123)`的区别：
  
  1. `new Integer(123)`:{{c1:: 每次都会新建一个对象； }}
  2. `Integer.valueOf(123)`:{{c1:: 会使用缓存池中的对象，多次调用会取得同一个对象的引用。 }}
  
+ valueOf()方法的实现思路：{{c1:: 就是先判断值是否在缓存池中，如果在的话就直接返回缓存池的内容。
  ```java
  public static Integer valueOf(int i) {
      if (i >= IntegerCache.low && i <= IntegerCache.high)
          return IntegerCache.cache[i + (-IntegerCache.low)];
      return new Integer(i);
  }
  ```
  }}

### java基本类型包装类中的缓存池 [ ](java_se_20210106110103447)

+ 各基本类型对应缓冲池范围：
  | 类型      | 缓存范围                           |
  | --------- | ---------------------------------- |
  | `boolean` | {{c1:: `boolean` values true and false     }} |
  | `byte`    | {{c1:: all `byte` values                   }} |
  | `short`   | {{c1:: `short` values between -128 and 127 }} |
  | `int`     | {{c1:: `int` values between -128 and 127   }} |
  | `char`    | {{c1:: `char` in the range \u0000 to \u007F}} |

+ 修改Integer缓冲池 IntegerCache 默认上限大小：{{c1:: 这个缓冲池的下界是-128，上界默认是127，但是这个上界是可调的，在启动jvm的时候，通过`-XX:AutoBoxCacheMax=<size>`来指定这个缓冲池的大小 }}

## 运算 [ ](java_se_20210106110103450)

### java对于整数，有四种表示方式： [ ](java_se_20201227010951461)

+ 二进制：{{c1:: (binary)`0,1`.以**0b**或**0B**开头。 }}
+ 十进制：{{c1:: (decimal)`0-9` }}
+ 八进制：{{c1:: (octal)`0-7` 以数字**0开头**表示。 }}
+ 十六进制：{{c1:: (hex)`0-9` `A-F` 以**0x**或**0X**开头表示。 }}

### java的6种逻辑运算符 [ ](java_se_20201227010951463)
+ `&` `|`和`&&` `||`的区别：
  + 单&时:{{c1:: 左边无论真假，右边都进行运算； }}
  + 双&时:{{c1:: 如果左边为真，右边参与运算，如果左边为假，那么右边不参与运算。 }}
  + ||表示：{{c1:: 当左边为真，右边不参与运算。 }}
+ 异或`^`与或`|`的不同之处是：{{c1:: 当左右都为true时，结果为false。 }}

### 位运算符 [ ](java_se_20201227010951466)
| 运算符 | 作用                                                         |
| ------ | ------------------------------------------------------------ |
| `<<`   | {{c1::空位补0，被移除的高位丢弃，空缺位补0。}}               |
| `>>`   | {{c1::被移位的二进制最高位是0，右移后，空缺位补0；最高位是1，空缺位补1。}} |
| `>>>`  | {{c1::被移位二进制最高位无论是0或者是1，空缺位都用0补。}}    |
| `&`    | {{c1::二进制位进行&运算，只有1&1时结果是1，否则是0;}}          |
| `^`    | {{c1::相同二进制位进行 ^ 运算，结果是0；1^1=0 , 0^0=0不相同二进制位 ^ 运算结果是1。1^0=1 , 0^1=1}} |
| `~`    | {{c1::正数取反，各二进制码按补码各位取反负数取反，各二进制码按补码各位取反}} |

### switch语句有关规则 [ ](java_se_20201227010951468)

+ switch(表达式)中表达式的值必须是下述5种类型之一：{{c1:: `byte`  `short`  `char`  `int`  `枚举 (jdk 5.0)`  `String (jdk 7.0)；`   switch 的设计初衷是对那些只有少数几个值的类型进行等值判断}}

+ 必须是常量:{{c1:: case子句中的值必须是常量，不能是变量名或不确定的表达式值； }}

+ 常量值互不相同：{{c1:: 同一个switch语句，所有case子句中的常量值互不相同； }}

+ break语句:{{c1:: 用来在执行完一个case分支后使程序跳出switch语句块；如果没有break，程序会顺序执行到switch结尾 }}

+ default子句:{{c1:: 是可任选的。同时，位置也是灵活的。当没有匹配的case时，执行default }}

## 数组 [ ](java_se_20210106110103452)

### 数组元素的默认初始化值 [ ](java_se_20210106110103456)

| 数组元素类型 | 元素默认初始值              |
| -------------- | ----------------------------- |
| `byte`         | {{c1:: `0`}}                           |
| `short`        | {{c1:: `0`}}                           |
| `int`          | {{c1:: `0`}}                           |
| `long`         | {{c1:: `0L`}}                          |
| `float`        | {{c1:: `0.0F`}}                        |
| `double`       | {{c1:: `0.0` }}                        |
| `char`         | {{c1:: `0 或写为:’\u0000’(表现为空)`}} |
| `boolean`      | {{c1:: `false`}}                       |
| `引用类型`     | {{c1:: `null``数组元素类型`}}          |

### 二维数组内存解析 [ ](java_se_20210106110103458)

+ 主要思路：java中实际上只有一维数组

+ 图示：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201230113749.png)

###  Arrays工具类的使用 [ ](java_se_20210106110103462)

| 方法                                | 作用                                             |
| ----------------------------------- | ------------------------------------------------ |
| `boolean equals(int[] a,int[] b)`   | {{c1:: 判断两个数组是否相等。 }}                 |
| `String toString(int[] a)`          | {{c1:: 输出数组信息。 }}                         |
| `void fill(int[] a,int val)`        | {{c1:: 将指定值填充到数组之中。 }}               |
| `void sort(int[] a)`                | {{c1:: 对数组进行排序。 }}                       |
| `int binarySearch(int[] a,int key)` | {{c1:: 对排序后的数组进行二分法检索指定的值。 }} |


## 字符串 [ ](java_se_20210106110103464)

### String的内部数据类型 [ ](java_se_20210106110103466)

+ 在Java8中:{{c1::String内部使用char数组存储数据。
  ```java
  public final class String
      implements java.io.Serializable, Comparable<String>, CharSequence {
      /** The value is used for character storage. */
      private final char value[];
  }
  ​```}}
  ```
  
+ 在Java9之后:{{c1::String类的实现改用byte数组存储字符串，同时使用`coder`来标识使用了哪种编码。
  ```java
  public final class String
      implements java.io.Serializable, Comparable<String>, CharSequence {
      /** The value is used for character storage. */
      private final byte[] value;
      /** The identifier of the encoding used to encode the bytes in {@code value}. */
      private final byte coder;
  }
  ```
  }}
  
+ value数组被声明为final，这表明：{{c1:: value数组初始化之后就不能再引用其它数组。并且String内部没有改变value数组的方法，因此可以保证String不可变。 }}

  

### 一个不变类具有以下特点：

1. {{c1:: 定义class时使用`final`，无法派生子类； }}
2. {{c1:: 每个字段使用`final`，保证创建实例后无法修改任何字段。 }}

### record关键字定义不变类
+ 仔细观察`Point`的定义：`public record Point(int x, int y) {}`
+ 相当于以下代码：
  ```java
  //{{c1::
  public final class Point extends Record {
    private final int x;
    private final int y;

    public Point(int x, int y) {
      this.x = x;
      this.y = y;
    }

    public int x() {
      return this.x;
    }

    public int y() {
      return this.y;
    }

    public String toString() {
      return String.format("Point[x=%s, y=%s]", x, y);
    }

    public boolean equals(Object o) {
      ...
    }
    public int hashCode() {
      ...
    }
  }
  //}}
  ```
+ 给Point的构造方法加上检查逻辑:
  ```java
  //{{c1::
  public record Point(int x, int y) {
    public Point {
        if (x < 0 || y < 0) {
            throw new IllegalArgumentException();
        }
    }
  }
  //}}
  ```
+ 编译器最终生成的构造方法如下：
  ```java
  //{{c1::
  public final class Point extends Record {
      public Point(int x, int y) {
          // 这是我们编写的Compact Constructor:
          if (x < 0 || y < 0) {
              throw new IllegalArgumentException();
          }
          // 这是编译器继续生成的赋值代码:
          this.x = x;
          this.y = y;
      }
      ...
  }
  //}}
  ```
  ```java
  //{{c1::
  public final class Point extends Record {
      public Point(int x, int y) {
          // 这是我们编写的Compact Constructor:
          if (x < 0 || y < 0) {
              throw new IllegalArgumentException();
          }
          // 这是编译器继续生成的赋值代码:
          this.x = x;
          this.y = y;
      }
      ...
  }
  //}}
  ```
+ 可以添加静态方法:
  ```java
  //{{c1::
  public record Point(int x, int y) {
      public static Point of() {
          return new Point(0, 0);
      }
      public static Point of(int x, int y) {
          return new Point(x, y);
      }
  }
  //}}
  ```
### String不可变的好处 [ ](java_se_20210106110103468)

**1. 可以缓存 hash 值**:{{c1:: 因为 String 的 hash 值经常被使用，例如 String 用做 HashMap 的 key。不可变的特性可以使得 hash 值也不可变，因此只需要进行一次计算。}}
**2. String Pool 的需要**:{{c1:: 如果一个 String 对象已经被创建过了，那么就会从 String Pool 中取得引用。只有 String 是不可变的，才可能使用 String Pool。![](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191210004132894.png)}}

**3. 安全性**:{{c1:: String 经常作为参数，String 不可变性可以保证参数不可变。例如在作为网络连接参数的情况下如果 String 是可变的，那么在网络连接过程中，String 被改变，改变 String 的那一方以为现在连接的是其它主机，而实际情况却不一定是。}}
**4. 线程安全**:{{c1:: String 不可变性天生具备线程安全，可以在多个线程中安全地使用。}}

### String, StringBuffer and StringBuilder区别 [ ](java_se_20210106110103471)

1. **可变性角度** 
- {{c1:: `String` 不可变 }}
- {{c1:: `StringBuffer` 和 `StringBuilder` 可变 }}
2. **线程安全角度**  
- {{c1:: `String` 不可变，因此是线程安全的 }}
- {{c1:: `StringBuilder` 不是线程安全的 }}
- {{c1:: `StringBuffer` 是线程安全的，内部使用 `synchronized` 进行同步 }}

### String Pool [ ](java_se_20210106110103474)

+ 概念：{{c1:: 字符串常量池（String Pool）保存着所有字符串字面量（literal strings），这些字面量在**编译时期**就确定。不仅如此，还可以使用 String 的 intern() 方法在运行过程将字符串添加到 String Pool 中。}}

+ 当一个字符串调用 intern() 方法时:{{c1:: 如果 String Pool 中已经存在一个字符串和该字符串值相等（使用 equals() 方法进行确定），那么就会返回 String Pool 中字符串的引用；否则，就会在 String Pool 中添加一个新的字符串，并返回这个新字符串的引用。}}

+ 示例：

  ```java
  //{{c1::
  String s1 = new String("aaa");
  String s2 = new String("aaa");
  System.out.println(s1 == s2);           // false
  String s3 = s1.intern();
  String s4 = s2.intern();
  System.out.println(s3 == s4);           // true
  
  String s5 = "bbb";
  String s6 = "bbb";
  System.out.println(s5 == s6);  // true
  //}}
  ```

### 调用`new String("abc")`会发生什么？ [ ](java_se_20210106110103477)
+ 原理解析：
  + {{c1:: 使用这种方式一共会创建两个字符串对象（前提是 String Pool 中还没有 "abc" 字符串对象）。 }}
  + {{c1:: "abc" 属于字符串字面量，因此编译时期会在 String Pool 中创建一个字符串对象，指向这个 "abc" 字符串字面量； }}
  + {{c1:: 而使用 new 的方式会在堆中创建一个字符串对象。 }}
  
+ `String(String original)`构造函数的源码:{{c1::
  
  ```java
  public String(String original) {
      this.value = original.value;
      this.hash = original.hash;
  }
  ```
}}

### StringJoiner

+ 作用：高效拼接字符串
+ 例，使用`StringJoiner`构造一个`SELECT`语句：
  ```java
  	public static void main(String[] args) {
  		String[] fields = { "name", "position", "salary" };
  		String table = "employee";
  		String select = buildSelectSql(table, fields);
  		System.out.println("SELECT name, position, salary FROM employee".equals(select) ? "测试成功" : "测试失败");
  	}
  
  	static String buildSelectSql(String table, String[] fields) {
      //{{c1::
          StringJoiner sj=new StringJoiner(", ","SELECT "," FROM "+table);
          for(String field:fields){
          sj.add(field);
          return sj.toString();
      //}}
  	}
  ```
  
+ `String.join()`：{{c1:: 在不需要指定“开头”和“结尾”的时候，用String.join()更方便
  ```java
  String[] names = {"Bob", "Alice", "Grace"};
  var s = String.join(", ", names);
  ```
  }}

## 关键字 [ ](java_se_20210106110103480)

### final关键字：分别作用于变量、方法、类的特点 [ ](java_se_20210106110103482)
1. **变量**: {{c1:: 声明数据为常量，可以是编译时常量，也可以是在运行时被初始化后不能被改变的常量。 }}
    - 对于基本类型:{{c1:: final 使数值不变； }}
    - 对于引用类型:{{c1:: final 使引用不变，也就不能引用其它对象，但是被引用的对象本身是可以修改的。 }}
2. **方法**: {{c1:: 声明方法不能被子类重写。 }}
    + 关于private方法：{{c1:: private 方法隐式地被指定为 final，如果在子类中定义的方法和基类中的一个 private 方法签名相同，此时子类的方法不是重写基类方法，而是在子类中定义了一个新的方法。 }}
3. **类**: {{c1:: 声明类不允许被继承。 }}

### static关键字:作用于类各成员的特点 [ ](java_se_20210106110103485)

+ 静态变量：{{c1:: 又称为类变量，也就是说这个变量属于类的。 }}

+ 静态方法：{{c1:: 在类加载的时候就存在了，不依赖于任何实例，不能是抽象方法 }}
  
  + `this`和`super`关键字：{{c1:: 静态方法中不能有this和super关键字，因此这两个关键字与具体对象关联。 }}
  
+ 静态语句块：{{c1:: 静态语句块在类初始化时运行一次。
  ```java
  public class A {
      static {
          System.out.println("123");
      }
  
      public static void main(String[] args) {
          A a1 = new A();
          A a2 = new A();
      }
  }
  ```
  ```
  123
  ```
  }}

+ 静态内部类：{{c1:: 非静态内部类依赖于外部类的实例，而静态内部类不需要 }}

+ 静态导包：{{c1::`import static com.xxx.ClassName.*`  例如打印操作System.out.println(…);就可以将其写入一个静态方法print(…)}}

+ 存在继承的情况下，`静态变量，静态语句块，实例变量，普通语句块，构造函数`初始化顺序为：
  1. {{c1:: 父类（静态变量、静态语句块） }}
  2. {{c1:: 子类（静态变量、静态语句块） }}
  3. {{c1:: 父类（实例变量、普通语句块） }}
  4. {{c1:: 父类（构造函数） }}
  5. {{c1:: 子类（实例变量、普通语句块） }}
  6. {{c1:: 子类（构造函数） }}

## Object中的通用实例方法 [ ](java_se_20210106110103487)

### 对象的等价关系 [ ](java_se_20210106110103490)

+ 两个对象具有等价关系，需要满足以下五个条件：
  + **自反性**：{{c1:: 
    ```java
    x.equals(x); // true
    ```
    }}

  + **对称性**：{{c1:: 
    ```java
    x.equals(y) == y.equals(x); // true
    ```
    }}

  + **传递性**：{{c1:: 
    ```java
    if (x.equals(y) && y.equals(z))
        x.equals(z); // true;
    ```
    }}
    
  + **一致性**：{{c1:: 多次调用 equals() 方法结果不变
    ```java
    x.equals(y) == x.equals(y); // true
    ```
    }}
    
  + **与null的比较**：{{c1:: 对任何不是 null 的对象 x 调用 x.equals(null) 结果都为 false
    
    ```java
    x.equals(null); // false;
    ```
    }}
+ 等价与相等
  - 对于基本类型，== 判断：{{c1:: 两个值是否相等，基本类型没有 equals() 方法。 }}
  - 对于引用类型，== 判断：{{c1:: 两个变量是否引用同一个对象，而 equals() 判断引用的对象是否等价。 }}

### Object的实例方法：重写`equals()`思路 [ ](java_se_20210106110103494)

1. {{c1:: 检查是否为同一对象引用：`if (this == o) return true;` }}
2. {{c1:: 检查是否是同一类型：`if (this == o) return true;` }}
3. {{c1:: 转型 }}
4. {{c1:: 判断每个关键域是否相等 }}
- 例：{{c1::
  ```
  public class EqualExample {
  
      private int x;
      private int y;
      private int z;
  
      public EqualExample(int x, int y, int z) {
          this.x = x;
          this.y = y;
          this.z = z;
      }
  
      @Override
      public boolean equals(Object o) {
          if (this == o) return true;
          if (o == null || getClass() != o.getClass()) return false;
  
          EqualExample that = (EqualExample) o;
  
          if (x != that.x) return false;
          if (y != that.y) return false;
          return z == that.z;
      }
  }
  ```
  }}

### Object的实例方法：`hashCode()` [ ](java_se_20210106110103497)

+ 与`equals()`实例方法的关系
  + 哈希值与等价：{{c1:: hashCode() 返回哈希值，而 equals() 是用来判断两个对象是否等价 }}
  + 哈希值具有随机性：{{c1:: **等价的两个对象散列值一定相同**，但是**散列值相同的两个对象不一定等价**，这是因为计算哈希值具有随机性，两个**值不同**的对象可能**计算出相同**的哈希值。 }}
  + 同时存在：{{c1:: 在覆盖 equals() 方法时应当总是覆盖 hashCode() 方法，保证等价的两个对象哈希值也相等。 }}

+ 与HashSet和HashMap等类的关系:{{c1:: 因此要将对象添加到这些集合类中，需要让对应的类实现hashCode()方法,如果没有实现 hashCode() 方法，可能会造成等价而哈希值不同，最终导致集合添加了两个等价的对象。 }}

### Object的实例方法：`toString()` [ ](java_se_20210106110103500)
+ 作用：{{c1:: 默认返回`ToStringExample@4554617c`这种形式，其中 @ 后面的数值为 散列码的无符号十六进制表示。 }}

### Object的实例方法：`clone()` [ ](java_se_20210106110103502)

+ 作用：{{c1:: clone() 是 Object 的 protected 方法，它不是 public，一个类不显式去重写 clone()，其它类就不能直接去调用该类实例的 clone() 方法。 }}
+ 与Cloneable接口关系：{{c1:: 如果一个类没有实现 Cloneable 接口又调用了 clone() 方法，就会抛出 CloneNotSupportedException。 }}

+ clone() 的替代方案：{{c1:: 最好不要去使用 clone()，可以使用拷贝构造函数或者拷贝工厂来拷贝一个对象。 }}

## 工具类

### BigInteger

+ 作用：{{c1:: `BigInteger`用于表示任意大小的整数}}
+ 不可变：{{c1:: `BigInteger`是不变类，并且继承自`Number`}}
+ 将`BigInteger`转换成基本类型时可使用：{{c1:: `longValueExact()`等方法保证结果准确}}

### BigDecimal
+ 作用：{{c1:: 表示一个任意大小且精度完全准确的浮点数。 }}
+ `BigDecimal`的比较：{{c1:: 总是使用`compareTo()`比较两个`BigDecimal`的值，不要使`用equals()`！ }}
+ 小数位数：{{c1:: `BigDecimal`用`scale()`表示小数位数 }}
+ 去掉末尾0：{{c1:: `BigDecimal`的`stripTrailingZeros()`方法，可以将一个`BigDecimal`格式化为一个相等的，但去掉了末尾`0`的`BigDecimal` }}
+ 如果一个`BigDecimal`的`scale()`返回负数:{{c1:: 例如，-2，表示这个数是个整数，并且末尾有2个0。 }}
+ **四舍五入**与**直接截断**:
  ```java
  //{{c1::
    BigDecimal d1 = new BigDecimal("123.456789");
    BigDecimal d2 = d1.setScale(4, RoundingMode.HALF_UP); // 四舍五入，123.4568
    BigDecimal d1 = new BigDecimal("123.456");
    BigDecimal d2 = new BigDecimal("23.456789");
    BigDecimal d3 = d1.divide(d2, 10, RoundingMode.HALF_UP); // 保留10位小数并四舍五入
    BigDecimal d4 = d1.divide(d2); // 报错：ArithmeticException，因为除不尽
  //}}
  ```

### Java提供的常用工具类有：
+ `Math`：{{c1:: 数学计算 }}
+ `Random`：{{c1:: 生成伪随机数 }}
+ `SecureRandom`：{{c1:: 生成安全的随机数 }}

## 继承 [ ](java_se_20210106110103504)

### 访问权限修饰符 [ ](java_se_20210106110103507)

+ 修饰对象：{{c1:: 类 与 类成员 }}

+ 4种访问权限从大到小：{{c1:: `public > protected > default(包访问权限) > private` }}
+ protected只用于修饰成员：{{c1:: 表示在继承体系中成员对于子类可见，但是这个访问修饰符对于类没有意义。 }}
+ 重写后访问权限：{{c1:: 如果子类的方法重写了父类的方法，那么子类中该方法的访问级别不允许低于父类的访问级别。这是为了满足里氏替换原则。 }}
+ 字段决不能是公有的：{{c1:: AccessExample 拥有 `String id` 公有字段，如果在未来某个时刻，我们想要使用 `int id` 字段，那么就需要修改所有的客户端代码，而使用getId()与setId()即可避免该问题。 }}

### 抽象类与接口 [ ](java_se_20210106110103511)

- 抽象类
  - 定义：{{c1:: 抽象类和抽象方法都使用 abstract 关键字进行声明。如果一个类中包含抽象方法，那么这个类必须声明为抽象类。}}
  - 抽象类和普通类最大的区别：{{c1:: 抽象类不能被实例化，只能被继承。 }}
- 接口
  - 定义：{{c1:: 接口是抽象类的延伸，在 Java 8 之前，它可以看成是一个完全抽象的类，也就是说它不能有任何的方法实现。 }}
  - java8支持默认方法的原因：{{c1:: 从 Java 8 开始，接口也可以拥有默认的方法实现，这是因为不支持默认方法的接口的维护成本太高了。在 Java 8 之前，如果一个接口想要添加新的方法，那么要修改所有实现了该接口的类，让它们都实现新增的方法。}}
  - 接口各成员的可见性：{{c1:: 接口的成员（字段 + 方法）默认都是 public 的，并且不允许定义为 private 或者 protected。从 Java 9 开始，允许将方法定义为 private，这样就能定义某些复用的代码又不会把方法暴露出去。 }}
  - 接口中的`static`  `final`: {{c1:: 接口的字段默认都是 static 和 final 的 }}

### 抽象类与接口比较 [ ](java_se_20210106110103514)

- `IS-A`与`LIKE-A` ：{{c1:: 从设计层面上看，抽象类提供了一种 IS-A 关系，需要满足里式替换原则，即子类对象必须能够替换掉所有父类对象。而接口更像是一种 LIKE-A 关系，它只是提供一种方法实现契约，并不要求接口和实现接口的类具有 IS-A 关系。 }}
- 单继承：{{c1:: 从使用上来看，一个类可以实现多个接口，但是不能继承多个抽象类。 }}
- `static final`: {{c1:: 接口的字段只能是 static 和 final 类型的，而抽象类的字段没有这种限制。 }}
- `public`: {{c1:: 接口的成员只能是 public 的，而抽象类的成员可以有多种访问权限。 }}

### 为了满足里式替换原则，重写有以下三个限制： [ ](java_se_20210106110103516)

1. {{c1:: 子类方法的访问权限必须大于等于父类方法； }}
2. {{c1:: 子类方法的返回类型必须是父类方法返回类型或为其子类型。 }}
3. {{c1:: 子类方法抛出的异常类型必须是父类抛出异常类型或为其子类型。 }}
+ `@Override`：{{c1:: 可以让编译器帮忙检查是否满足上面的三个限制条件。 }}

### 类继承链中方法调用的顺序 [ ](java_se_20210106110103519)

+ 概况：{{c1:: 在调用一个方法时，先从本类中查找看是否有对应的方法，如果没有再到父类中查看，看是否从父类继承来。否则就要对参数进行转型，转成父类之后看是否有对应的方法。}}
+ 总的来说，方法调用的优先级为（注意`.`前面与后面转型目标）： 
  + {{c1:: `this.func(this)` }}
  + {{c1:: `super.func(this)` }}
  + {{c1:: `this.func(super)` }}
  + {{c1:: `super.func(super)` }}

### 重写与重载 [ ](java_se_20210106110103523)

+ 重写：{{c1:: 指子类实现了一个与父类在方法**声明上完全相同**的一个方法。 }}
+ 重载：{{c1:: 存在于同一个类中，指一个方法与已经存在的方法名称上相同，但是**参数类型、个数、顺序**至少有一个不同。 }}
  + 注意：{{c1:: 返回值不同，其它都相同不算是重载 }}

## 枚举类

### 和`int`定义的常量相比，使用`enum`定义枚举有如下好处：

- 首先，`enum`常量本身带有类型信息，即`Weekday.SUN`类型是`Weekday`，编译器会自动检查出类型错误。

  ```
  int day = 1;
  if (day == Weekday.SUN) { // Compile error: bad operand types for binary operator '=='
  }
  ```

- 不同类型的枚举不能互相比较或者赋值，因为类型不符

### enum实例直接使用`==`比较

+ 原因：{{c1::  这是因为`enum`类型的每个常量在 JVM中只有一个唯一实例，所以可以直接用`==`比较。`==`比较的是两个引用类型的变量是否是同一个对象。因此，引用类型比较，要始终使用`equals()`方法.}}

### 枚举类特点

+ 与普通类的关系：{{c1:: Java使用`enum`定义枚举类型，它被编译器编译为`final class Xxx extends Enum { … }`； }}
+ `name()`：{{c1::  通过`name()`获取常量定义的字符串，注意不要使用`toString()`； }}
+ `ordinal()`：{{c1::  通过`ordinal()`返回常量定义的顺序（无实质意义）； }}
+ 定义成员：{{c1:: 可以为`enum`编写构造方法、字段和方法 }}
+ 构造方法：{{c1:: `enum`的构造方法要声明为`private`，字段强烈建议声明为`final`； }}
+ `switch`：{{c1:: `enum`适合用在`switch`语句中。 }}

## 异常
### java的异常类体系
+ 图：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210107155809.png) }}

### java常见异常类

+ `Error`：{{c1:: 表示严重的错误 }}
  + `OutOfMemoryError`：{{c1:: 内存耗尽 }}
  + `NoClassDefFoundError`：{{c1:: 无法加载某个Class }}
  + `StackOverflowError`：{{c1:: 栈溢出 }}
+ `Exception`：{{c1:: 运行时的错误，它可以被捕获并处理理。 }}
  + `NumberFormatException`：{{c1:: 数值类型的格式错误 }}
  + `FileNotFoundException`：{{c1:: 未找到文件 }}
  + `SocketException`：{{c1:: 读取网络失败 }}
  + `NullPointerException`：{{c1:: 对某个null的对象调用方法或字段 }}
  + `IndexOutOfBoundsException`：{{c1:: 数组索引越界 }}

### 必须捕获的异常与不需要捕获的异常
+ 必须捕获的异常：{{c1:: 包括`Exception`及其子类，但不包括`RuntimeException`及其子类，这种类型的异常称为`Checked Exception`。 }}
+ 不需要捕获的异常：{{c1:: 包括`Error`及其子类，`RuntimeException`及其子类 }}
+ 注意：{{c1:: 编译器对RuntimeException及其子类不做强制捕获要求，不是指应用程序本身不应该捕获并处理RuntimeException。是否需要捕获，具体问题具体分析。 }}

## Java IO

### Java 的 I/O 大概可以分成以下几类：

- 磁盘操作：{{c1:: `File` }}
- 字节操作：{{c1:: `InputStream` 和 `OutputStream` }}
- 字符操作：{{c1:: `Reader` 和 `Writer` }}
- 对象操作：{{c1:: `Serializable` }}
- 网络操作：{{c1:: `Socket` }}
- 新的输入/输出：{{c1:: `NIO` }}

### 磁盘操作：File类

+ 作用：{{c1:: File 类可以用于表示文件和目录的信息，但是它不表示文件的内容。 }}

+ 代替方案：{{c1:: 从 Java7 开始，可以使用 Paths 和 Files 代替 File。 }}

+ 使用例：递归地列出一个目录下所有文件
  ```java
  //{{c1::
  public static void listAllFiles(File dir) {
      if (dir == null || !dir.exists()) {
          return;
      }
      if (dir.isFile()) {
          System.out.println(dir.getName());
          return;
      }
      for (File file : dir.listFiles()) {
          listAllFiles(file);
      }
  }
  //}}
  ```

### 字节操作： 使用`InputStream` 和 `OutputStream`实现文件复制

```java
//{{c1::
public static void copyFile(String src, String dist) throws IOException {
    FileInputStream in = new FileInputStream(src);
    FileOutputStream out = new FileOutputStream(dist);
    byte[] buffer = new byte[20 * 1024];
    int cnt;

    // read() 最多读取 buffer.length 个字节
    // 返回的是实际读取的个数
    // 返回 -1 的时候表示读到 eof，即文件尾
    while ((cnt = in.read(buffer, 0, buffer.length)) != -1) {
        out.write(buffer, 0, cnt);
    }

    in.close();
    out.close();
  //}}
}
```

### Java I/O中的装饰者模式

- Java I/O 使用了装饰者模式来实现。以 InputStream 为例：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/9709694b-db05-4cce-8d2f-1c8b09f4d921.png) }}
- `DataInputStream` ：{{c1:: 提供了对更多数据类型进行输入的操作 }}
- `BufferedInputStream` ：{{c1:: 为 FileInputStream 提供缓存的功能。 }}

## 字符操作

### 编码与解码

+ 各编码方式的中英文占比：
  + GBK 编码中:{{c1:: 中文字符占 2 个字节，英文字符占 1 个字节； }}
  + UTF-8 编码中:{{c1:: 中文字符占 3 个字节，英文字符占 1 个字节； }}
  + UTF-16be 编码中:{{c1:: 中文字符和英文字符都占 2 个字节。 }}
+ Java 的内存编码使用：{{c1:: 双字节编码UTF-16be，双字节编码的好处是可以使用一个 char 存储中文和英文}}

- String类的编码与解码：{{c1::

  ```java
  String str1 = "中文";
  //注意：getBytes() 的默认编码方式与平台有关，一般为 UTF-8。
  byte[] bytes = str1.getBytes("UTF-8");
  String str2 = new String(bytes, "UTF-8");
  System.out.println(str2);
  ```
  
  }}



### Reader 与 Writer

+ 作用：{{c1:: 不管是磁盘还是网络传输，最小的存储单元都是字节，而不是字符。但是在程序中操作的通常是字符形式的数据，因此需要提供对字符进行操作的方法。 }}
- `InputStreamReader` ：{{c1:: 实现从字节流解码成字符流； }}

- `OutputStreamWriter` ：{{c1:: 实现字符流编码成为字节流。 }}

- 例:实现逐行输出文本文件的内容
  ```java
  public static void readFileContent(String filePath) throws IOException {
  //{{c1::
      FileReader fileReader = new FileReader(filePath);
      BufferedReader bufferedReader = new BufferedReader(fileReader);
  
      String line;
      while ((line = bufferedReader.readLine()) != null) {
          System.out.println(line);
      }
  
      // 装饰者模式使得 BufferedReader 组合了一个 Reader 对象
      // 在调用 BufferedReader 的 close() 方法时会去调用 Reader 的 close() 方法因此只要一个 close() 调用即可
      bufferedReader.close();
  //}}
  }
  ```

## 对象操作

### 序列化

+ 作用：{{c1:: 序列化就是将一个对象转换成字节序列，方便存储和传输。 }}
+ 实现：
  - 序列化核心方法：{{c1:: `ObjectOutputStream.writeObject()` }}
  
  - 反序列化核心方法：{{c1:: `ObjectInputStream.readObject()` }}
  
    ```java
    //{{c1::
    public static void main(String[] args) throws IOException, ClassNotFoundException {
    
        A a1 = new A(123, "abc");
        String objectFile = "file/a1";
    
        ObjectOutputStream objectOutputStream = new ObjectOutputStream(new FileOutputStream(objectFile));
        objectOutputStream.writeObject(a1);
        objectOutputStream.close();
    
        ObjectInputStream objectInputStream = new ObjectInputStream(new FileInputStream(objectFile));
        A a2 = (A) objectInputStream.readObject();
        objectInputStream.close();
        System.out.println(a2);
    }
    //}}
    ```
  
+ 不会对静态变量进行序列化：{{c1:: 因为序列化只是保存对象的状态，静态变量属于类的状态。 }}
          + Serializable接口：{{c1:: 序列化的类需要实现 Serializable 接口，它只是一个标准，没有任何方法需要实现，但是如果不去实现它的话而进行序列化，会抛出异常。 }}

## java容器

