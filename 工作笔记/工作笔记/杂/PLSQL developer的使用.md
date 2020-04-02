# PLSQL Developer软件使用大全

[![wps4B06.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302233924391-1085785292.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233922157-623698225.jpg)

[![wps4B07.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302233928438-2130658850.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233926548-1736351990.jpg) 

# **第一章 PLSQL Developer特性**

PL/SQL Developer是一个集成开发环境，专门面向Oracle数据库存储程序单元的开发。如今，有越来越多的商业逻辑和应用逻辑转向了Oracle Server，因此，PL/SQL编程也成了整个开发过程的一个重要组成部分。PL/SQL Developer侧重于易用性、代码品质和生产力，充分发挥Oracle应用程序开发过程中的主要优势。

PL/SQL Developer主要特性：

PL/SQL编辑器，功能强大——该编辑器具有语法加强、SQL和PL/SQL帮助、对象描述、代码助手、编译器提示、PL/SQL完善、代码内容、代码分级、浏览器按钮、超链接导航、宏库等许多智能特性，能够满足要求性最高的用户需求。当您需要某个信息时，它将自动出现，至多单击即可将信息调出。

集成调试器（要求Oracle 7.3.4或更高）——该调试器提供您所需要的全部特性：跳入（Step In）、跳过（Step Over）、跳出（Step Out）、异常时停止运行、断点、观察和设置变量、观察全部堆栈等。基本能够调试任何程序单元（包括触发器和Oracle8 对象类型），无需作出任何修改。

PL/SQL完善器——该完善器允许您通过用户定义的规则对SQL和PL/SQL代码进行规范化处理。在编译、保存、打开一个文件时，代码将自动被规范化。该特性提高了您编码的生产力，改善了PL/SQL代码的可读性，促进了大规模工作团队的协作。

SQL 窗口——该窗口允许您输入任何SQL语句，并以栅格形式对结果进行观察和编辑，支持按范例查询模式，以便在某个结果集合中查找特定记录。另外，还含有历史缓存，您可以轻松调用先前执行过的SQL语句。该SQL编辑器提供了同PL/SQL编辑器相同的强大特性。

命令窗口——使用PL/SQL Developer 的命令窗口能够开发并运行SQL脚本。该窗口具有同SQL*Plus相同的感观，另外还增加了一个内置的带语法加强特性的脚本编辑器。这样，您就可以开发自己的脚本，无需编辑脚本/保存脚本/转换为SQL*Plus/运行脚本过程，也不用离开PL/SQL Developer集成开发环境。

报告——PL/SQL Developer提供内置的报告功能，您可以根据程序数据或Oracle字典运行报告。PL/SQL Developer本身提供了大量标准报告，而且您还可以方便的创建自定义报告。自定义报告将被保存在报告文件中，进而包含在报告菜单内。这样，运行您自己经常使用的自定义报告就非常方便。

您可以使用Query Reporter免费软件工具来运行您的报告，不需要PL/SQL Developer，直接从命令行运行即可。

工程——PL/SQL Developer内置的工程概念可以用来组织您的工作。一个工程包括源文件集合、数据库对象、notes和选项。PL/SQL Developer允许您在某些特定的条目集合范围之内进行工作，而不是在完全的数据库或架构之内。这样，如果需要编译所有工程条目或者将工程从某个位置或数据库移动到其他位置时，所需工程条目的查找就变得比较简单，

To-Do条目——您可以在任何SQL或PL/SQL源文件中使用To-Do条目快速记录该文件中那些需要进行的事项。以后能够从To-Do列表中访问这些信息，访问操作可以在对象层或工程层进行。

对象浏览器——可配置的树形浏览能够显示同PL/SQL开发相关的全部信息，使用该浏览器可以获取对象描述、浏览对象定义、创建测试脚本以便调试、使能或禁止触发器或约束条件、重新编译不合法对象、查询或编辑表格、浏览数据、在对象源中进行文本查找、拖放对象名到编辑器等。

此外，该对象浏览器还可以显示对象之间的依存关系，您可以递归的扩展这些依存对象（如包参考检查、浏览参考表格、图表类型等）。

性能优化——使用PL/SQL Profiler，可以浏览每一执行的PL/SQL代码行的时序信息（Oracle8i或更高），从而优化您SQL和PL/SQL的代码性能。

更进一步，您还可以自动获取所执行的SQL语句和PL/SQL程序统计信息。该统计信息包括CPU使用情况、块I/O、记录I/O、表格扫描、分类等。

HTML指南——Oracle目前支持HTML格式的在线指南。您可以将其集成到PL/SQL Developer工作环境中，以便在编辑、编译出错或运行时出错时提供内容敏感帮助。

非PL/SQL对象——不使用任何SQL，您就可以对表格、序列、符号、库、目录、工作、队列、用户和角色进行浏览、创建和修改行为。PL/SQL Developer提供了一个简单易用的窗体，只要将信息输入其中，PL/SQL Developer就将生成相应的SQL，从而创建或转换对象。

模板列表——PL/SQL Developer的模板列表可用作一个实时的帮助组件，协助您强制实现标准化。只要点击相应的模板，您就可以向编辑器中插入标准的SQL或PL/SQL代码，或者从草稿出发来创建一个新程序。

查询构建器——图形化查询构建器简化了新选择语句的创建和已有语句的修改过程。只要拖放表格和视窗，为区域列表选择专栏，基于外部键约束定义联合表格即可。

比较用户对象——对表格定义、视图、程序单元等作出修改后，将这些修改传递给其他数据库用户或检查修改前后的区别将是非常有用的。这也许是一个其他的开发环境，如测试环境或制作环境等。而比较用户对象功能则允许您对所选对象进行比较，将不同点可视化，并运行或保存应用必要变动的SQL脚本。

导出用户对象——该工具可以导出用户所选对象的DDL（数据定义语言）语句。您可以方便的为其他用户重新创建对象，也可以保存文件作为备份。

工具——PL/SQL Developer为简化日常开发专门提供了几种工具。使用这些工具，您可以重新编译全部不合法对象、查找数据库源中文本、导入或导出表格、生成测试数据、导出文本文件、监控dbms_alert和dbms_pipe事件、浏览会话信息等。

授权——大多数开发环境中，您不希望所有数据库都具备PL/SQL Developer的全部功能性。例如，数据库开发中您可以允许PL/SQL Developer的全部功能性，而数据库测试中您可以仅允许数据查询/编辑和对象浏览功能，而数据库制作中您甚至根本不希望PL/SQL Developer访问。利用PL/SQL Developer授权功能，您可以方便的定义特定用户或规则所允许使用的功能。

插件扩展——可以通过插件对PL/SQL Developer功能进行扩展。Add-ons页面提供插件可以免费下载。Allround Automations或其他用户均可提供插件（如版本控制插件或plsqldoc插件）。如果您具备创建DLL的编程语言，您还可以自己编写插件。

多线程IDE——PL/SQL Developer是一个多线程IDE。这样，当SQL查询、PL/SQL程序、调试会话等正在运行时，您依然可以继续工作。而且，该多线程IDE还意味着出现编程错误时不会中止：您在任何时间都可以中断执行或保存您的工作。

易于安装——不同于SQL*Net，无需中间件，也无需数据库对象安装。只需点击安装程序按钮，您就可以开始安装从而使用软件了。

 

 

# **第二章 PLSQL Developer配置**

 

## **2.1   记住密码**   

   这是个有争议的功能，因为记住密码会给带来数据安全的问题。但假如是开发用的库，密码甚至可以和用户名相同，每次输入密码实在没什么意义，可以考虑让PLSQL Developer记住密码。

设置方法：菜单Tools --> Preferences --> Oracle --> Logon History --> Store With Password 

重新登录再输入一次密码则记住了。

上述方法若不好用,使用下面的方式：

在上面所说的界面中的"Fixed Users"中,

添加需要直接选择后就可登录的用户名/密码@ORACLE_SID,

如:

cbsdb/cbsdb@cbsdb

重新登录的时候,从Oracle Logon的登录界面的Username后面的...按钮处,

选择需要登录的用户即可。

## **2.2   SQL语句字符全部大写**

信息系统的核心是数据库，系统出问题时最先要查的就是SQL语句，怎样在浩瀚的日志中快速找到那条SQL语句是件比较痛苦的事情。SQL语句全部大写并不能彻底解决这一问题，但在一堆代码中间找一行全部大写的字符相对容易些。设置方法：菜单Tools --> Preferences --> Editor --> Keyword Case --> Uppercase

## **2.3   特殊Copy**   

在SQL Window里写好的SQL语句通常需要放到Java或者别的语言内，就需要转成字符串并加上相应的连字符，这一个事不需要再重复做了，在写好的SQL 上点右键，使用特殊Copy即可！

设置方法：鼠标右键 --> Special Copy

## **2.4   自定义快捷键**  

   PLSQL Developer里预留了很多键让用户自定义，通常情况下，打开PLSQL Developer后，最常用的就是打开SQL Window和Command Window，就可以给这两个操作定义快捷键ALT+S和ALT+ C。

设置方法：菜单Tools --> Preferences --> Key Configuration

 

Shortcut:

============================================================================

Edit/UndoCtrl+Z

Edit/RedoShift+Ctrl+Z

Edit/PL/SQL BeautifierCtrl+W(自定义)

Shift+Home选择光标位置到行首

Shift+End选择光标位置到行尾

Ctrl+Shift+Home选择光标位置到首行行首

Ctrl+Shift+End选择光标位置到尾行行尾

Object:ViewShift+Ctrl+V查看(自定义)

Object:DescribeShift+Ctrl+D结构(自定义)

Object:PropertiesShift+Ctrl+P属性(自定义)

Object:BrowseShift+Ctrl+B浏览(自定义)

Object:Edit DataShift+Ctrl+E编辑数据(自定义)

Object:Standard QueryShift+Ctrl+S标准查询(自定义)

Edit/Find ReplaceCtrl+F

Edit/Find NextCtrl+L

Edit/Find PreviousShift+Ctrl+L

Edit/Replace NextCtrl+P

EDIT/Full ScreenCtrl+F11

Edit/Go to LineCtrl+G

Edit/Next Tab PageCtrl+H

Edit/Previous Tab PageShift+Ctrl+H

 

Session/ExecuteF8

Session/BreakShift+Esc

Session/CommitF10

Session/RollbackShift+F10

 

Debug/Toggle BreakpointCtrl+B

Debug/StartF9

Debug/RunCtrl+R

Debug/Step IntoCtrl+N

Debug/Step OverCtrl+O

Debug/Step OutCtrl+T

 

 

Tools/Explain PlanF5

Tools/Code AssistantF6

 

Editor: Start of DocumentCtrl+PgUpORCtrl+Home

Editor:End of DocumentCtrl+PgDnORCtrl+End

Editor:Delete LineCtrl+Y

Editor:Navigate BackAlt+Left

Editor:Navigate ForwardAlt+Right

SQL Window:Previous SQLCtrl+Up

SQL Window:Next SQLCtrl+Down

[![wps4B08.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302233932438-237439787-1566378962893.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233930563-1357198070.jpg) 

 

 

 

## **2.5   执行单条SQL语句(SQL Window中根据光标位置自动选择语句)**

 

   在使用PL/SQL Developer的SQL Window时，按F8键，PL/SQL Developer默认是执行该窗口的所有SQL语句，需要设置为鼠标所在的那条SQL语句，即执行当前SQL语句；

设置方法：PL/SQL Developer  -->tools->Preferences-->Window types ，勾上“AutoSelect Statement” 即可。**注意，每条语句后面要加分号。** 

 

## **2.6   自动替换**

   快捷输入SQL语句，例如输入s，按下空格，自动替换成SELECT；再例如，输入sf，按下空格，自动替换成SELECT * FROM，非常方便，节省了大量的时间去编写重复的SQL语句。

   设置方法：菜单Tools --> Preferences --> Editor --> AutoReplace. --> Edit

   下面定义了一些规则作为参考

s=SELECT

f=FROM

w=WHERE

o=ORDER BY

d=DELETE

sf=SELECT * FROM

df=DELETE FROM

sc=SELECT COUNT(*) FROM

[![wps4B18.tmp](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233936282-261745390.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233934485-25230366.jpg) 

## **2.7   格式化SQL语句** 

 

在使用PL/SQL Developer的SQL Window时，有时候输入的SQL语句太长或太乱，希望能用比较通用的写法格式话一下，这样看起来会好看些，也好分析；

使用方法：选中需要格式化的SQL语句，然后点击工具栏的PL/SQL beautifier按钮即可.

[![wps4B19.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302233937298-2124187574-1566378962954.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233936798-1927497081.jpg) 

## **2.8   左下角显示window list**

  点击菜单 tools -> window list, 将弹出的小窗口拖到左下角合适位置，然后点击菜单 window->save layout

## **2.9   防止登录超时** 

  tools->Preferences-->Oracle->Connection  选择 "check connection"

## **2.10   不备份sql文件**

  tools->Preferences->Files->backup,页面中backup files中选择 disabled

## **2.11   右键菜单**

在PL/SQL Developer(下面简称PLD)中的每一个文本编辑窗口,

如SQL Window,Command Window和Porgram Window,

右键点击某个对象名称,会弹出一个包含操作对象命令的菜单,我们这里称之为右键菜单。

 

对象类型可以是表,视图,同义词,存储过程和函数等。

根据对象类型的不同,弹出的菜单也有区别。

表和视图有View, Edit, Rename, Drop, Query data 和Edit data等功能。

View和Edit分别是查看和修改表的结构信息,如字段,主键,索引和约束等。

Query data相当于新打开一个窗口,并执行select * from 表。

Edit data相当于新打开一个窗口,并执行select * from 表 for update。

存储过程和函数有Test功能,选中后可以进入调试状态。

有时由于PLD识别错误,右键点击对象并不能出来正确的菜单,

可以在对象所在的DDL或DML语句的前面,加上分号,这样PLD就能正确的判断出对象的类型

 

## **2.12   TNS Names**

菜单Help->Support Info->TNS Names,可以查看Oracle的tnsnames.ora。

## **2.13   Copy to Excel**

在SQL Window中执行Select语句,在结果出来以后,右键点击下面的数据区,

选择Copy to Excel,可以把数据区的记录原样拷贝到Excel中。

但有两点需要注意:

(1)field中不能以=开始,否则Excel会误认为是函数;

(2)数字不要超过17位,否则后面的位数将会置为0,

但可以通过在数字前加'来使Excel认为该field是文本,

同时对于数据库中Numbe类型的字段,最好用to_char输出,不然可能会显示不正常;

## **2.14   保持上次打开的SQL脚本**

重新进入PL/SQL Developer时,Window List能打开上次退出时的文档:

(1)将菜单Tools->Window list选项勾上;

(2)Tools->Perferences->User Interface->Options的右边,

将"Autosave desktop"勾选.

(3)退出PL/SQL Developer重新进入.

 

## **2.15   快速找到已知表名的表或其他对象**

在Tools菜单中,勾选上Object Browser,将对象浏览器打开,

双击对象浏览器中的某个对象所处的文件夹,

比如表都是在Tables文件夹中,

然后以尽快的速度输入表名,即可找到以你输入的几个字母开头的对象了.

## **2.16   快速关闭打开于Windows List中的文档窗口:**

按住Shift键,左键点击需要关闭的文档窗口.

## **2.17   去掉plsql 9.0及以上版本的多连接模式（找了很久的，必做的）**

plsql 9.0及以上版本的多连接模式在实际的开发过程中容易连接错误的库导致生产事故，可以关闭这个功能，如图：

[![wps4B1A.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302233940470-1873509860-1566378962942.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233938938-322083381.jpg) 

 

这样在窗口的最下边就不会出现这个了，[![wps4B1B.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302233941688-1956226112-1566378962938.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233941079-1101741001.jpg)

 

 

## **2.18   设置连接指示灯**

如下图设置后的外观就有所改变：

[![wps4B1C.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302233945345-153695778-1566378962997.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233943610-1435387645.jpg) 

 

如果连接上有所显示：

[![wps4B1D.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302233946970-720417981-1566378962988.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233945985-1245215169.jpg) 

 

## **2.19   null 值的显示**

由于结果集中的空值和空格难以区分，所以可以进行设置颜色来区分null值。

[![wps4B1E.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302233951626-2106076921-1566378963012.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233949329-590777599.jpg) 

 

 

## **2.20  设置最近对象的最大值**

[![wps4B1F.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302233954970-1154169540-1566378963038.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233953485-1313171631.jpg) 

## **2.21  重新调用语句**

[![wps4B20.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302233958173-1276585017-1566378963060.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233956704-2091112339.jpg) 

 

## **2.22  设置工具栏**

[![wps4B21.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234001563-1838777447-1566378963092.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302233959923-287226355.jpg) 

效果：

[![wps4B22.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234003548-1722287358-1566378963150.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234002610-692238919.jpg) 

## **2.23  设置代码助手**

[![wps4B33.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234006438-577393454-1566378963241.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234005048-1754711147.jpg) 

当你键入数据库对象的名字时，代码助手将自动地显示关于它们的信息，这个首选项页允许你定义这个特性的行为。

 

**自动激活**

在某一个延迟之后，代码助手能自动地被调用（请看下面）。你还可以通过功能键选择手工激活代码助手。

 

**延迟**

编辑器在显示代码助手列表之前将等待的毫秒数。

 

**代码风格**

控制了当你选择了已选的项目时它们将怎样被插入到编辑器里：

?  Smart - 代码助手将考虑被描述的对象来决定风格。

?  Init Caps - 每个词（用下划线分隔）的首字符大写。

?  Lowercase - 所有字符都转换到小写。

?  Uppercase –所有字符都转换到大写。

 

**如果可能使用原来的大小写**

这个选项被允许时，如果可能的话，代码助手将确定来自于存储于Oracle 词典的源里的标识符的大小写。这将应用到所有的程序单元和它们的元素（参数、类型等等）以及应用到查看列，并且越过了上面描述的代码风格首选项。如果原始的大小写不能被确定，代码风格将被应用。你可以因执行的原因要求禁止这个特性。

 

**描述用户**

确定了当你键入一个后面跟随着句点的用户名时被用户拥有的对象是否被列出来。如果这个选项被允许，你还可以定义哪些对象类型你要包括在里表里。

 

**描述前后关系**确定了代码助手是否应该描述当前用户、编辑器和程序单元的前后关系。

 

**最少字符数**

确定了在前后关系描述能自动地被调用之前有多少个字符的词需要被键入。注意，你始终可以手工调用代码助手，即使字符数没有被键入也是这样。

 

**描述标准函数**

在默认的情况下，代码助手将描述标准的函数诸如to_char 、add_months 等等。如果你很熟悉这些函数，你可以禁止这个选项。

## **2.24  PL/SQL Developer下设置“长SQL自动换行”**

进入到Tools—Preferences—Editor下进行相关设置，步骤如下图：

点击“Editor”项进行设置，如下图：

[![wps4B34.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234009704-497558514-1566378963163.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234008063-494343256.jpg) 

本次设置，为了实现长代码自动换行，勾选“wrap lines”即可。

长代码自动换行了，更易于显示阅读了，如下所示：

[![wps4B35.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234011970-1324897013-1566378963181.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234010798-744599362.jpg)

补充上图SQL是错误的，只为演示长SQL换行，正常书写应该为：

SQL> create table cool ("1" number(4),"2" varchar2(10),"3" varchar2(9),"4" number(4),"5" date,"6" number(7,2),"7" number(7,2),"8" number(2)); 

Table created   

 

 

 

# **第三章 PLSQL Developer使用技巧**

## **3.1   新建命令窗口**

[![wps4B36.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234015391-1171345220-1566378963202.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234013673-1855005259.jpg) 

## **3.2   PL\SQL 打开时出现"动态执行表不可访问，本会话的自动统计被禁止"** 

 

 

Dynamic Performance Tables not accessible,

Automatic Statistics Disabled for this session

 

You can disable statistics in the preference menu,or obtanin select

priviliges on the v$session,v$sesstat and v$statname tables

 

这个报错信息在不同的PL/SQL Developer版本都会出现，从上面详细的报错提示信息中我们可以判断得到，报错原因不在工具本身。

**产生该提示原因****：**

plsql dev在用户运行过程中，要收集用户统计信息，但是由于你现在登录的用户没有访问v$session,v$sesstat and v$statname视图的权限，所以不能收集当前用户的统计信息，和plsql dev工具中配置的Automatic Statistics相冲突，所以就出现了这个提示

 

在此，详细记录一下这个小问题的三种处理方法。

 

### **3.2.1   第一种处理方法（不推荐）**

 

就是在报错的Error对话框中将“Don't show this message again”选项选中，下次就不在提示这个错误了。

 

这种方法应该可以叫做“鸵鸟方式”的处理方法。没有从根本上解决这个问题。

[![wps4B37.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234017563-1388519706-1566378963294.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234016438-555088875.jpg) 

### **3.2.2   第二种处理方法（可以采纳）**

 

 

报错信息中描述的非常详细，原因是动态性能表没有权利被访问导致的问题，因此，我们通过把所需访问权限赋予给具体用户的方法来解决这个问题。

 

这里给出我能想到的三种具体处理方法。大家可以继续补充。

 

1）如果只是某一具体用户有权限查询这三个动态性能视图，可以如下进行操作

 

这里注意一下：我们授权的视图是V_$session不是V$session，因为V$session是同名不是具体的视图。否则您会收到下面这个错误。

 

sys@ora10g> grant select on V$session to user_sec;

 

grant select on V$session to user_sec

 

*

 

ERROR at line 1:

 

ORA-02030: can only select from fixed tables/views

 

正确的授权方法如下：

 

SQL> grant select on V_$session to user_sec;

 

SQL> grant select on V_$sesstat to user_sec;

 

SQL> grant select on V_$statname to user_sec;

 

2）可以使用下面这个“简单粗暴”的方法处理之。

 

SQL> grant SELECT ANY DICTIONARY to user_sec;

 

3）以上两种方法是针对特定用户的处理方法，如果想让所有用户（不局限在上面的user_sec用户）都能够查询这三个动态性能视图，可以通过将查询权限授权给public方法来实现，操作如下。这样就可以保证所有开发人员都不会再出现上述的报错信息了。

 

SQL> grant select on V_$session to public;

 

SQL> grant select on V_$sesstat to public;

 

SQL> grant select on V_$statname to public;

 

 

### **3.2.3   第三种方法（推荐）**

 

彻底禁掉PL/SQL Developer的这个功能。

 

方法如下：

 

导航到Tools --> Preferences --> Options

 

找到“Automatic Statistics”选项，将其前面的小对勾去掉，然后点击“Apply”和“OK”保存退出

 

## **3.3   查看执行计划**

 

  在使用PL/SQL Developer的SQL Window时，有时候输入的SQL语句执行的效率，分析下表结构，如何可以提高查询的效率，可以通过查看Oracle提供的执行计划；

使用方法：选中需要分析的SQL语句，然后点击工具栏的Explain plan按钮（即执行计划），或者直接按F5即可。

这个里边点击下一步下一步就可以看到执行计划的过程。

另外，对于plsql 11中还可以看到html格式，**Plan Hash Value****或****SQL PROFILE，非常实用：**

[![wps4B38.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234020516-584806704-1566378963274.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234018954-1804029790.jpg) 

[![wps4B39.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234023173-785218945-1566378963310.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234021829-85643069.jpg) 

[![wps4B3A.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234026329-1958735288-1566378963332.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234024673-1356447472.jpg) 

 

## **3.4   调试存储过程** 

 

   在使用PL/SQL Developer操作Oracle时，有时候调用某些存储过程，或者调试存储过程；

调用存储过程的方法：首先，在PL/SQL Developer左边的Browser中选择Procedures，查找需要调用的存储过程；然后，选中调试的存储过程，点击右键，选择Test，在弹 出来的Test scrīpt窗口中，对于定义为in类型的参数，需要给该参数的Value输入值；最后点击上面的条数按钮：Start debugger 或者按F9；最后点击：RUN 或者Ctrl+R

 

 

## **3.5   导出数据到Excel表格后的文件位置：**

C:\Users\Administrator\AppData\Local\Temp

 

如图：

 

[![wps4B3B.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234028891-425718681-1566378963365.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234027688-370921953.jpg) 

 

## **3.6   用pl/sql developer debug**

 

  连接数据库后建立一个Test WINDOW

  在窗口输入调用SP的代码,F9开始debug,CTRL+N单步调试

 

 

 

## **3.7   调试触发器**

右键点击要调试的触发器，选择编辑，在行号位置上点击一下设置断点。

[![wps4B3C.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234032016-1245092314-1566378963392.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234030501-194461417.jpg)

 

在菜单的新建中选择“测试窗口”，打开一个如下块，在begin和end中间添加能触发触发器的语句

[![wps4B4C.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234035970-274248378-1566378963373.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234033923-1390273366.jpg)

按F9或者点击调试菜单中的开始菜单，进入运行调试状态

[![wps4B4D.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234039204-1202106192-1566378963431.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234037360-1054283734.jpg)

点击运行图标跳到触发器中断点位置

[![wps4B4E.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234043485-1337985341-1566378963477.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234041251-683139281.jpg)

鼠标放到变量上可以显示变量值。

## **3.8  Plsql出现乱码**

右击我的电脑--电脑属性--高级系统设置--环境变量。

找到变量名：NLS_LANG（没有的话新建一个，有的话点击--编辑）。

将它的变量值改为：SIMPLIFIED CHINESE.ZHS16GBK

然后点击--确定，重启PLSQL就OK了

[![wps4B4F.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234046704-855145713-1566378963514.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234045204-1843733781.jpg) 

## **3.9   关联oracle官方文档**

【技巧】如何全文搜索oracle官方文档:**http://blog.itpub.net/26736162/viewspace-2065550/**

 

[![wps4B50.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234049657-188815141-1566378963506.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234048126-1098261839.jpg) 

**http://wenku.baidu.com/view/412b6ac208a1284ac9504304.html**

 

 

使用PLSQL Developer 来查看官方文档

 

今天教大家使用PLSQL Developer来查看官方文档，这个是非常方便的，相当于联机在线的搜索功能，大家看好了：

**第1步 下载官方文档到本地，并且解压缩，这个就不多说了**

| **Oracle Server version** | **File size** |
| ------------------------- | ------------- |
| Oracle 11.2 Library       | 408 MB        |
| Oracle 11.1 Library       | 374 MB        |
| Oracle 10.2 Library       | 446 MB        |
| Oracle 10.1 Library       | 257 MB        |
| Oracle 9.2 Library        | 209 MB        |
| Oracle 9.0 Library        | 210 MB        |

 

 

 

 

 

 

 

 

 

 

 

 

 

 

**第2步 打开plsql  developer，按F1，或者打开如下界面：**

[![wps4B51.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234051329-122537148-1566378963554.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234050657-237884387.jpg) 

 

**第3步 输入官方文档的位置，点击建立按钮**

[![wps4B52.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234053516-418055182-1566378963562.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234052485-1799693637.jpg) 

建立的过程有点慢，稍等。。。。。

如图操作：

[![wps4B53.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234057126-754627942-1566378963656.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234055095-1614516612.jpg) 

 

这里给个例子

[![wps4B54.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234059313-236961882-1566378963624.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234058251-1968388513.jpg) 

 

可以查询了

[![wps4B55.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234102266-2086434616-1566378963602.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234100751-1554449881.jpg) 

 

 

或者在

[![wps4B56.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234105798-861964378-1566378963639.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234105126-416173837.jpg) 

 

不过，小麦苗现在基本上都使用离线的chm文件来搜索需要的内容了，详见http://blog.itpub.net/26736162/viewspace-2065550/

需要离线的chm文件的朋友可以去小麦苗的微云下载，地址为：http://blog.itpub.net/26736162/viewspace-1624453/

[![wps4B57.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234106985-136822524-1566378963652.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234106423-243792875.jpg) 

 

## **3.10  除去PL/SQL Developer打开时烦人的logon窗口**

去除PL/SQL Developer打开时烦人的logon窗口

新版本的PL/SQL Developer打开时总会出现如下logon窗口 

[![wps4B58.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234108829-280889858-1566378963694.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234107938-56742343.jpg) 

解决方法： 

1.首先如果你的PL/SQL Developer有修改过配置，先备份你的PLSQL配置和你的连接配置 

2.删除C:\Users\登陆用户\AppData\Roaming\PLSQL Developer下的Preferences文件夹 

3.重新打开后就会发现烦人的logon窗口就会消失了，但是连接配置也被清除了，所以切记 

保存之前的连接配置 

4.将你之前备份的配置重新导入即可

# **第四章 PLSQL Developer配置文件的路径**

[![wps4B69.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234110610-1031378538-1566378963682.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234110001-111746362.jpg) 

C:\Users\Administrator\AppData\Roaming

[![wps4B6A.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234114282-389934098-1566378963703.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234112329-1445488669.jpg) 

 

还有一部分的的配置文件在安装文件夹中，如图：

[![wps4B6B.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234117204-476176566-1566378963712.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234115970-905201618.jpg) 

## **4.1  11版本支持导入配置**

11版本的plsql支持把配置文件导出后再导入了，这个功能很好。

[![wps4B6C.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234120548-1881779788-1566378963739.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234118766-719047634.jpg) 

 

## **4.2   配置字体时找不到相应的字体**

在如下窗口中如果找不到对应的字体可以手动进行设置，前提是系统里必须有这个字体，

[![wps4B6D.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234125688-1362315377-1566378963771.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234123407-431954410.jpg) 

 

收到设置的方法是找到安装路径，然后找到配置文件夹

[![wps4B6E.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234126501-1273576875-1566378963800.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234126251-180729274.jpg) 

进入后找到

[![wps4B6F.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234127016-920216474-1566378963802.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234126751-1825634792.jpg) 

进行收到配置即可。 

# **第五章 一个非常实用的插件**

[![wps4B70.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234128470-203847747-1566378963829.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234127845-1852277049.jpg) 

 

现有功能简要说明：

主菜单功能所有主菜单可在PL/SQL中设置工具栏按钮，以方便调用

CnPlugin / Comment /&Commnet Lines 以“--”注释当前选中的代码

CnPlugin / Comment /&Uncommnet Lines 去除当前选中以“--”注释的代码

CnPlugin / &ReConnect 重连中断的数据库连接

CnPlugin / &ExPaste 对当前选中或剪贴板内空格式化为IN 字符串，如格式化字符串AA,BB,CC为('AA','BB',CC')

CnPlugin / &ExCreate 建表时插入COMMENT的字段说明,如CREATE TABLE tt(ID NUMBER --编号);语句，除执行当前建表语句外，会自动生成comment on column TT.ID is '编号'注释语句

CnPlugin / Script / Load From MDB 以列表窗口形式读取已保存在Access数据库中的SQL语句

CnPlugin / Script / Save To MDB 保存当前SQL语句至Access数据库

CnPlugin / Script / Save As To MDB 另存为当前SQL语句至Access数据库

CnPlugin / Toggle Read Only 设置/取消设置当前SQL窗口为直读。

CnPlugin / Find All... 对当前窗口容空查找指定的字符串，列出全部匹配内容，支持正则表达式查找

CnPlugin / &Preferences CnPlugin插件属性设置窗口

CnPlugin / &About' CnPlugin关于窗口右键菜单功能

Query data using alias 以字段注释字符作为字段名拼出查询SQL语句（选中表名出现）

Open in new SQL Window 复制当前窗口选中的SQL语句到新窗口中（选中字符串是出现）

Execute in new SQL Window 复制当前窗口选中的SQL语句到新窗口中并执行语句（选中字符串是出现）

Generate Word Documentation 导出当前表结构内容至Word文档（选中表名出现）

无菜单功能

快捷键输入功能:如输入s空格，带出'select * from '，支持光标定位登录时打开或执行指定SQL文件

 

我常用的功能是Expaste功能，这个功能能把复制的文本自动添加单引号，这个功能非常实用。

[![wps4B71.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234130532-1331622441-1566378963838.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234129423-1442545373.jpg) 

复制如下数字：

1

2

3

4

执行expaste粘贴后：

[![wps4B72.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234132423-666923912-1566378963845.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234131454-283279869.jpg) 

# **第六章  报错**

## **6.1   PL/SQL Developer启动时报错:"Control 'dxDockBrowserPanel' has no parent window"**

 

PL/SQL Developer启动时报错:

"Control 'dxDockBrowserPanel' has no parent window"

 

出现原因:某次刚打开PL/SQL Developer 8.0.4,界面还没有加载的时候,机器死机了,然后强行重启,再打开PL/SQL Developer就报错.

尝试过的办法:

1.重装PL/SQL Developer7.1.5/8.0.2/8.0.4/9.0.2等多个版本均出现该问题;

2.系统还原也无效.

3.删除C:\Users\用户名\AppData\Roaming\PLSQL Developer的配置文件无效.

解决办法:

删除注册表中的

HKEY_CURRENT_USER\Software\Allround Automations\PL/SQL Developer\Docking

也有可能是Docking1、Docking2、Docking3......

这种东西全删掉就好了,然后打开OK

 

 

## **6.2  不支持64位**

PLSQL Developer连接不上Win7 64位系统下安装的Oracle11g64位的解决办法

 

[![wps4B73.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234134454-114928077-1566378963861.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234133345-2074140807.jpg) 

 

由于在本机Win7X64上安装了64位的Oracle，结果试图使用PLSQL Developer去访问它的时候，报告说无法加载oci.dll文件。原来oci.dll是64位的，32位应用程序PLSQL Developer自然无法加载了。

这个问题目前有3种解决办法

### **6.2.1  办法一，网上的通用办法**

 

1）安装Oracle 11g 64位

2）安装32位的Oracle客户端（ instantclient-basic-nt-11.2.0.2.0）

 

下载instantclient-basic-nt-11.2.0.2.0.zip (一定得是32位的，不要下错了版本，Oracle官网有下载），将其解压至Oracle安装目录的Product下（里面默认的文件夹名为：instantclient_11_2）：D:\app\yeohcooller\product\instantclient_11_2。

 

拷贝数据库安装根目录下的一个目录D:\app\yeohcooller\product\11.2.0\dbhome_1\NETWORK到Oracle客户端目录下D:\app\yeohcooller\product\instantclient_11_2（其实只需要 NETWORK\ADMIN\tnsnames.ora）

 

3）安装PL/SQL Developer

 

安装 PL/SQL Developer，在perference->Connection里面设置OCI Library和Oracle_Home，例如本机设置为：

 

Oracle Home ：D:\app\yeohcooller\product\instantclient_11_2

 

OCI Library ：D:\app\yeohcooller\product\instantclient_11_2\oci.dll  

接下来这步可选。

 

设置环境变量(修改PATH和TNS_ADMIN环境变量)

 

对于NLS_LANG环境变量, 最好设置成和数据库端一致, 首先从数据库端查询字符集信息:

  SQL> select userenv('language') nls_lang from dual;

  NLS_LANG

  \----------------------------------------------------

SIMPLIFIED CHINESE_CHINA.ZHS16GBK

 

右击"我的电脑" - "属性" - "高级" - "环境变量" - "系统环境变量":

  1>.选择"Path" - 点击"编辑", 把 "D:\app\yeohcooller\product\instantclient_11_2;" 加入;

  2>.点击"新建", 变量名设置为"TNS_ADMIN", 变量值设置为"D:\app\yeohcooller\product\instantclient_11_2;",点击"确定";

  3>.点击"新建", 变量名设置为"NLS_LANG", 变量值设置为"SIMPLIFIED CHINESE_CHINA.ZHS16GBK", 点击"确定";

  最后点击"确定"退出.

这里需要注意oracle 的安装目录中不能包含空格

 

 

### **6.2.2  我自己的办法(1)--批处理**

我自己解决的时候其实没有这么麻烦：

1．下载instantclient-basic-nt-11.2.0.2.0（高版本也行，但是必须是32位的）到任意目录，目录不能含有空格

2．在客户端目录中新建一个批处理文件，文件内容如下代码所示，这里要把plsqldev的快捷方式加载到该目录下，或者把该批处理文件加载到plsql developer 目录中也行，以后直接运行该批处理文件就可以了

@echo off

set path=D:\instantclient_12_1

set ORACLE_HOME=D:\instantclient_12_1

set TNS_ADMIN=C:\app\oracle\product\12.1.0\dbhome_1\NETWORK\ADMIN

set NLS_LANG=AMERICAN_AMERICA.ZHS16GBK

start D:\instantclient_12_1\plsqldev

Windows  环境下有的时候需要设置ORACLE_HOME 的变量

 

### **6.2.3  我自己的办法(2) 强烈推荐 --下载小麦苗定制版的pl/sql developer**

在小麦苗云盘里下载PLSQL Developer_all_lhr_new.zip文件，解压文件后，设置环境变量后即可使用（设置方法在里边已经提供），无需安装，绿色版。

**注意：不需要单独下载****instantclien****t文件，小麦苗的定制版里边已经包含了客户端工具，包含sqlplus、sqlldr、exp、tnsping等工具，非常实用。**

 

### **6.2.4  我自己的办法（3）--下载64位的版本**

下载64位的 PL/SQL Developer。

 

小麦苗的云盘有下载。http://blog.itpub.net/26736162/viewspace-1624453/

 

 

## **6.3  连接时数据库角色不能选择**

如下，如果角色不能选择的话，可能是OCI配置的问题：

[![wps4B74.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234136188-1816057655-1566378963841.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234135345-548737038.jpg) 

[![wps4B75.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234138845-506459635-1566378963874.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234137454-646589306.jpg) 

 

正确界面：

[![wps4B86.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234142173-1936764304-1566378963891.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234141485-1599393622.jpg) 

 

 

配置里边是否合适？如下是我的配置：

D:\Program files\app\oracle\product\11.2.0.1\dbhome_1

D:\Program files\app\oracle\product\11.2.0.1\dbhome_1\bin\oci.dll

[![wps4B87.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234144501-1827968463-1566378963887.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234143470-1633960266.jpg) 

 

## **6.4  数据库连接符tns不能选择**

该问题虽然不影响登录，但是始终觉得欠缺点什么东西：

错误登录界面：

[![wps4B88.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234146407-1142946624-1566378963903.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234145501-794833374.jpg) 

 

正确界面：

[![wps4B89.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234148657-1089576244-1566378963911.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234147516-74074754.jpg) 

 

解决办法：

设置TNS_ADMIN，查看系统环境变量是不是设置了TNS_ADMIN变量，且变量的值是到目录名：

TNS_ADMIN=D:\Programfiles\app\oracle\product\11.2.0.1\dbhome_1\NETWORK\ADMIN

[![wps4B8A.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234151001-743176523-1566378963923.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234150141-1943734167.jpg)

 

## **6.5  编译存储过程时不能显示错误**

如下，正常的有错误窗口：

[![wps4B8B.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234153235-1804787634-1566378963929.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234151985-1969643355.jpg) 

 

而下边的存储过程没有错误窗口：

[![wps4B8C.tmp](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/646850-20170302234155923-969218393-1566378963947.jpg)](http://images2015.cnblogs.com/blog/646850/201703/646850-20170302234154438-981102086.jpg) 

 

原因：其实很明显了，就是存储过程的名称后边的小括号应该使用英文的，而不应该使用**中文括号**。





------

------

> **About Me**
>
> 
>
>  [![img](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/ico_mailme_02.png)](http://mail.qq.com/cgi-bin/qm_share?t=qm_mailme&email=eRURCxscCg05CAhXGhYU)  [![DBA笔试面试讲解](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/group.png)](http://shang.qq.com/wpa/qunwpa?idkey=8bb4d1af8e3188b523227caf7f070851169e74a66ef92c2a436634de6bc0ad56)



来自 “ ITPUB博客 ” ，链接：http://blog.itpub.net/26736162/viewspace-2134628/，如需转载，请注明出处，否则将追究法律责任。

1

2

分享到：

上一篇： [HugePages 大内存页](http://blog.itpub.net/26736162/viewspace-2134314/)

下一篇： [数据库笔试面试题库（Oracle、MySQL等）](http://blog.itpub.net/26736162/viewspace-2134706/)

[![img](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/user_pic_default.png)](javascript:;)

请登录后发表评论 登录

全部评论 1

[![img](PLSQL%20developer%E7%9A%84%E4%BD%BF%E7%94%A8.assets/44.jpg)](http://blog.itpub.net/20893244)

[甲骨文技术支持](http://blog.itpub.net/20893244)回复

2017-03-05 13:10:57

感谢分享

2017-03-05 16:45:11回复

[lhrbest](http://blog.itpub.net/20893244)   回复   [甲骨文技术支持](http://blog.itpub.net/26736162)： <img src="/images/qqface/13.gif" />

 

[支持我们](http://www.it168.com/bottomfile/it168.shtml) [作者招募](http://www.it168.com/bottomfile/tgzn.shtml) [用户协议](http://www.it168.com/bottomfile/sytk.shtml) [FAQ](http://blog.itpub.net/31509949/viewspace-2157750/) [Contact Us](http://edu.itpub.net/contactus.html) [站长统计](https://www.cnzz.com/stat/website.php?web_id=1274521965)

北京盛拓优讯信息技术有限公司. 版权所有  [京ICP备09055130号-4](http://beian.miit.gov.cn/)  北京市公安局海淀分局网监中心备案编号：11010802021510

广播电视节目制作经营许可证(京) 字第1234号 中国互联网协会会员