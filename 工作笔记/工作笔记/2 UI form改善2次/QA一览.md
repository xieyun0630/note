【停止申込】

http://localhost:8080/clubkatene/apply/haishi/detail/haishiDetailInput.html?nla=true

【開始申込】
http://localhost:8080/clubkatene/apply/kaishi/detail/kaishiDetailInput.html?nla=true

【開始廃止申込】
http://localhost:8080/clubkatene/apply/hikkoshi/detail/hikkoshiDetailInputHaishi.html?nla=true

## mayaa绑定问题

## pageClose与topPage的显示有什么区别吗，如何做到分别显示

```html

<span m:id="amazonBtn">
    <p class="pModEleCenter"><a m:id="amazonUrlTarget" href="" target="_blank"><img
                                                                                    class="opImg" m:id="amazonJpg" src="" alt="amazonprime購入"></a></p><br>
</span>
<span id="pageClose" style="display: none">
    <p class="pModEleCenter comBtn comBtn01"><a href="#" onclick="closeWindow();">このページを閉じる</a></p>
    <input type="hidden" id="needDelay" src="/clubkatene/list/top.do" value="5000"/>
</span>

<span id="topPage" style="display: none">
    <p>引続き「カテエネ」をご利用ください。</p><br>
    <p class="pModEleCenter comBtn comBtn02"><a m:id="appLinkHome" href="mypage.html"
                                                onclick="linkEvt(event, this)">カテエネ トップページへ</a></p>
</span>
<input type="hidden" m:id="hiddenUserId" id="userId" name="userId"/>
```

## uik.entry.sapoene.param.gas.p.key是代表什么的？
```js
    $(function(){
  //QRコード経由ガス申込み制御
	if ($.cookie("uik.entry.sapoene.param.gas.p.key")) {
		//クッキーの値がある場合、ガス申込みボタンを表示
      $("#topPage").show();
		//クッキー削除
      $.removeCookie("uik.entry.sapoene.param.gas.p.key",{ path: "/" });
      return;
	}else{
		$("#pageClose").show();
      return;
	}
   });
```

## 关于错误信息处理问题。

![1572260276376](QA%E4%B8%80%E8%A7%88.assets/1572260276376.png)

关于新的住所参数检查问题：

![1572262073362](QA%E4%B8%80%E8%A7%88.assets/1572262073362.png)

1. 这里对应的检查有7个，是否要改成这种类型的？
2. checkAddress检查里没有返回值，而目前的检验方法需要返回一个boolean,这里是否有问题？
3. 3.在UIKEJusyoDTO中拼接的字符串  没有空格 是否有影响？
4. 使用了新的checkAddress中的getAddress后，form中还有必要继续保存住所名字啊？

# 新指示书问题：

## 问题：图片如何处理？  删除线所标注的内容不需要吗？

![image-20191029120651207](QA%E4%B8%80%E8%A7%88.assets/image-20191029120651207.png)

```html
<a class="c-link-has-line ga_click" href="/image/regist/img_meter.png" target="_blank">熱田（受付センター）    <svg class="c-icon c-icon-inline c-icon-primary">        <use xlink:href="#blank"></use>    </svg></a>
```

## 【インライン表示】是什么意思？

![image-20191031144246864](QA%E4%B8%80%E8%A7%88.assets/image-20191031144246864.png)

![image-20191031143903740](QA%E4%B8%80%E8%A7%88.assets/image-20191031143903740.png)



## 待处理bug

文本框的值 自动填入？

### ![image-20191101190819995](QA%E4%B8%80%E8%A7%88.assets/image-20191101190819995.png)

## 以下隐藏有问题： 	

![image-20191101200112109](QA%E4%B8%80%E8%A7%88.assets/image-20191101200112109.png)





![image-20191102174706318](QA%E4%B8%80%E8%A7%88.assets/image-20191102174706318.png)



# 考用画面

【停止申込】
http://localhost:8080/clubkatene/apply/haishi/detail/haishiDetailInput.html?nla=true

【開始申込】
http://localhost:8080/clubkatene/apply/kaishi/detail/kaishiDetailInput.html?nla=true

【開始廃止申込】
http://localhost:8080/clubkatene/apply/hikkoshi/detail/hikkoshiDetailInputHaishi.html?nla=true

http://localhost:8080/clubkatene/gasswreq4m/gasSwReq4mInput.html?kid=1117588000072&org.apache.struts.taglib.html.TOKEN=bb9d62aa7cd22c6e3c2ff887847f4193&current.page=L2dhc3JlcWxpc3QvZ2FzUmVxTGlzdFN3Lmh0bWw%3D

http://192.168.6.60:8080/clubkatene/gasswreq4m/gasSwReq4mInput.html?kid=1117588000072&org.apache.struts.taglib.html.TOKEN=bb9d62aa7cd22c6e3c2ff887847f4193&current.page=L2dhc3JlcWxpc3QvZ2FzUmVxTGlzdFN3Lmh0bWw%3D



## 当期工作

#### 用到的错误文件路径

`D:\All-In-One-IDE4.8_UI\workspace\UIK-WebApp\WebEnvSetup\src\00.default\etc\msg\UIERIMessage.csv`

#### jusyo部分参考部分

`D:\All-In-One-IDE4.8_UI\workspace\UIK-WebApp\src\main\java\jp\co\chuden\ui\uik\webapp\web\apply\kaishigasset\detail\impl\KaishiGasSetDetailConfirmServiceImpl.java`

#### 问题：这里的方法选择哪一个？

```html
<!-- 》住所選択時の要求URL -->
  <m:echo m:id="jushoSelectUrl">
    <m:attribute name="value" value="${getLink('jusyo_addressSelectAction', 'doSelectJushoForZenpaiSaisin', null)}" />
  </m:echo>

```

## 问题：格式问题

![image-20191111152721210](QA%E4%B8%80%E8%A7%88.assets/image-20191111152721210.png)

## todo:错误信息修改以后注意运行一下以下工程的ant文件 

![image-20191113200015621](QA%E4%B8%80%E8%A7%88.assets/image-20191113200015621.png)

## 单选的控制

```
  <m:write m:id="juyoBasyoPostCd" value="${form.juyoBasyoPostCd}" />
  <m:write m:id="juyoBasyoAddress" value="${form.juyoBasyoAddress}" />
  <!-- 検針票の送付先住所 郵便番号 -->
  <m:write m:id="gasPostCd" value="${form.gasPostCd}" />
  <!-- 検針票の送付先住所 住所 -->
  <m:write m:id="gasAddress" value="${form.gasAddress}" />

  <!-- ご契約名義 -->
  <m:write m:id="keyakuMeigi" value="${form.keyakuMeigi}" />
  <!-- ご契約名義（カナ） -->
  <m:write m:id="keyakuMeigiKana" value="${form.keyakuMeigiKana}" />
```

## url

http://localhost:8080/clubkatene/gasswreq4m/gasSwReq4mInput.html?kid=1103440099401&org.apache.struts.taglib.html.TOKEN=38c8bc1aaeca06da742bfaff277b50ba&current.page=L2dhc3JlcWxpc3QvZ2FzUmVxTGlzdFN3Lmh0bWw%3D 

http://192.168.6.12:8888/clubkatene/gasswreq4m/gasSwReq4mInput.html?kid=1103440099401&org.apache.struts.taglib.html.TOKEN=38c8bc1aaeca06da742bfaff277b50ba&current.page=L2dhc3JlcWxpc3QvZ2FzUmVxTGlzdFN3Lmh0bWw%3D 

http://192.168.6.67:8080/clubkatene/gasswreq4m/gasSwReq4mInput.html?kid=1103440099401&org.apache.struts.taglib.html.TOKEN=38c8bc1aaeca06da742bfaff277b50ba&current.page=L2dhc3JlcWxpc3QvZ2FzUmVxTGlzdFN3Lmh0bWw%3D 



 http://localhost:8080/clubkatene/gasswreq4m/gasSwReq4mInput.html?kid=1103440099401&org.apache.struts.taglib.html.TOKEN=38c8bc1aaeca06da742bfaff277b50ba&current.page=L2dhc3JlcWxpc3QvZ2FzUmVxTGlzdFN3Lmh0bWw%3D 

 电气：

 http://localhost:8080/clubkatene/gasswreq4m/gasSwReq4mInput.html?kid=1176745047700&org.apache.struts.taglib.html.TOKEN=dd970ffbaa158709915c8f85d7518e40&current.page=L2dhc3JlcWxpc3QvZ2FzUmVxTGlzdFN3Lmh0bWw%3D 

```html
UIERIMessage
```

```js
UIKR74423E,都道府県が選択されていません。,-,都道府県が選択されていない。,0
UIKR74424E,市区町村が選択されていません。,-,市区町村が選択されていない。,0
UIKR74425E,大字名が選択されていません。,-,大字名が選択されていない。,0
UIKR74426E,字丁目が選択されていません。,-,字丁目が選択されていない。,0
UIKR74427E,番地が入力されていません。,-,番地が入力されていない。,0
UIKR74428E,番地が18文字を超えています。,-,番地が18文字を超えている。,0
UIKR74429E,番地に機種依存文字又は、全角文字でない文字が入力されています。,-,番地に機種依存文字又は、全角文字でない文字が入力されている。,0
UIKR74430E,建物名・アパート名が24文字を超えています。,-,建物名・アパート名が24文字を超えている。,0
UIKR74431E,建物名・アパート名について全角文字で入力してください。,-,建物名・アパート名に機種依存文字又は、全角文字でない文字が入力されている。,0
UIKR74432E,部屋番号が8文字を超えています。,－,部屋番号が8文字を超えている。,0
UIKR74433E,部屋番号について全角英数で入力してください。,-,部屋番号に全角英数カタカナ文字でない文字が入力されている。,0
```



## 问题：

![image-20191111165643468](QA%E4%B8%80%E8%A7%88.assets/image-20191111165643468.png)

![image-20191113162834189](QA%E4%B8%80%E8%A7%88.assets/image-20191113162834189.png)

## 学习待办：

http://localhost:8088/kp/download/downloadCondition.do?keiyakuKbn=01&org.apache.struts.taglib.html.TOKEN=94a83ee90976a950156fd388fb393a53&current.page=L3N5b2thaS9yeW9raW5KaXNzZWtpLmh0bWw%3D

![image-20191113203242803](QA%E4%B8%80%E8%A7%88.assets/image-20191113203242803.png)







![image-20191115121042837](QA%E4%B8%80%E8%A7%88.assets/image-20191115121042837.png)

# 开会

![image-20191121152850504](QA%E4%B8%80%E8%A7%88.assets/image-20191121152850504.png)

## 1个

![image-20191121152540533](QA%E4%B8%80%E8%A7%88.assets/image-20191121152540533.png)

## 2个

![image-20191121152626533](QA%E4%B8%80%E8%A7%88.assets/image-20191121152626533.png)