# SpreadJS_ValueSwitching
公式单元格显示公式数值切换

# SpreadJS_ValueSwitching
公式单元格显示公式数值切换

### SpreadJS 示例，公式单元格显示公式/数值切换
该示例包括使用 SpreadJS API 的演示脚本，可用于实现公式单元格显示公式/数值切换
有关 SpreadJS API 的更多信息，请参阅[SpreadJS API指南]( https://demo.grapecity.com.cn/spreadjs/help/api/) 和[帮助手册]( https://help.grapecity.com.cn/pages/viewpage.action?pageId=5963808)。



### 运行步骤
1、在开始之前，请确保您已满足以下先决条件：
要运行 SpreadJS，浏览器必须支持 HTML5，客户端导入和导出 Excel 需要 IE10及以上。
请先了解 [SpreadJS 的产品使用环境]( https://www.grapecity.com.cn/developer/spreadjs/selection-guide/product-use-environment)，并申请临时部署授权激活
安装并更新NodeJS和NPM
2、克隆或下载此代码库
3、初始化控件，并运行示例脚本
#### 控件初始化
首先，创建一个新页面，并在页面上输入以下代码：
```
<!DOCTYPE html>
    <html>
    <head>
        <title>SpreadJS HTML Test Page</title>
```
2、在页面中添加对 SpreadJS 的引用。代码如下。需要注意的是，SpreadJS 提供压缩过
```
//（minified）的 JavaScript 文件和和用于调试的文件：
<script src="[Your_Scripts_Path]/gc.spread.sheets.all.xxxx.min.js" type="text/javascript"></script>
```
3、添加 CSS 文件以改变Spread.JS 的外观。默认的CSS文件名为： 
gc.spread.sheets.xxxx.css，里面包含了所有的默认样式。该 CSS 文件将会影响滚动条，筛选框及其子元素，单元格和下方标签栏的样式。引入 CSS 的代码如下：
```
//<link href="[Your_CSS_Path]/gc.spread.sheets.xxxx.css" rel="stylesheet" type="text/css"/>
```
4、添加产品授权，代码为（本地测试可以不添加）：
```
GC.Spread.Sheets.LicenseKey = "xxx";
```
5. 添加控件初始化代码。本例会在一个 id 为 “ss” 的 DOM 元素上初始化 SpreadJS：
```
<script type="text/javascript">
// Add your license
// If run this in local for testing, remove or comment below code
 GC.Spread.Sheets.LicenseKey = "xxx";

// Add your code
 window.onload = function(){
var spread = new GC.Spread.Sheets.Workbook(document.getElementById("ss"),{sheetCount:3});
var sheet = spread.getActiveSheet();
 }
</script>
</head>
<body>
```
6、 创建一个 id 为 “ss” 的元素，SpreadJS 将在该 DOM 中初始化：
```
<div id="ss" style="height: 500px; width: 800px"></div>
</body>
</html>
```
#### 示例代码
```
HTML：
<p>公式单元格显示公式/数值切换</p>
<h6>点击按钮留意E4的变化</h6>
<button id="btn">显示/隐藏公式</button>
<div id="ss"></div>

CSS：
p{
    text-align: center;
    color: #336699;
}

button{
    margin-bottom: 10px;
}

#ss{
    width: 100%;
    height: 400px;
}

JavaScript：
// Title:显示公式
// Description：显示公式
// Tag:公式

var spread = new GC.Spread.Sheets.Workbook(document.getElementById("ss"));
var sheet2 = spread.getActiveSheet();
var spreadNS = GC.Spread.Sheets;
sheet2.setArray(1, 1, [
    ["序号", "底边长", "高", "面积"],
    [1, 4, 5],
    [2, 3, 4]
]);
sheet2.addSpan(0, 1, 1, 4);
sheet2.setValue(0, 1, "计算三角形面积");
sheet2.getRange(0, 1, 1, 1).hAlign(spreadNS.HorizontalAlign.center);
sheet2.setFormula(2, 4, '=(C3*D3)/2');
sheet2.setValue(2, 0, '使用普通公式:');
sheet2.setValue(3, 0, '使用自定义单元格:');
sheet2.setFormula(3, 4, '=(C4*D4)/2');
sheet2.setColumnWidth(4, 180);

function ShowFormula() {}
ShowFormula.prototype = new GC.Spread.Sheets.CellTypes.Text();
ShowFormula.prototype.paint = function(ctx, value, x, y, w, h, style, context) {
    let formula = context.sheet.getFormula(context.row, context.col);
    // 判断当formulaFlg为true时才显示
    if (formulaFlg && formula) {
        value = "=" + formula;
    }
    spreadNS.CellTypes.Base.prototype.paint.apply(this, [ctx, value, x, y, w, h, style, context]);
}

// 控制是否显示formula
var formulaFlg = false;

function showFormulaFun() {
    formulaFlg = !formulaFlg;
    sheet2.repaint();
}
showFormulaFun();
$("#btn").click(showFormulaFun);
var showFormulaType = new ShowFormula();
sheet2.setCellType(3, 4, showFormulaType);
```
#### 关于 SpreadJS
[SpreadJS]( https://www.grapecity.com.cn/developer/spreadjs) 是一款基于 HTML5 的纯前端表格控件，兼容 450 多种 Excel 公式，具备“高性能、跨平台、与 Excel 高度兼容”的产品特性。使用 SpreadJS，可直接在 Angular、 React、 Vue 等前端框架中实现高效的模板设计、在线编辑和数据绑定等功能，为最终用户提供高度类似 Excel 的使用体验。

