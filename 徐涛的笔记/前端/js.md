# 1. js
## 1.1. js基础原生方法
### 1.1.1. js其他小知识
    JavaScript 严格模式(use strict)
![](_v_images/20190927151307587_14260.png =72x)


### 1.1.2. js数组常用方法整理
[链接](https://www.cnblogs.com/jinzhou/p/9072614.html)
### 1.1.3. 提交表单下载文件excel
```
//DMS 导出表单提交，由于现在没有找到jquery的解决办法，现在先通过W3C的标准实现
function dmsExportSubmit(url,form){
	var formId = form||"fm";
	var currDate = new Date();
	var url2 = (url+(url.lastIndexOf("?")!=-1?"&xxx="+currDate.getMilliseconds():"?xxx="+currDate.getMilliseconds()));
	document.getElementById(formId).action = (url2);
	document.getElementById(formId).submit();
}
```

### 1.1.4. js数组的过滤

```js
var oldArr = [
  1,2,5,7
];
//普通数组
var newArr=oldArr.filter(function (item) {//item数组里面的对象
	console.log(item);
	if(item==5){
		return  false;//舍弃
	}else{
		return true;//保留
	}
	

});

///!!!!!!!!!!!注意 过滤后产生的是新的数组   oldArr=newArr;才能把原来的过滤掉
console.log(newArr);

//---对象数据

var arrOldObj = [
  { id: 1, text: 'aa', done: true },
  { id: 2, text: 'bb', done: false }
];
var newArrObj=arrOldObj.filter(function (item) {//item数组里面的对象
	console.log(item);
	if(item.done){
		return true;//保留
	}else{
		return  false;//舍弃
	}
});
console.log(newArrObj);

```

### 1.1.5. js-json对象常用方法
[链接](https://www.cnblogs.com/huangshuqiang/p/8886746.html)

### 1.1.6. js字符串操作

#### 1.1.6.1. 数字位数不够，进行前补零的JS最简实现方案
```js

代码实现
/**
* 自定义函数名：PrefixZero
* @param num： 被操作数
* @param n： 固定的总位数
*/
function PrefixZero(num, n) {
    return (Array(n).join(0) + num).slice(-n);
}
具体示例
var myNum = 9;
var myNum2 = 12;

console.log('原变量myNum：'+myNum);//9
console.log('处理后myNum：'+PrefixZero(myNum, 3));//009
 
console.log('原变量myNum2：'+myNum2);
console.log('处理后myNum2：'+PrefixZero(myNum2, 3));//012

```







#### 1.1.6.2. 字符串替换
```js

console.log("2018/08/08".replace(/\//g, '-'));


```

```js

#### 按对应字符分割成数组


var valid_date="2007.04.02-2027.04.02";
var startDate = valid_date.split("-")[0];
var endDate = valid_date.split("-")[1];

```



#### 1.1.6.3. 字符串截取str.substring(开始包含,结束包含);

```js

var str ="0,123,456";
if(str!='0'){
	str=str.substring(2,str.length);
	//str=str.substring(2);截取str后面全部
}
console.log(str);

```
#### 1.1.6.4. 数组join，数组转字符串。按照对应分割

```
在本例中，我们将使用分隔符来分隔数组中的元素：

<script type="text/javascript">

var arr = new Array(3)
arr[0] = "George"
arr[1] = "John"
arr[2] = "Thomas"

document.write(arr.join("."))

</script>
输出：

George.John.Thomas

```




### 1.1.7. js时间日期操作
#### 1.1.7.1. js日期的比较
[链接](https://www.cnblogs.com/holddie/p/7411848.html)

```js

Js 日期比较方法
第一种方式
function compareDate(s1,s2){
  return ((new Date(s1.replace(/-/g,"\/")))>(new Date(s2.replace(/-/g,"\/"))));
}
第二种方式
var curTime = new Date();
//把字符串格式转化为日期类
var starttime = new Date(Date.parse(begintime));
var endtime = new Date(Date.pares(endtime));
//进行比较
return (curTime>=starttime && cutTime<=endtime);

```




#### 1.1.7.2. 快速计算年龄

```js

function Age(status, index) {
var aDate = new Date();

var thisYear = aDate.getFullYear();
var bDate = new Date(status);
var brith = bDate.getFullYear();
var age = (thisYear - brith);
return age;
}

```


#### 1.1.7.3. js日期格式化

```js
// 对Date的扩展，将 Date 转化为指定格式的String   
// 月(M)、日(d)、小时(h)、分(m)、秒(s)、季度(q) 可以用 1-2 个占位符，   
// 年(y)可以用 1-4 个占位符，毫秒(S)只能用 1 个占位符(是 1-3 位的数字)   
// 例子：   
// (new Date()).Format("yyyy-MM-dd hh:mm:ss.S") ==> 2006-07-02 08:09:04.423   
// (new Date()).Format("yyyy-M-d h:m:s.S")      ==> 2006-7-2 8:9:4.18   
Date.prototype.Format = function(fmt)   
{ //author: meizz   
  var o = {   
    "M+" : this.getMonth()+1,                 //月份   
    "d+" : this.getDate(),                    //日   
    "h+" : this.getHours(),                   //小时   
    "m+" : this.getMinutes(),                 //分   
    "s+" : this.getSeconds(),                 //秒   
    "q+" : Math.floor((this.getMonth()+3)/3), //季度   
    "S"  : this.getMilliseconds()             //毫秒   
  };   
  if(/(y+)/.test(fmt))   
    fmt=fmt.replace(RegExp.$1, (this.getFullYear()+"").substr(4 - RegExp.$1.length));   
  for(var k in o)   
    if(new RegExp("("+ k +")").test(fmt))   
  fmt = fmt.replace(RegExp.$1, (RegExp.$1.length==1) ? (o[k]) : (("00"+ o[k]).substr((""+ o[k]).length)));   
  return fmt;   
}



var time1 = new Date().Format("yyyy-MM-dd HH:mm:ss");     
  
var time2 = new Date().Format("yyyy-MM-dd");  
```
#### 1.1.7.4. 多少秒转对应时分秒

```js
function GetSecondTimeFomate(a) {
            var h = (parseInt(a / 3600));
            if (h.toString().length == 1) {
                h = "0" + h;
            }
            var m = (parseInt((a % 3600) / 60));
            if (m.toString().length == 1) {
                m = "0" + m;
            }
            var s = (a - 3600 * h - 60 * m);
            if (s.toString().length == 1) {
                s = "0" + s;
            }
            return (h + ":" + m + ":" + s)
        }
```



### 1.1.8. json字符串与对象相互转换
```js
JSON字符串:
var str1 = '{ "name": "cxh", "sex": "man" }'; 
JSON对象:
var str2 = { "name": "cxh", "sex": "man" };
一、JSON字符串转换为JSON对象
    var obj = str.parseJSON(); //由JSON字符串转换为JSON对象
    * var obj = JSON.parse(str); //由JSON字符串转换为JSON对象
二、可以使用toJSONString()或者全局方法JSON.stringify()将JSON对象转化为JSON字符串。
    var last=obj.toJSONString(); //将JSON对象转化为JSON字符
    * var last=JSON.stringify(obj); //将JSON对象转化为JSON字符    
```
### 1.1.9. 余总将俩个相同的对象添加为数组形式
```js
var json = [];
var row = {};
$("#spouseInfo :input").each(function(){
    debugger;
      var key = $(this).attr("name");
      row[key]= $(this).val();
      if(key=='enddate'){
      	json.push(row);
      	row = {};
      }
  	

});
```
![mZMr6K.png](https://s2.ax1x.com/2019/08/16/mZMr6K.png)
### 1.1.10. js初始化自执行
1. 放在紧接着script后面的函数
+ $(function(){ });//文档加载好
+ (function () { console.log('自执行1'); } ());

### 1.1.11. js对象数组(JSON) 根据某个共同字段 分组
[js对象数组(JSON) 根据某个共同字段 分组](https://www.cnblogs.com/rysinal/p/5834446.html)
> js建议使用vscode测试

```js
var  arr  = [
{ "id":  "1001", "name":  "值1", "value":  "111" },
{ "id":  "1001", "name":  "值1", "value":  "11111" },
{ "id":  "1002", "name":  "值2", "value":  "25462" },
{ "id":  "1002", "name":  "值2", "value":  "23131" },
{ "id":  "1002", "name":  "值2", "value":  "2315432" },
{ "id":  "1003", "name":  "值3", "value":  "333333" }
];

var map = {},
    dest = [];
for (var i = 0; i < arr.length; i++) {
    var ai = arr[i];
    if (!map[ai.id]) {
        dest.push({
            id: ai.id,
            // name: ai.name,
            data: [ai]
        });
        map[ai.id] = ai;
    } else {
        for (var j = 0; j < dest.length; j++) {
            var dj = dest[j];
            if (dj.id == ai.id) {
                dj.data.push(ai);
                break;
            }
        }
    }
}

console.log(dest);
debugger;
```
### 1.1.12. 根据数组对应分类map值对象
```js
var  arr  =
[{CODE_NAME:  "已保存", REMARK:  "借款申请单状态", CODE_TYPE:  2064, CODE:  20641001}
,{CODE_NAME:  "征信待查", REMARK:  "借款申请单状态", CODE_TYPE:  2064, CODE:  20641002}
,{CODE_NAME:  "征信已查", REMARK:  "借款申请单状态", CODE_TYPE:  2064, CODE:  20641003}
,{CODE_NAME:  "内勤大数据录入", REMARK:  "借款申请单状态", CODE_TYPE:  2064, CODE:  20641004}
,{CODE_NAME:  "风控电核审核", REMARK:  "借款申请单状态", CODE_TYPE:  2064, CODE:  20641005}]
;

var  map  = {},
dest  = [];
for (var  i  =  0; i  <  arr.length; i++) {
var  obj=arr[i];
var  key=obj.CODE;
var  val=obj.CODE_NAME;
map[key]=val;
}

console.log(map);
debugger;
```

### 1.1.13. 动态添加的标签绑定click事件不响应
[动态添加的标签绑定click事件不响应和关于IOS下click事件委托失效的解决方案](https://blog.csdn.net/u011784205/article/details/76522091)

## 1.2. jquery

### 1.2.1. jquery插件库及自定义方法
#### 1.2.1.1. jQuery Validate 插件为表单提供了强大的验证功能
[链接](https://www.runoob.com/jquery/jquery-plugin-validate.html)
#### 1.2.1.2. jquery serializeobject();方法序列化表单的属性，返回字符串。
[链接](https://blog.csdn.net/lg12lp12/article/details/76443715)
> 禾下cms得出的数据（字符串）

```js


var obj={
	"loanId": "578",
	"idCard": "110101199003076181",
	"customerName": "李雪晴",
	"mobilePhone": "18655303551",
	"sendBank": "20701001",
	"carType": "0",
	"familyAddress": "安徽芜湖",
	"intentionPrice": "18000.00",
	"issueAuthority": "安徽芜湖机关",
	"startDate": "2000-01-01",
	"endDate": "2020-01-01",
	"spouseId": "32,33",
	"idcard": ",",
	"username": ",",
	"phonenum": ",",
	"isquerycredit": "0,0",
	"userrelationship": ",",
	"familyaddress": ",",
	"issueauthority": ",",
	"startdate": ",",
	"enddate": ","
};

```



> 可以将表单中的文本框 下拉框 根据name 属性 序列化成字符串，必须在js中写这个方法

```js
serializeobject(); 可以将表单中的文本框 下拉框 根据name 属性 序列化成字符串，必须在js中写这个方法

$.fn.serializeObject = function() {
    var o = {"unique_id":new Date().getTime(),"state":false};
    var a = this.serializeArray();
    $.each(a, function() {
        if (o[this.name]) {
            if (!o[this.name].push) {
                o[this.name] = [o[this.name]];
            }
            o[this.name].push(this.value || '');
        } else {
            o[this.name] = this.value || '';
        }
    });
    return o;
};

<form class="form-horizontal m-t" id="design_task_form" οnsubmit="return false">
                        <div class="form-group">
                            <label class="col-sm-3 control-label" style="margin-left: 15%;">制作项目：</label>
                            <div class="col-sm-6">
                                <select style="width:245px;"  class="chosen-select" data-id="task_item" id="task_item" name="task_item"></select>
                                <input type="hidden" id="f_task_item" value="${designTask.task_item}">
                            </div>
                        </div>
                        <div class="hr-line-dashed"></div>
                        <div class="form-group">
                            <label class="col-sm-3 control-label" style="margin-left: 15%;">制作类别：</label>
                            <div class="col-sm-6">
                                <select style="width:245px;"  class="chosen-select" data-id="task_classify" id="task_classify" name="task_classify"></select>
                                <input type="hidden" id="f_task_classify" value="${designTask.task_classify}">
                            </div>
                        </div>
                        <div class="hr-line-dashed"></div>
                        <div class="form-group">
                            <label class="col-sm-3 control-label" style="margin-left: 15%;">色别：</label>
                            <div class="col-sm-6">
                                <%-- <input id="color" name="" class="form-control required" value="${designTask.color}"> --%>
                                <select style="width:245px;"  class="chosen-select" data-id="color" id="color" name="color"></select>
                                <input type="hidden" id="f_color" name="f_color" value="${designTask.color}">
                            </div>
                        </div>
                        <div class="hr-line-dashed"></div>
                        <div class="form-group">
                            <label class="col-sm-3 control-label" style="margin-left: 15%;">数量：</label>
                            <div class="col-sm-6">
                                <input id="quantity" style="width:245px;" name="quantity" class="form-control required" value="${designTask.quantity}">
                            </div>
                        </div>
                        <div class="hr-line-dashed"></div>
                        <div class="form-group">
                            <label class="col-sm-3 control-label" style="margin-left: 15%;">单位：</label>
                            <div class="col-sm-6">
                                <select style="width:245px;"  class="chosen-select" data-id="unit" id="unit" name="unit" value="${designTask.unit}"></select>
                                <input type="hidden" id="f_unit" value="${designTask.unit}">
                            </div>
                        </div>
                        <%-- <div class="hr-line-dashed"></div>
                        <div class="form-group">
                            <label class="col-sm-3 control-label" style="margin-left: 15%;">设计人：</label>
                            <div class="col-sm-6">
                                <select style="width:245px;"  class="chosen-select" data-id="server" id="designer" name="designer">
                                    <c:forEach items="${userList}" var="user" varStatus="status">
                                        <option value="${user.user_id}" id="user${user.user_id}">${user.true_name}</option>
                                    </c:forEach>
                                </select>
                                <input type="hidden" id="f_designer" value="${designTask.designer}">
                                <input type="hidden" id="designer_name" name="designer_name">
                            </div>
                        </div> --%>
                        <input type="hidden" id="designer" name="designer" value="${designTask.designer}">
                        <input type="hidden" id="designer_name" name="designer_name" value="${designTask.designer_name}">
                        <div class="hr-line-dashed"></div>
                        <div class="form-group">
                            <label class="col-sm-3 control-label" style="margin-left: 15%;">完成时间：</label>
                            <div class="col-sm-6">
                                <input placeholder="完成时间" style="width:245px;" class="form-control layer-date required" id="finish_date" name="finish_date" value="<fmt:formatDate value="${designTask.finish_date}" pattern="yyyy-MM-dd HH:mm:ss"/>">
                            </div>
                        </div>
                    </form>
 ———————————————— 
版权声明：本文为CSDN博主「奋斗的怪怪程序猿」的原创文章，遵循CC 4.0 by-sa版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/lg12lp12/article/details/76443715
```

### 1.2.2. jquery常用方法
>  .addClass("class1") 
> .removeClass("class1")
> .hasClass("intro")
> jQuery中的empty()方法：些方法可以清空/删除指定元素下的所以子节点或是内容 $(selector).empty()
### 1.2.3. jquery（serialize()、serializeArray()）序列化表单的方法总结
```js
 $("#test_form").serialize();    > username=xt&age=18
 $("#test_form").serializeArray() > 
[ 
     {name: 'firstname', value: 'Hello'}, 
     {name: 'lastname', value: 'World'},
     {name: 'alias'}, // this one was empty
  ]



//禾下cms内容
var formArr=$("#form-addWorkExperience").serializeArray();
var formSerializeObj={};
for(var i in formArr){
	formSerializeObj[formArr[i].name]=formArr[i].value;
}

console.log(formSerializeObj);//json
var submitFormData=JSON.stringify(formSerializeObj);//转json字符串
console.log(submitFormData);

```



### jquery插入元素方法

```js
append() - 在被选元素的结尾插入内容 -内部
prepend() - 在被选元素的开头插入内容 -内部
after() - 在被选元素之后插入内容    -外部
before() - 在被选元素之前插入内容    -外部

```

---
### 1.2.4. jquery普通元素选择器
[链接](https://www.cnblogs.com/onlys/articles/jQuery.html)

```js

jQuery 的选择器可谓之强大无比，这里简单地总结一下常用的元素查找方法 
 
$("#myELement")    选择id值等于myElement的元素，id值不能重复在文档中只能有一个id值是myElement所以得到的是唯一的元素 
$("div")           选择所有的div标签元素，返回div元素数组 
$(".myClass")      选择使用myClass类的css的所有元素 
$("*")             选择文档中的所有的元素，可以运用多种的选择方式进行联合选择：例如$("#myELement,div,.myclass") 
 
层叠选择器： 
$("form input")         选择所有的form元素中的input元素 
$("#main > *")          选择id值为main的所有的子元素 
$("label + input")     选择所有的label元素的下一个input元素节点，经测试选择器返回的是label标签后面直接跟一个input标签的所有input标签元素 
$("#prev ~ div")       同胞选择器，该选择器返回的为id为prev的标签元素的所有的属于同一个父元素的div标签 
 
基本过滤选择器： 
$("tr:first")               选择所有tr元素的第一个 
$("tr:last")                选择所有tr元素的最后一个 
$("input:not(:checked) + span")   
 
过滤掉：checked的选择器的所有的input元素 
 
$("tr:even")               选择所有的tr元素的第0，2，4... ...个元素（注意：因为所选择的多个元素时为数组，所以序号是从0开始） 
 
$("tr:odd")                选择所有的tr元素的第1，3，5... ...个元素 
$("td:eq(2)")             选择所有的td元素中序号为2的那个td元素 
$("td:gt(4)")             选择td元素中序号大于4的所有td元素 
$("td:ll(4)")              选择td元素中序号小于4的所有的td元素 
$(":header") 
$("div:animated") 
内容过滤选择器： 
 
$("div:contains('John')") 选择所有div中含有John文本的元素 
$("td:empty")           选择所有的为空（也不包括文本节点）的td元素的数组 
$("div:has(p)")        选择所有含有p标签的div元素 
$("td:parent")          选择所有的以td为父节点的元素数组 
可视化过滤选择器： 
 
$("div:hidden")        选择所有的被hidden的div元素 
$("div:visible")        选择所有的可视化的div元素 
属性过滤选择器： 
 
$("div[id]")              选择所有含有id属性的div元素 
$("input[name='newsletter']")    选择所有的name属性等于'newsletter'的input元素 
 
$("input[name!='newsletter']") 选择所有的name属性不等于'newsletter'的input元素 
 
$("input[name^='news']")         选择所有的name属性以'news'开头的input元素 
$("input[name$='news']")         选择所有的name属性以'news'结尾的input元素 
$("input[name*='man']")          选择所有的name属性包含'news'的input元素 
    根据经验  $("input[class~='isIdCard']")          选择所有的class属性包含'isIdCard'的input元素 和上面具有同样的效果
 
$("input[id][name$='man']")    可以使用多个属性进行联合选择，该选择器是得到所有的含有id属性并且那么属性以man结尾的元素 
 
子元素过滤选择器： 
 
$("ul li:nth-child(2)"),$("ul li:nth-child(odd)"),$("ul li:nth-child(3n + 1)") 
 
$("div span:first-child")          返回所有的div元素的第一个子节点的数组 
$("div span:last-child")           返回所有的div元素的最后一个节点的数组 
$("div button:only-child")       返回所有的div中只有唯一一个子节点的所有子节点的数组 
 
表单元素选择器： 
 
$(":input")                  选择所有的表单输入元素，包括input, textarea, select 和 button 
 
$(":text")                     选择所有的text input元素 
$(":password")           选择所有的password input元素 
$(":radio")                   选择所有的radio input元素 
$(":checkbox")            选择所有的checkbox input元素 
$(":submit")               选择所有的submit input元素 
$(":image")                 选择所有的image input元素 
$(":reset")                   选择所有的reset input元素 
$(":button")                选择所有的button input元素 
$(":file")                     选择所有的file input元素 
$(":hidden")               选择所有类型为hidden的input元素或表单的隐藏域 
 
表单元素过滤选择器： 
 
$(":enabled")             选择所有的可操作的表单元素 
$(":disabled")            选择所有的不可操作的表单元素 
$(":checked")            选择所有的被checked的表单元素 
$("select option:selected") 选择所有的select 的子元素中被selected的元素 

```

### 1.2.5. jquery兄弟父子选择器
```js
jQuery.parent(expr) 找父亲节点，可以传入expr进行过滤，比如("span").parent()或者(“span”).parent(“.class”)

jQuery.parents(expr),类似于jQuery.parents(expr),但是是查找所有祖先元素，不限于父元素

jQuery.children(expr).返回所有子节点，这个方法只会返回直接的孩子节点，不会返回所有的子孙节点

jQuery.contents(),返回下面的所有内容，包括节点和文本。这个方法和children()的区别就在于，包括空白文本，也会被作为一个

jQuery对象返回，children()则只会返回节点

jQuery.prev()，返回上一个兄弟节点，不是所有的兄弟节点

jQuery.prevAll()，返回所有之前的兄弟节点

jQuery.next(),返回下一个兄弟节点，不是所有的兄弟节点

jQuery.nextAll()，返回所有之后的兄弟节点

jQuery.siblings(),返回兄弟姐妹节点，不分前后

jQuery.find(expr),跟jQuery.filter(expr)完全不一样。jQuery.filter()是从初始的jQuery对象集合中筛选出一部分，而jQuery.find()

的返回结果，不会有初始集合中的内容，比如$(“p”),find(“span”),是从

p元素开始找,等同于$(“p span”)

```

### 1.2.6. jsonp

```

//ajax请求
$.ajax({
	url: "http://cross-domain/get_data",
	dataType: "jsonp"， //指定服务器返回的数据类型
	jsonp: "invoker", //指定参数名称
	jsonpCallback: "handleData" //指定回调函数
}).done(function(resp_data) {
	console.log("Ajax Done!");
}).fail(...);
————————————————
版权声明：本文为CSDN博主「般若Neo」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/hwhsong/article/details/84070918



		$.ajax({
			url: "http://suggestion.baidu.com/s?wd=苹果&cb=callback&param=gg&callback=?",
			type: 'post', 
			dataType: 'json',
			jsonp: 'callback',
			jsonpCallback: 'callback',
			crossDomain: true,
			timeout: 30000,
			success: function(result) {
				console.log(result)
			},
			error: function(jqXHR, textStatus, errorThrown) {},
			complete: function(jqXHR, status) {}
		});

```



### 1.2.7. ajax


```js
var path = "${pageContext.request.contextPath}/dd/businessManagement/customerCreditApplication";
$.ajax({
    url: path + "/customerCreditApplicationInitQuery",
    data: "limit=" + limit ,
    type: "post",
    //async: false,//false为同步
    dataType: "json",
    success: function(obj) {

    }
});

$(function(){
    $.ajax({
        url: '/path/to/file',
        type: 'get or post',
        dataType: 'default: Intelligent Guess (Other values: xml, json, jsonp, script, or html)',
        data: {param1:'value1', param2:'value2'},
        jsonp: "jsoncallback", //ajax跨域写法
        async: true, //默认值: true。默认设置下，所有请求均为异步请求。如果需要发送同步请求，请将此选项设置为false。
        processData: false, // 告诉jQuery不要去处理发送的数据
        contentType: false, // 告诉jQuery不要去设置Content-Type请求头
        success: function (data){
            /*当请求之后调用。传入返回后的数据，以及包含成功代码的字符串。*/
        },
        dataFilter: function(){
            /*在请求成功之后调用。传入返回的数据以及 "dataType" 参数的值。并且必须返回新的数据（可能是处理过的）传递给 success 回调函数。*/
        },
        error: function(){
            /*在请求出错时调用*/
        },
        beforeSend: function(){
            /*在发送请求之前调用*/
        },
        complete: function(){
            /*当请求完成之后调用这个函数*/
        }
    });
})
```
### 1.2.8. jquery杂项方法-filter数组过滤-建议使用grep
```js
var  newArr  =  queryBankParam.filter(function (p) {
    //console.log(p); 
    return  p.CODE_TYPE  ==  1005;
    }).filter(function (p) {
    return  p.CODE  ==  value;
    });
    if (newArr.length  ==  0) {
    return  '-';
    } else {

    return  newArr[0].CODE_NAME;
    }
```

### 1.2.9. jquery杂项方法grep-过滤并返回满足指定函数的数组元素
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
<style>
    div {
        color: blue;
    }
    p {
        color: green;
        margin: 0;
    }
    span {
        color: red;
    }
</style>    
<script src="https://cdn.staticfile.org/jquery/1.10.2/jquery.min.js"></script>
</head>
<body>
    
    
    
<div></div>
<p></p>
<span></span>
<script>
/*
1, 9, 3, 8, 6, 1, 5, 9, 4, 7, 3, 8, 6, 9, 1

1, 9, 4, 7, 3, 8, 6, 9, 1

1, 4, 7, 3, 8, 6, 1

*/
$(function () { 
    var arr = [ 1, 9, 3, 8, 6, 1, 5, 9, 4, 7, 3, 8, 6, 9, 1 ];
    $( "div" ).text( arr.join( ", " ) );//显示
    
    arr = jQuery.grep(arr, function( n, i ) {//第一次过滤 n !== 5 && i > 4 n代表元素值 i代表当前值的下表
        return ( n !== 5 && i > 4 );
    });
    $( "p" ).text( arr.join( ", " ) ); 
    
    
    arr = jQuery.grep(arr, function( a ) {
        return a !== 9;
    });//第二次过滤 a !== 9;
    
    $( "span" ).text( arr.join( ", " ) );//显示
})
</script>
 
</body>
</html>
```

### 1.2.10. jquery，代替toggle()绑定多个click事件方法
1. 方法一
```js
$(".btn").on("click",function(){
    //通过判断按钮btn有没有active这个class名判断是否已经点击过
    if($(this).hasClass("active")){
    //如果有了active，假设已经点击过了
    //执行你的代码
    //把active去掉
    $(this).removeClass("active");
    }else{
    //没有active，假设还没有点击过
    //执行你的代码
    $(this).addClass("active");
    }
})
```
2. 方法二  [https://blog.csdn.net/chaplinlong/article/details/51198578](https://blog.csdn.net/chaplinlong/article/details/51198578)

### 1.2.11. jquery合并对象


![](_v_images/20190927145951356_12991.png =123x)

### 1.2.12. $.fn.method()=function(){}和$.fn.extend({})的比较
[链接](https://www.cnblogs.com/qicao/p/8568158.html)

### 1.2.13. jquery扩展函数extend，提前设置bootstrap-inputfile默认值
    !function(){}
    都是跟(function(){})();这个函数是一个意思，都是告诉浏览器自动运行这个匿名函数的，因为!+()这些符号的运算符是最高的，所以会先运行它们后面的函数


[Bootstrap FileInput(文件上传)中文API整理](https://segmentfault.com/a/1190000018477200?utm_source=tag-newest)
> 禾下cms线索 dms-tools.js UploaderController。根据 uploadUrl: "index.php", //上传的地址追踪js得到线索

![](_v_images/20190927143928479_27066.png =106x)
![](_v_images/20190927142833639_21232.png =118x)
    $.extend(true, $.fn.fileinput.defaults, defaults);
    



## 1.3. js高级
### 1.3.1. js对象原型
[链接](https://www.w3school.com.cn/js/js_object_prototypes.asp)

```js

JavaScript prototype 属性也允许您为对象构造器添加新方法：

实例
function Person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
}
Person.prototype.name = function() {
    return this.firstName + " " + this.lastName;
};

```

### 1.3.2. .then()的用法

    异步
    
[js中then()的用法](https://blog.csdn.net/chengmo123/article/details/89281022)

    如下载图片中的getBase64(src,i).then(function(data){
![](_v_images/20190930170243650_6629.png =65x)


### 1.3.3. JavaScript 全局对象
[JavaScript 全局对象](https://www.w3school.com.cn/jsref/jsref_obj_global.asp)

### 1.3.4. js中如何将数组转化为base64encode的字符串
[链接](https://segmentfault.com/q/1010000007195539)

```js

            function base64Encode(input) {
                var rv;
                rv = encodeURIComponent(input);
                rv = unescape(rv);
                rv = window.btoa(rv);
                return rv;
            }
            function base64Decode(input) {
                rv = window.atob(input);
                rv = escape(rv);
                rv = decodeURIComponent(rv);
                return rv;
            }
            var arry = [21, 23, 0, 0, 0, 0, 21, 255, 43, 154, 87, 32, 4, 13, 64, 7, 86, 52, 1, 23, 16, 57, 73, 1];
            var str = base64Encode(arry);//转换字符串
            console.log(str);
            var arry2= base64Decode(str).split(',');
            console.log(arry2);//转回数组


```

### 1.3.5. base64转码
[链接](https://blog.csdn.net/zhumizhumi/article/details/90375358)
[链接](https://wangdoc.com/javascript/types/string.html#参考链接)

```html

一、使用Base64 转码原因
（1）有时，文本里面包含一些不可打印的符号，比如 ASCII 码0到31的符号都无法打印出来，这时可以使用 Base64 编码，将它们转成可以打印的字符

（2）有时需要以文本格式传递二进制数据，那么也可以使用 Base64 编码

二、Base64 转码定义和目的
所谓 Base64 就是一种编码方法，可以将任意值转成 0～9、A～Z、a-z、+和/这64个字符组成的可打印字符。使用它的主要目的，不是为了加密，而是为了不出现特殊字符，简化程序的处理

三、Base64 转码的方法及例子
JavaScript 原生提供两个 Base64 相关的方法

btoa()：任意值转为 Base64 编码
atob()：Base64 编码转为原来的值
 （1）ASCII 码字符转码和复原

var string = 'Hello World!'
// 转为 Base64 编码
console.log(btoa(string)) // SGVsbG8gV29ybGQh
// 转为原来的值
console.log(atob('SGVsbG8gV29ybGQh')) // "Hello World!"
（2）非ASCII 码字符转码和复原

btoa('你好') // 报错 VM319:1 Uncaught DOMException: Failed to execute 'btoa' on 'Window': The string to be encoded contains characters outside of the Latin1 range.
    at <anonymous>:1:1
要将非 ASCII 码字符转为 Base64 编码，必须中间插入一个转码环节，再使用这两个方法。

encodeURIComponent是非ASCII 码字符转为 Base64 编码时使用

function b64Encode(str) {
  return btoa(encodeURIComponent(str));
}
b64Encode('你好') // "JUU0JUJEJUEwJUU1JUE1JUJE"
decodeURIComponent是非ASCII 码字符转为原值的时候使用(注意两者使用位置的细节差别)

function b64Decode(str) {
  return decodeURIComponent(atob(str));
}
b64Decode('JUU0JUJEJUEwJUU1JUE1JUJE') // "你好"
借鉴作者：https://wangdoc.com/javascript/types/string.html#%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5
————————————————
版权声明：本文为CSDN博主「胭脂ing」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/zhumizhumi/article/details/90375358



```


### 1.3.6. 图片转base64
[链接](https://www.cnblogs.com/zhangdiIT/p/7895903.html)

> 场景三：将网络图片资源转化为base64，（感觉场景二中的资源换成绝对路径即可使用在场景三中）

```js
function startToBase64(){
    　　 //这是网上的一张图片链接
    　　 var url="http://p1.pstatp.com/large/435d000085555bd8de10";
        getBase64(url)
            .then(function(base64){
                  console.log(base64);//处理成功打印在控制台
            },function(err){
                  console.log(err);//打印异常信息
            });                        
    }    

    //传入图片路径，返回base64
    function getBase64(img){
        function getBase64Image(img,width,height) {//width、height调用时传入具体像素值，控制大小 ,不传则默认图像大小
          var canvas = document.createElement("canvas");
          canvas.width = width ? width : img.width;
          canvas.height = height ? height : img.height;
 
          var ctx = canvas.getContext("2d");
          ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
          var dataURL = canvas.toDataURL();
          return dataURL;
        }
        var image = new Image();
        image.crossOrigin = '';
        image.src = img;
        var deferred=$.Deferred();
        if(img){
          image.onload =function (){
            deferred.resolve(getBase64Image(image));//将base64传给done上传处理
          }
          return deferred.promise();//问题要让onload完成后再return sessionStorage['imgTest']
        }
      }
startToBase64();
```
> 拓展一：后台需要以纯字符串的形式上传（即去掉data:image/png;base64，截取字符串即可）


```js

reader.result.substring(reader.result.indexOf(",") + 1)

```

### 1.3.7. XMLHttpRequest 对象用于在后台与服务器交换数据。
> [链接](https://www.w3school.com.cn/xml/xml_http.asp)
> XMLHTTPRequest的一些方法介绍[链接](https://blog.csdn.net/qq_40761839/article/details/82526465)

### 1.3.8. HTML5新特性：FileReader 和 FormData
[链接](https://blog.csdn.net/DavidFFFFFF/article/details/77836522)

### 1.3.9. JS中的Blob对象
[链接](https://www.jianshu.com/p/b322c2d5d778)
> 代表二进制类型的大对象




## 1.4. bootstrap
### 1.4.1. bootstrap-inputfile相关设置
[链接1](https://segmentfault.com/a/1190000018477200?utm_source=tag-newest)
[链接2](https://www.cnblogs.com/franknihao/p/8126837.html)


```js

					var optionsOfFileinput =JSON.parse('${files}');
					optionsOfFileinput.uploadUrl=ctx + '/tools/uploader/uploadFileOfCddBusiness';
					optionsOfFileinput.browseLabel="补充资料";
					optionsOfFileinput.layoutTemplates={
                        	actionDelete:'', //去除上传预览的缩略图中的删除图标
                        	actionUpload:'',//去除上传预览缩略图中的上传图片；
                        	};
					console.log(optionsOfFileinput);
					$("#input-dialog").fileinput(
							optionsOfFileinput
					
					).on('filebatchselected', function(event, files) {
						$(this).fileinput("upload");
					});
					$("#input-dialog").fileinput("disable");//禁用/启用文件上传 fileinput('disable/enable')　　禁用/启用文件上传

```
        



### 1.4.2. bootstrap日历时间控件datetimepicker
[基本使用教程](https://www.cnblogs.com/beimingbingpo/p/9913124.html)
#### 1.4.2.1. minview:'month'就不用再去选择时间了，只选择日期
```js

		<div class="col-sm-4">
				<label class="control-label col-sm-3" style="padding-top: 6px;">开始日期</label>
			<div class="form-group form-group-sm">
				<div class="col-sm-4" style="width:60%;">
					<div class="input-group input-group-sm date form_date form_datetime">
						<input class="form-control" type="text"
							id="dateByMonth" name="dateByMonth"
							value="" readonly /> <span class="input-group-addon"><span
							class="glyphicon glyphicon-remove"></span></span> <span
							class="input-group-addon"><span
							class="glyphicon glyphicon-calendar"></span></span>

					</div>
				</div>
			</div>
		</div>


 $(document).ready(function(){ 
	    $('.form_datetime').datetimepicker({//设置月
	        format: 'yyyy-mm',
	        autoclose: true,
	        todayBtn: true,
	        startView: 'year',
	        minView:'year',
	        maxView:'decade',
	        language:  'zh-CN',
	    });

}); 


datetimepicker选择日期后事件


window.οnlοad=function(){
        $('#daotime').datetimepicker({
                    language:  'zh-CN',
                    weekStart: 1,
                    todayBtn:  1,
                    autoclose: 1,
                    todayHighlight: 1,
                    startView: 2,
                    minView: 0,
                    forceParse: 0,
                    format:'yyyy-mm-dd hh:ii:ss',
        }).on('changeDate',function(ev){
            var  time=$("#daotime").val();
            var  recently=$("#recently").val();
            if(recently!=''&&time!=''){
                if(time.split(" ")[0]===recently.split(" ")[0]){
                    return confirm("该学生在所选择当天已登记诺访，是否继续操作？");
                }
            }
        }); 
    }
————————————————
版权声明：本文为CSDN博主「Forrest_Gumps」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/u011974321/article/details/52817270





-----------------下面为旧的----------------















楼主如果你要的是时间间隔的话    这是我写的，你可以参考下 ，另外你少了个参数 minview:'month'就不用再去选择时间了，只选择日期
   $('#txtDatastartTime').datepicker({
                minView: 'month',
                todayBtn: 1,
                format: 'yyyy-mm-dd',
                startView: 2,
                autoclose: true,
                todayHighlight: true,
                endDate: new Date(),
                showMeridian: 1,
                language: 'zh-CN'
            }).on('changeDate', function (e) {
                var startTime = e.date;
                $('#txtDataToTime').datepicker('setStartDate', startTime);
            });
            //结束时间：  
            $('#txtDataToTime').datepicker({
                minView: 'month',
                todayBtn: 1,
                format: 'yyyy-mm-dd',
                startView: 2,
                autoclose: true,
                todayHighlight: true,
                endDate: new Date(),
                showMeridian: 1,
                language: 'zh-CN'
            }).on('changeDate', function (e) {
                var endTime = e.date;
                $('#txtDatastartTime').datepicker('setEndDate', endTime);
            });
```


## 1.5. js常用框架库

### 1.5.1. FileSaver
[-链接](https://www.cnblogs.com/yunser/p/7629399.html)和jszip
### 1.5.2. Clipboard.js 实现点击复制
[链接](https://blog.csdn.net/fly_wugui/article/details/80327385)
### 1.5.3. 瀑布流Masonry
[链接](https://www.cnblogs.com/Renyi-Fan/p/9592585.html)
![](_v_images/20190829172750665_9493.png =288x)

### 1.5.4. zoom图片放大框架
#### 

> lightgallery
> ![](_v_images/20190829172255248_18038.png =288x)
> 



## 1.6. 自定义功能
### 1.6.1. 自定义校验功能

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script src="https://cdn.bootcss.com/jquery/3.4.1/jquery.js"></script>
	</head>

	<body>
		<ul>
			<li>姓名<input type="text" diy-dataTitle="姓名" class="diy-needVerify diy-required" diy-Title="姓名" diy-verifyType="isZnName"
				 name="" id="" value="" /></li>
			<li>身份证号码<input type="text" class="diy-needVerify diy-required"  diy-Title="身份证号码" diy-verifyType="isIdCard" name="" id="" value="" /></li>
			<li>手机号<input type="text"  class="diy-needVerify "  diy-Title="手机号" diy-verifyType="isPhone"  name="" id="" value="" /></li>
		</ul>
		<button onclick="startVerify()" type="button">校验</button>



	</body>
	<script>
		function startVerify(){
			
			var allNeedVerifyElements = $('.diy-needVerify');
			//console.log('allNeedVerifyElements:');
			//console.log(allNeedVerifyElements);
			console.log("------");
			
			var thisGroupVerifyResult={totalResult:true,errorTip:''};//通过
			
			for (var i = 0; i < allNeedVerifyElements.length; i++) {
				var thisElementOfJquery = $(allNeedVerifyElements[i]);
				var thisElementTitle = thisElementOfJquery.attr("diy-Title"); //标题
				var thisElementValue = thisElementOfJquery.val(); //输入值
				var whetherRequired = false; //false为不必填
				if (thisElementOfJquery.hasClass('diy-required')) { //如果有diy-required 则必填
					whetherRequired = true;
				}
				var verifyType = thisElementOfJquery.attr('diy-verifyType'); //校验类型
				
				var thisElementVerifyResult=verifyTypeFun(verifyType,thisElementTitle,thisElementValue,whetherRequired);
				console.log(thisElementVerifyResult);
				if(!thisElementVerifyResult.isPass){//有错误
					thisGroupVerifyResult.totalResult=false;
					thisGroupVerifyResult.errorTip+=thisElementVerifyResult.title+thisElementVerifyResult.erroeContent+"，"
				}
			}
			console.log('thisGroupVerifyResult:');
			console.log(thisGroupVerifyResult);
		}
		
		/**
		 * 身份证号码 isIdCard
		 * 手机号 isPhone
		 * 中文名 isZnName
		 * 两位小数点的金额 isMoney
		 * 
		 * 
		 * 
		 * 
		 */
		//传入检验类型和值，返回{title: "身份证号码", verifyValue: "340222199409270543", verifyType: "isIdCard", isPass: true, correctContent: "请输入"}
		/**
		 * @param {Object} verifyType 校验类型
		 * @param {Object} title 校验标题
		 * @param {Object} verifyValue 校验值
		 * @param {Object} whetherRequired 是否必填
		 */
		function verifyTypeFun(verifyType, title, verifyValue,whetherRequired) {
			//console.log(whetherRequired);
			var verifyResult = {
				title: title,
				verifyValue: verifyValue,
				verifyType: verifyType
			};
			var iphoneReg = /^[1][0,1,2,3,4,5,6,7,8,9][0-9]{9}$/; //手机号码验证规则
			var cnNameReg = /^[\u4E00-\u9FA5\uf900-\ufa2d]{2,4}$/; //验证姓名是否正确（2-4个中文字符）
			//正数且保留2位有效小数点的正则表达式
			var moneyReg = /^\d{1,9}(\.\d{1,2})?$/;
			
			if (whetherRequired) {//是,或者有参数 非undefined
				if (verifyValue==''){
					verifyResult.isPass = false;
					verifyResult.erroeContent = "必填项，格式错误";
					return verifyResult;
				}
			}
			
			
			
			if (verifyType == "isPhone") {
				if(!whetherRequired&&verifyValue==''){//可以不必填。空值通过
					verifyResult.isPass = true;
					verifyResult.correctContent = "请输入";
					return verifyResult;
				}
				
				
				
				
				if (iphoneReg.test(verifyValue)) { //通过
					verifyResult.isPass = true;
					verifyResult.correctContent = "请输入";
					return verifyResult;
				} else {
					verifyResult.isPass = false;
					verifyResult.erroeContent = "格式错误";
					//verifyResult.result={isPass: false,erroeContent:"必填项，格式错误"}
					return verifyResult;
				}
			} else if (verifyType == "isIdCard") {
				if(!whetherRequired&&verifyValue==''){
					verifyResult.isPass = true;
					verifyResult.correctContent = "请输入";
					return verifyResult;
				}
				
				
				
				
				if (IdentityCodeValid(verifyValue)) { //通过
					verifyResult.isPass = true;
					verifyResult.correctContent = "请输入";
					return verifyResult;
				} else {
					verifyResult.isPass = false;
					verifyResult.erroeContent = "格式错误";
					return verifyResult;
				}
			} else if (verifyType == "isZnName") { //中文名字
				if(!whetherRequired&&verifyValue==''){
					verifyResult.isPass = true;
					verifyResult.correctContent = "请输入";
					return verifyResult;
				}
			
			
			
			
				if (cnNameReg.test(verifyValue)) { //通过
					verifyResult.isPass = true;
					verifyResult.correctContent = "请输入";
					return verifyResult;
				} else {
					verifyResult.isPass = false;
					verifyResult.erroeContent = "格式错误";
					return verifyResult;
				}
			} else if (verifyType == "isMoney") {
				
				if(!whetherRequired&&verifyValue==''){
					verifyResult.isPass = true;
					verifyResult.correctContent = "请输入";
					return verifyResult;
				}
				
				
				
				
				if (moneyReg.test(verifyValue)) {
					verifyResult.isPass = true;
					verifyResult.correctContent = "请输入";
					return verifyResult;
				} else {
					verifyResult.isPass = false;
					verifyResult.erroeContent = "格式错误";
					return verifyResult;
				}


			} else if (verifyType == "isCommonCharacter") { //普通字符输入
			
				if(!whetherRequired&&verifyValue==''){
					verifyResult.isPass = true;
					verifyResult.correctContent = "请输入";
					return verifyResult;
				}
				
				
				
				
				if (verifyValue != "") {
					verifyResult.isPass = true;
					verifyResult.correctContent = "请输入";
					return verifyResult;
				} else {
					verifyResult.isPass = false;
					verifyResult.erroeContent = "为必填项，格式错误";
					return verifyResult;
				}

			} else {
				
				if(!whetherRequired&&verifyValue==''){
					verifyResult.isPass = true;
					verifyResult.correctContent = "请输入";
					return verifyResult;
				}
				
				
				
				
				
				verifyResult.isPass = false;
				verifyResult.erroeContent = "未知校验格式，格式错误";
				return verifyResult;
			}
		}
		
		
		
	//由XT在网上搜集而来，放入统一js中，为的是jsp的整洁

	//身份证校验 var true/false=IdentityCodeValid(身份证码);
	//iphoneReg = /^[1][3,4,5,7,8,9][0-9]{9}$/; //手机号码验证规则
	function IdentityCodeValid(code) {
		var city = {
			11: "北京",
			12: "天津",
			13: "河北",
			14: "山西",
			15: "内蒙古",
			21: "辽宁",
			22: "吉林",
			23: "黑龙江 ",
			31: "上海",
			32: "江苏",
			33: "浙江",
			34: "安徽",
			35: "福建",
			36: "江西",
			37: "山东",
			41: "河南",
			42: "湖北 ",
			43: "湖南",
			44: "广东",
			45: "广西",
			46: "海南",
			50: "重庆",
			51: "四川",
			52: "贵州",
			53: "云南",
			54: "西藏 ",
			61: "陕西",
			62: "甘肃",
			63: "青海",
			64: "宁夏",
			65: "新疆",
			71: "台湾",
			81: "香港",
			82: "澳门",
			91: "国外 "
		};
		var tip = "";
		var pass = true;
		if(!code || !/^\d{6}(18|19|20)?\d{2}(0[1-9]|1[012])(0[1-9]|[12]\d|3[01])\d{3}(\d|X)$/i.test(code)) {
			//tip = "身份证号格式错误";
			pass = false;
		} else if(!city[code.substr(0, 2)]) {
			//tip = "地址编码错误";
			pass = false;
		} else {
			//18位身份证需要验证最后一位校验位
			if(code.length == 18) {
				code = code.split('');
				//∑(ai×Wi)(mod 11)
				//加权因子
				var factor = [7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2];
				//校验位
				var parity = [1, 0, 'X', 9, 8, 7, 6, 5, 4, 3, 2];
				var sum = 0;
				var ai = 0;
				var wi = 0;
				for(var i = 0; i < 17; i++) {
					ai = code[i];
					wi = factor[i];
					sum += ai * wi;
				}
				var last = parity[sum % 11];
				if(parity[sum % 11] != code[17]) {
					//tip = "校验位错误";
					pass = false;
				}
			}
		}
		//if(!pass) alert(tip);
		return pass;
	};
	
	</script>
</html>


```