### UI单个请求处理文件封装格式以及主要步骤 [	](UI_20200604111305718)

1. MyAction.java
1. 继承AbstractBaseAction类
   2. 添加@StrutsAction注解
   3. 声明HTML路径常量
   4. 声明服务接口
   5. 声明doXXX()函数
   6. 添加getter/setter
2. MyForm.java
   1. 继承AbstractUILForm
   2. 实现InfUILDisplay
   3. 添加页面上的表单数据属性
3. MyService.java
   1. 继承UfBaseBLService类
4. impl/MyService.java
   1. 继承AbstractUIKRService类
   2. 实现MyService接口

### UI的ACTION类定义模板 [	](UI_20200604111305720)

```java
   @StrutsAction(parameter = "method", validate = BoolType.FALSE)
   public class MyAction extends AbstractBaseAction {
       @StrutsActionForward(path = "/list/top.do?method=index")
       public static final String MYINPUT = "accountInput";
       private MyService myService;
       private MyForm form;
       public void initialize() {
       }
       @ActionIndex
       @BLID("XXX")
       public String doIndex() throws AbsUfException {
           initAccountInputService.delegate(UfWebUtil.getBLID(), inputForm);
           return INPUT;
       }
       public String doInitWithBack/doBack/...() throws AbsUfException {
           return INPUT;
       }
   }
```

### 添加AJAX请求的方法 [	](UI_20200604111305721)

1. 添加`mayaa`文件 

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <m:mayaa xmlns:m="http://mayaa.seasar.org"
            xmlns:mcep="http://mld.chuden.co.jp/mcep"
            xmlns:cep="http://tld.chuden.co.jp/cep"
            xmlns:s2struts="http://www.seasar.org/tags-s2struts"
            xmlns:bean="http://struts.apache.org/tags-bean"
            m:noCache="true">
   
     <!-- 画面表示前処理 -->
     <m:beforeRender><![CDATA[
   
       load("init.js");
   
       load("mayaaView.js");
   
     ]]></m:beforeRender>
   
     <!-- jsonText TODO：※処理に応じて必ず書き換えてください。 -->
     <m:write m:id="jsonText" value="${jsonText}" escapeXml="false" />
   
   </m:mayaa>
   
   ```

2. 添加HTML文件

   ```html
   <html xmlns:m="http://mayaa.seasar.org" lang="ja" m:id="jsonText"></html>
   ```

3. 在`ServiceImpl`中添加`mayaa`中绑定的request的attribute

   ```java
   super.setRequestAttribute("jsonText", json.getJSONText());	
   ```

   `jsonText`属性是一个JSON字符串