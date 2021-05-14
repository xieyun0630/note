## C# 正则表达式式使用
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
that.$message({
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

## 新页面对话框组件

**父页面代码**

​	**调用**

```vue
<Slide v-if="slideShow" :propA="propA" @close="closeSlide" />
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

  **显示/隐藏事件**

```javascript
openSlide() {
	this.slideShow = true
},
closeSlide() {
	this.slideShow = false
}
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

```
    <el-row type="flex" justify="center">
      <el-col :span="6">
        <el-input v-model="searchForm.DeliveryOrderNumber" class="el-form-item__content" clearable placeholder="送货单号" @input="handleGetList" />
      </el-col>
    </el-row>
```



## 日期框

![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210510113907.png)

### 前端

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

### 后端

```c#
if(input.StartCreationDate.HasValue && input.EndCreationDate.HasValue){
    where = where.And(x => x.CreationDate >= input.StartCreationDate);
    where = where.And(x => x.CreationDate < input.EndCreationDate);
}
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

### 前端：

```html
<el-table-column align="center" label="操作" width="280" fixed="right">
    <template slot-scope="scope">
    <el-button v-if="checkPermission(['produce-dailyplan-wobox'])" type="success" size="mini" icon="el-icon-menu" style="margin-right:5px" />
    </template>
</el-table-column>
```

