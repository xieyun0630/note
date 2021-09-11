### 读写工作表数据 [ ](excel_20210911041056251)

```
//读
Console.log(Worksheets.Item(1).Cells.Item(1, 1).Value2)
//写
Worksheets.Item(1).Cells.Item(1, 1).Value2 = 24
```

###  写入数据到单元格里 [ ](excel_20210911041056253)

![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210524111500.png)

###  写入一维数组到单元格里 [ ](excel_20210911041056255)

![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20210524111535.png)



## 出勤统计例子 [ ](excel_20210911041056257)

```javascript
function Macro1()
{
	//参数
	let rangeArr = [
        Range("B2:AE76"),
        Range("B2:AE76"),
        Range("B2:AE76"),
        Range("B2:AE76"),
        Range("B2:AE76"),
        Range("B2:AE76"),
        Range("B2:AE76"),
        Range("B2:AE76"),
        Range("B2:AE76"),
        Range("B2:AE76"),
        Range("B2:AE76"),
        Range("B2:AE76")
    ]
	
	const rowsCount = range.Rows.Count + 1
	const colsCount = range.Columns.Count + 1
    for(let sheetNo = 1;sheetNo <= 12; sheetNo++ ){
        for(let row = 2;row <= rowsCount;row++){
            //当前行数组
            let currentArray = []
            //当前行实际出勤
            let total = Worksheets.Item(sheetNo).Cells.Item(row, colsCount + 1).Value2
            //读取当前行数据到数组
            for(let col=2;col<=colsCount;col++){
                currentArray.push(Worksheets.Item(sheetNo).Cells.Item(row, col).Value2)
            }
            
            
            // 当前总数
            let sum = currentArray.reduce((previousValue, item) => item + previousValue, 0)
            let i = 0
            //小于的情况
            while(total - sum > 5 && total != 0){
                if(currentArray[i%(currentArray.length-1)] == 0){
                    currentArray[i%(currentArray.length-1)] += 8
                }
                
                if(i >= currentArray.length){
                    currentArray[i%(currentArray.length-1)]++
                }
                
                i++
                sum = currentArray.reduce((previousValue, item) => item + previousValue, 0)
            } 
            
            i=0
            //小于的情况
            while( (total - sum) < -5 && total != 0){
                
                if(currentArray[i%currentArray.length] > 14){
                    currentArray[i%currentArray.length]--
                    continue
                }else if(currentArray[i%currentArray.length] > 12){
                    currentArray[i%currentArray.length]--
                    continue
                }else if(currentArray[i%currentArray.length] > 10){
                    currentArray[i%currentArray.length]--
                    continue
                }else if(currentArray[i%currentArray.length] > 8){
                    currentArray[i%currentArray.length]--
                    continue
                }else if(currentArray[i%currentArray.length] > 0){
                    currentArray[i%currentArray.length]--
                    continue
                }
                i++
                sum = currentArray.reduce((previousValue, item) => item + previousValue, 0)
            } 
            Sheets.Item(sheetNo).Range("B" + row).Resize(1,currentArray.length).Value2=currentArray
            Console.log(currentArray.toString() + "实际：" + total + "总数:" + sum)
        }
    }
}
```
