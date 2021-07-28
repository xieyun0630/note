## 常用正则表达式

### 识别时间：去掉多余打卡

```
(\d\d:\d\d).+(\d\d:\d\d)$
```

匹配中文字符的正则表达式：` [\u4e00-\u9fa5]`

日期匹配

```
(\d{1,4}[-]\d{1,2}[-]\d{1,2})
```

时间匹配

```
(\d{1,2}:\d{1,2})
```

无打卡的数据

```
^[\u4e00-\u9fa5 ]{1,6}	\d{4}[\\-]\d{2}[\\-]\d{2}	$
```

只打一次卡的数据

```
^[\u4e00-\u9fa5 ]{1,6}	\d{4}[\\-]\d{2}[\\-]\d{2}	(\d{1,2}:\d{1,2})$
```

```
^([\u4e00-\u9fa5 ]{1,6}	\d{4}[\\-]\d{2}[\\-]\d{2})	(\d{1,2}:\d{1,2}) (\d{1,2}:\d{1,2})
```

```
#替换
^([\u4e00-\u9fa5 ]{1,6}	\d{4}[\\-]\d{2}[\\-]\d{2})\n	(\d{1,2}:\d{1,2}) (\d{1,2}:\d{1,2})

$1 $2\n$1 $3
```



## 部署命令

```
npm run build:prod
```

## Excel模板下载

**按钮注册**

```html
<el-button v-if="printBtnShow" type="primary" @click="handleExcelPrint">打印内箱标签(Excel)</el-button>
```

**按钮函数**

```javascript
    /** 打印内箱标签 */
    handleExcelPrint() {
      const that = this
      GetLabelExcelByERPNO(this.postForm.erpno, this.postForm.lotNo, this.total).then((res) => {
        const blob = new Blob([res], {
          type: 'application/vnd.ms-excel'
        })
        const fileName = 'InnerLabel.xlsx'
        const linkNode = document.createElement('a')

        linkNode.download = fileName // a标签的download属性规定下载文件的名称
        linkNode.style.display = 'none'
        linkNode.href = URL.createObjectURL(blob) // 生成一个Blob URL
        document.body.appendChild(linkNode)
        linkNode.click() // 模拟在按钮上的一次鼠标单击

        URL.revokeObjectURL(linkNode.href) // 释放URL 对象
        document.body.removeChild(linkNode)

        that.$notify({
          message: '下载成功',
          type: 'success',
          duration: 2000
        })
      }).finally(_ => (that.loading = false))
    }
```

**模板下载请求**

```javascript
export function GetLabelExcelByERPNO(erpno, lotNo, total, start, end) {
  return request({
    url: '/api/SectList/GetLabelExcelByERPNO',
    method: 'post',
    params: { erpno, lotNo, total, start, end },
    responseType: 'blob'
  })
}
```

**后端代码**

```c#
        private readonly IWebHostEnvironment _webHostEnvironment;

		[HttpPost]
        public async Task<FileResult> GetLabelExcelByERPNO(string erpno, string lotNo, string total,string start,string end)
        {
            var entity = (await _sectlistRepository.Query(x => x.ERPNO == erpno.Trim())).FirstOrDefault();
            var labelDto = new InnerBoxDto();
            labelDto.customerType = entity.CustomerName;
            labelDto.mpn = entity.ERPNO;
            labelDto.partNumber = entity.SectNo;
            labelDto.dateCode = string.IsNullOrWhiteSpace(start)?DateTime.Now.ToString("yyyyMMdd"):start;
            labelDto.expDate = string.IsNullOrWhiteSpace(end)?DateTime.Now.AddYears(1).AddDays(-1).ToString("yyyyMMdd"):end;
            labelDto.lotNo = lotNo;
            labelDto.vendor = entity.vendor;
            labelDto.qty = total;
            var barcode = (entity.CustomerName ?? "") + ","
                + (labelDto.mpn ?? "") + ","
                + (entity.SectNo ?? "") + ","
                + (labelDto.dateCode ?? "") + ","
                + (labelDto.expDate ?? "") + ","
                + (labelDto.qty ?? "") + ","
                + (labelDto.lotNo ?? "") + ","
                + (labelDto.vendor ?? "") ;
            labelDto.barcode = barcode;

            //模板文件  
            var tempFileFullPath = Path.Combine(_webHostEnvironment.WebRootPath, "excelTemplate", "InnerLabel.xlsx");

            //下载文件
            var newFilePath = Path.Combine(_webHostEnvironment.WebRootPath, "excelDownLoad", DateTime.Now.ToString("yyyyMMddHHmmss") + ".xlsx");

            var newFilePathPdf = Path.Combine(_webHostEnvironment.WebRootPath, "excelDownLoad", DateTime.Now.ToString("yyyyMMddHHmmss") + ".xlsx");
            //excel文件赋值
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;//5.0以上一定要指明非商业证书
            FileInfo fileInfo = new FileInfo(newFilePath);
            FileInfo file = new FileInfo(newFilePath);
            System.IO.File.Copy(tempFileFullPath, newFilePath, true);
            using (var package = new ExcelPackage(fileInfo))
            {
                var sheet1 = package.Workbook.Worksheets[0];
                
                //二维码图片
                // 读图片
                var qrImage = GetQRCodeImg.Get(labelDto.barcode); //把字符串转成图片

                var picture = sheet1.Drawings.AddPicture($"image_{DateTime.Now.Ticks}", qrImage);
                var cell = sheet1.Cells[8, 3];
                // int cellColumnWidthInPix = ExcelHelper.GetWidthInPixels(cell);
                // int cellRowHeightInPix = ExcelHelper.GetHeightInPixels(cell);
                int cellColumnWidthInPix = 100;
                int cellRowHeightInPix = 100;
                int adjustImageWidthInPix = cellColumnWidthInPix;
                int adjustImageHeightInPix = cellRowHeightInPix;


                //图片尺寸适应单元格
                var adjustImageSize = ExcelHelper.GetAdjustImageSize(qrImage, cellColumnWidthInPix, cellRowHeightInPix);
                adjustImageWidthInPix = adjustImageSize.Item1;
                adjustImageHeightInPix = adjustImageSize.Item2;

                //设置为居中显示
                int columnOffsetPixels = (int)((cellColumnWidthInPix - adjustImageWidthInPix) / 2.0);
                int rowOffsetPixels = (int)((cellRowHeightInPix - adjustImageHeightInPix) / 2.0);
                picture.SetSize(adjustImageWidthInPix, adjustImageHeightInPix);
                picture.SetPosition(7,10,2,0);

                sheet1.Cells[3, 2].Value = labelDto.customerType;
                sheet1.Cells[4, 2].Value = labelDto.mpn;
                sheet1.Cells[5, 2].Value = labelDto.partNumber;

                sheet1.Cells[6, 2].Value = labelDto.dateCode;
                sheet1.Cells[7, 2].Value = labelDto.expDate;
                sheet1.Cells[8, 2].Value = labelDto.qty;

                sheet1.Cells[9, 2].Value = labelDto.lotNo;
                sheet1.Cells[10, 2].Value = labelDto.vendor;
                package.Save();
            }
            var stream = System.IO.File.OpenRead(newFilePath);
            return File(stream, "application/vnd.android.package-archive", DateTime.Now.ToString("yyyyMMddHHmmss") + ".xlsx");
        }
```





## C# 正则表达式使用

```C#
for(var i = 0; i< elist.Count;i++){

    if(i == 0 && !string.IsNullOrWhiteSpace(elist[i].NGReason)){
        var NGReason = elist[i].NGReason;
        NGReason = NGReason.Substring(NGReason.IndexOf("，不取"));
        const string pattern = "\\d{1,2}#";
        MatchCollection matches = Regex.Matches(NGReason, pattern,
                                                RegexOptions.IgnoreCase |
                                                RegexOptions.ExplicitCapture);
        NGCount = matches.Count;
        foreach (Match nextMatch in matches)
        {
            string result = nextMatch.ToString();
        }
    }else{
        break;
    }
}
```



## C#截取字符串后几位

```C#
moldno = (dict["lotNo"] ?? "").Trim().Reverse().Take(3).Reverse().ToString(),
```

## query查询条件的创建

```C#
Expression<Func<Manu, bool>> where = x => true;
if (!string.IsNullOrWhiteSpace(input.batchCode))
{
    where = where.And(x => x.batchCode.Contains(input.batchCode));
    var lotNo = (await _batchCodeInfoRepository.Query(where)).First().lotNo;
    where = where.And(x => x.lotNo.Contains(lotNo));
}

if (!string.IsNullOrWhiteSpace(input.lotNo))
{
    where = where.And(x => x.lotNo.Contains(input.lotNo));
}
```
## C#反射获取属性

```C#
        /// <summary>
        /// 获取类中的属性值
        /// </summary>
        /// <param name="FieldName"></param>
        /// <param name="obj"></param>
        /// <returns></returns>
        public static string GetModelValue(string FieldName, object obj)
        {
            try
            {
                Type Ts = obj.GetType();
                object o = Ts.GetProperty(FieldName).GetValue(obj, null);
                string Value = Convert.ToString(o);
                if (string.IsNullOrEmpty(Value)) return null;
                return Value;
            }
            catch
            {
                return null;
            }
        }
        /// <summary>
        /// 设置类中的属性值
        /// </summary>
        /// <param name="FieldName"></param>
        /// <param name="obj"></param>
        /// <returns></returns>
        public static bool SetModelValue(string FieldName, string Value, object obj)
        {
            try
            {
                Type Ts = obj.GetType();
                object v = Convert.ChangeType(Value, Ts.GetProperty(FieldName).PropertyType);
                Ts.GetProperty(FieldName).SetValue(obj, v, null);
                return true;
            }
            catch
            {
                return false;
            }
        }
```



## 提示框

```javascript
this.$message({
    message: '最多输入4条',
    type: 'warning'
})
```

## 带模糊查询的下拉框

```js
<el-col :span="6">
    <el-select v-model="searchForm.ProdId" 
               placeholder="请选择产品" 
               clearable class="el-form-item__content" 
               filterable remote 
               :remote-method="getProdOptions" 
               style="width:100%">
    	<el-option v-for="item in prodOptions" :key="item.value" :label="item.label" :value="item.value" />
    </el-select>
</el-col>

/** 取产品下拉框数据 */
getProdOptions(kewWord) {
    const that = this
    if (kewWord !== '') {
        getProdOptionsByKey(kewWord).then(r => {
            that.prodOptions = r
        })
    } else {
        that.prodOptions = []
    }
}
```

## 表格添加总数量

**添加属性**：`show-summary :summary-method="getSummaries"`

```html

<el-table :data="postRecoreds" stripe style="width: 100%" show-summary :summary-method="getSummaries">
    <el-table-column label="内箱号" align="center" prop="packCode" />
    <el-table-column label="已装数" align="center" prop="productCount" />
    <el-table-column align="center">
        <template slot-scope="scope">
            <el-button type="danger" size="mini" icon="el-icon-delete" @click="handleDelete(scope.$index, scope.row)" />
        </template>
    </el-table-column>
</el-table>
```

**添加函数**:  `getSummaries`

```js
/** 合计 */
getSummaries({ columns }) {
    const sums = []
    const propertylist = ['productCount']
    columns.forEach((column, index) => {
        if (index === 0) {
            sums[index] = '合计:'
            return
        }
        if (propertylist.indexOf(column.property) > -1) {
            debugger
            sums[index] = this.postRecoreds.map(record => record.productCount).reduce((cur, next) => cur + next, 0)
        }
    })
    return sums
}
```



## 新页面对话框组件

**父页面代码**

​	**调用**

```vue
<Slide v-if="slideShow" :propA="propA" @close="slideShow = false" />
```

​	**注册**

```vue
import Slide from './slide'
components: { Slide },
```

​	**数据注册**

```vue
  data() {
    return {
      slideShow: false
    }
  },
```

**显示**

```javascript
<el-button type="success" icon="el-icon-printer" :loading="loading" @click="slideShow = true">对话框</el-button>
```

**新页面文件内代码**

注意点：

1. table内数据绑定正确
2. 生命周期方法，与调用方法不要搞混

```vue
<template>
  <el-dialog :title="getTitle" :visible="true" width="100%" top="10px" @close="handleClose">
    <div class="createPost-main-container">
      <el-table
        ref="tab"
        v-loading="loading"
        :data="value"
        width="65%"
        size="small"
        :span-method="objectSpanMethod"
        border
        stripe
        show-overflow-tooltip="true"
        class="tableSlide"
        :cell-style="cellStyle"
      >
        <el-table-column label="字段名" align="center" prop="MachineCode" />
      </el-table>
    </div>
    <span slot="footer" class="dialog-footer">
      <el-button @click="handleClose">取消</el-button>
      <el-button type="primary" @click="handleSave">确定</el-button>
    </span>
  </el-dialog>
</template>
<script>
// import { GetList } from '@/api/board/workshop-management-board.js'
export default {
  props: {
    propA: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      loading: false,
      Dict: {},
      getHeight: '400px'
    }
  },
  /** 计算 */
  computed: {
    getTitle() { return '拆箱' }
  },
  /** 创建 */
  created() {
    this.loading = true
    // GetList(this.searchForm).then(r => {
    //   this.Dict = r
    // }).finally(_ => (this.loading = false))
    this.getHeight = (window.screen.height - 100) + 'px'
  },

  activated() {

  },
  mounted() {

  },
  methods: {
      handleGetList() {
      },
      handleOpen() {
        this.loading = true
      },
      handleClose() {
        this.$emit('close', false)
      },
  }
}
</script>
<style>

</style>
```










## 折叠表格

**效果：**![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210510133307.png)

**HTML**

```html
  <el-table
    :data="tableData"
    style="width: 100%;margin-bottom: 20px;"
    row-key="id"
    border
    default-expand-all
    :tree-props="{children: 'children'}">
    <el-table-column
      prop="date"
      label="日期"
      sortable
      width="180">
    </el-table-column>
    <el-table-column
      prop="name"
      label="姓名"
      sortable
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="地址">
    </el-table-column>
  </el-table>
```

**js**

```js
data() {
    return {
    tableData: [{
        id: 1,
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
    }, {
        id: 2,
        date: '2016-05-04',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1517 弄'
    }, {
        id: 3,
        date: '2016-05-01',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1519 弄',
        children: [{
            id: 31,
            date: '2016-05-01',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1519 弄'
        }, {
            id: 32,
            date: '2016-05-01',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1519 弄'
        }]
    }, {
        id: 4,
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄'
    }]
    }
}

```

## 保存确认框

```javascript

      this.$confirm('确认删除吗？', '提示', {}).then(() => {
        DeleteListByBoxNo(this.multipleSelection).then(addResult => {
          if (addResult === this.multipleSelection.length) {
            this.$message({
              message: '添加成功',
              type: 'success'
            })
            this.$emit('close', false)
          }
        })
      })

```



## 文本框

```html
    <el-row type="flex" justify="center">
      <el-col :span="6">
        <el-input v-model="searchForm.DeliveryOrderNumber" class="el-form-item__content" clearable placeholder="送货单号" @input="handleGetList" />
      </el-col>
    </el-row>
```



## 时间框

```html
            <el-col :span="8">
              <el-row>
                <el-time-select
                  v-model="searchForm.StartWorkDate"
                  placeholder="起始时间"
                  :picker-options="{
                    start: '00:00',
                    step: '01:00',
                    end: '24:00'
                  }"
                />
                <el-time-select
                  v-model="searchForm.EndWorkDate"
                  placeholder="结束时间"
                  :picker-options="{
                    start: '00:00',
                    step: '01:00',
                    end: '24:00',
                    minTime: searchForm.StartWorkDate
                  }"
                />
              </el-row>
            </el-col>
```



## 日期框

![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210510113907.png)

前端

```html
<!-- 创建日期 -->
<el-col :span="8">
    <el-row>
        <el-date-picker v-model="searchForm.StartProdDate" value-format="yyyy-MM-dd" clearable placeholder="日期" class="el-form-item__content" />
        <label style="margin-left:5px;margin-right:5px">~</label>
        <el-date-picker v-model="searchForm.EndProdDate" value-format="yyyy-MM-dd" clearable placeholder="日期" class="el-form-item__content" />
    </el-row>
</el-col>
```

后端

```c#
if (input.boxTimeFm.HasValue)
{
    where = where.And(x => x.boxTime >= input.boxTimeFm.Value.Add(TimeZoneInfo.Local.BaseUtcOffset));
}
if (input.boxTimeTo.HasValue)
{
    where = where.And(x => x.boxTime <= input.boxTimeTo.Value.Add(TimeZoneInfo.Local.BaseUtcOffset));
}
```



## 前端，获取TOKEN以及当前用户信息

```javascript
import { getInfo } from '@/api/login'
import { getToken } from '@/utils/auth'

getInfo(getToken()).then(r => {
    that.postForm.packer = r.userInfo.LoginAccount
})
```



## 表格单元格条件格式

```javascript

// 设置style
//:cell-style="cellStyle"
cellStyle({ row, columnIndex }) {
    if (row.Status === '待物料' && columnIndex === 2) {
        return {
            backgroundColor: ['red'],
            color: ['black']
        }
    }
}

//设置class
// :cell-class-name="cellClass"
cellStyle({ row, columnIndex }) {
    if (row.Status === '生产中' && columnIndex === 2) {
        return ['green']
    }
    if (row.Status === '待物料' && columnIndex === 2) {
        return ['grey']
    }
    if (row.Status === '设备维修' && columnIndex === 2) {
        return ['pink']
    }
    if (row.Status === '待工单' && columnIndex === 2) {
        return ['orange']
    }
    if (row.Status === '模具保养' && columnIndex === 2) {
        return ['blue']
    }
    if (row.Status === '模具维修' && columnIndex === 2) {
        return ['red']
    }
    if (row.Status === '试模' && columnIndex === 2) {
        return ['yellow']
    }
}
```



## 表格列中添加内容

效果：![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210510115822.png)

前端：

```html
<el-table-column align="center" label="操作" width="280" fixed="right">
    <template slot-scope="scope">
    <el-button v-if="checkPermission(['produce-dailyplan-wobox'])" type="success" size="mini" icon="el-icon-menu" style="margin-right:5px" />
    </template>
</el-table-column>
```

## 报产数据与内外箱表关系
![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210527111902.png)
![image-20210713114440143](D:\books\note\项目笔记\IMES组件.assets\image-20210713114440143.png)

## 内箱表，外箱表，产品表的关联SQL

```SQL
SELECT *
FROM
boxInfo
INNER JOIN boxList ON boxInfo.boxCode = boxList.boxCode
INNER JOIN packageInfo ON boxList.packCode = packageInfo.packCode
INNER JOIN productNumber ON packageInfo.packCode = productNumber.packCode
WHERE
boxInfo.boxCode = 'ACFC337210713032'
```

![image-20210713115356989](D:\books\note\项目笔记\IMES组件.assets\image-20210713115356989.png)

### 项目路径设置别名的2种风格

- 单独src

```js
resolve: {
  alias: {
    '~': resolve(__dirname, 'src')
  }
}

//使用
import stickTop from '~/components/stickTop'
```

+ 各模块独立别名

```js
alias: {
  'src': path.resolve(__dirname, '../src'),
  'components': path.resolve(__dirname, '../src/components'),
  'api': path.resolve(__dirname, '../src/api'),
  'utils': path.resolve(__dirname, '../src/utils'),
  'store': path.resolve(__dirname, '../src/store'),
  'router': path.resolve(__dirname, '../src/router')
}

//使用
import stickTop from 'components/stickTop'
import getArticle from 'api/article'
```





# TODO

### 新需求：新添加页面，添加拦截功能

![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210710103219.png)