# 业务说明

20191101PF項目追加対応
--------------------
### 环境。

**开发环境地址：**\192.168.6.11\doc\Ux 環境\UF\All-In-One-IDE

和UI同一个BASELINE，但工程代码完全分开，代码SVN隔离
    PURE
    PLATFORM

入口：

   http://localhost:8088/index.html?by=oERLq                 （Google浏览器）

   http://localhost:8080/bp/login/index.html?by=oERLq

  http://192.168.6.12:8080/index.html?by=oERLq 

## 作业内容

文件夹：D:\UI_SVN\300_プロジェクト管理\20191101PF項目追加対応

文件：PF改修製造横一覧(内部).xlsx

--------------------
具体做什么事情需要参考的资料

文件夹：D:\UI_SVN\020_基本設計\20191101PF項目追加対応\参考資料

- 文件1：ENTITY[プラットフォーム月別実績情報].xlsx
- 文件2：PF_項目追加_ver.3.xlsx

/UIL-WebCommon/src/main/java/jp/co/chuden/ui/uil/webapp/service/csvfilter/PlatformCsvConverter.java

/UIL-WebCommon/src/main/java/jp/co/chuden/ui/uil/webapp/service/csvfilter/PlatformCsvDto.java

/UIL-WebCommon/src/main/java/jp/co/chuden/ui/uil/webapp/service/csvfilter/PlatformCsvClumnDto.java

### 这次修改的内容

**下面所修改的项目，注意工程代码中的注释，dto对应的修改**

**`PlatformKeiyakuLoaderManager`类中封装了这次要改的表的所有操作**

**`PlatformKeiyakuLoaderManager`类是2种subsystem共用的**

由于添加了2种【基本料金】下面黄色部分添加了状态

![image-20191114180727249](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191114180727249.png)

![image-20191114180732550](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191114180732550.png)

## カテエネPF:画面入口

### 第一步：登陆

进入：http://localhost:8088/index.html?by=oERLq

账户：CDE_MEMBER_MAIN
密码：abcd1234

登陆进入后会显示错误页面，接下来直接访问：http://localhost:8088/kp/platform/platformInit.do会正常进入

### 第二步：当月明细入口

![image-20191114211642148](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191114211642148.png)

式样书上的入口：



http://localhost:8088/kp/syokai/tougetumeisai.do?method=doIndex

### 修改完成目标

#### 機能：ログイン後トップ   

如果改修以后下面画面正常显示就说明对它没有影响，其他的只是确认而已。

![image-20191114211006585](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191114211006585.png)

### 3种契約状态

-   廃止月
-   当月（非廃止）
-   速报（bp）

### 3种契約種別

-   電気
-   ガス
- その他

## ビジエネPF：画面入口

先进入：http://localhost:8888/bp/login/index.html?by=oERLq 登陆

http://192.168.6.12:8081/bp/login/index.html?by=oERLq 

账户：CDE_MEMBER_MAIN
密码：abcd1234

然后进入：http://localhost:8888/bp/list/ichiran.do

http://192.168.6.12:8081/bp/list/ichiran.do

### 进入【料金実績】:

![image-20191114215253645](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191114215253645.png)

后面2个选项卡，分别有2个download。

#### 问题：确认一下以上2个csv是否相同

#### 问题：分别点进去就能拿到下面3个料金実績？？

![image-20191114215706669](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191114215706669.png)

#### todo:以下的内容是只是确认的，具体如何进去，等QA之后再处理

![image-20191114215954397](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191114215954397.png)

# 设计书与测试式样书

--------------------

### SVN\040_詳細設計\201906UI件名\1PF速報値対応\30.UI料金照会

找到对应的代码改的位置然后标上颜色

![image-20191114222735944](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191114222735944.png)

### todo:参照一下视频最后一部分关于测试截图的几个文件的内容

SVN\080_テスト管理\201906UI件名\1PF速報値対応\01_テスト仕様書\30.UI料金照会\20.Club BizEne

20191101PF項目追加対応
エビデンス     SVN\020_基本設計\20191101PF項目追加対応\20191111_仕様書\テストケース参考\エビデンス

---------------------------------------

9、20191101PF項目追加対応

## 常用SQL

```sql 
SELECT * FROM PF_JISSEKI_INFO_MONTHLY 
WHERE PLATFORM_SEQ='1000000000' 
AND JISSEKI_CHOTEI_Y='2019'
AND KEIYAKU_ID LIKE '20190F%';

SELECT   pjim.SPECIAL_RYOKIN_NAME01,
  pjim.SPECIAL_SIYORYO01,
  pjim.SPECIAL_RYOKIN01,
  pjim.SPECIAL_RYOKIN_NAME02,
  pjim.SPECIAL_SIYORYO02,
  pjim.SPECIAL_RYOKIN02,
  pjim.SPECIAL_RYOKIN_NAME03,
  pjim.SPECIAL_SIYORYO03,
  pjim.SPECIAL_RYOKIN03,
  pjim.SPECIAL_RYOKIN_NAME04,
  pjim.SPECIAL_SIYORYO04,
  pjim.SPECIAL_RYOKIN04,
  pjim.SPECIAL_RYOKIN_NAME05,
  pjim.SPECIAL_SIYORYO05,
  pjim.SPECIAL_RYOKIN05
FROM PF_JISSEKI_INFO_MONTHLY pjim
WHERE
pjim.JISSEKI_CHOTEI_YM > '201906'
AND pjim.KEIYAKU_ID = '20190F001'
FOR UPDATE




PlatformKeiyakuKihonInfoEntity
```

# todo列表

4. 理解QA中所提的问题 
5. 整理问题
9. 修改PlatformJissekiInfoMonthlyEntity类根据文件：
   D:\UI_SVN\020_基本設計\20191101PF項目追加対応\参考資料ENTITY[プラットフォーム月別実績情報].xlsx
5. CVS文件2个注意点：
   1. 字段头在：PlatformCsvConverter的HEADER_ITEM_NAME_ELC字段
   2. 实体对应的方法调用在：PlatformCsvDto的OUTPUT_METHODS_ELC字段
   3. CSV实体对象：PlatformCsvClumnDto
6. 修改4个修改字段的注释：注意要将所有调用GET SET的地方都检查一边
   ![image-20191114182420664](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191114182420664.png)

# QA管理

### 问题1:KATENE中是否没有[**速报（bp）**]这一契约状态?

### 问题2:确认以下画面的CSV是否要改

![image-20191114222057461](https://gitee.com/xieyun714/nodeimage/raw/master/img/image-20191114222057461.png)

