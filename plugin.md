## 开发后台用到的插件方法

@(文档笔记)[文档帮助, 文档api, 帮助, 接口文档]

***********************************************
[TOC]

### MSConfig.Toastr 方法
`方法介绍`

***用作内容的提示，可自定义显示时间和位置***     [详细的封装代码][code-1]
  
```javascript
    Config.Toastr = function(state, content, time, pos) {
       
    };
```
-  **参数说明**

>|参数|  参数类型| 参数说明 |缺省值|
  |:----------|:--------------:|----------:|:----------|
  |state| `string`|代表当前提示框的状态 分别是成功、失败、警告、提示(success/error/warning/info)|`必填`|
  |content|`string`|定义提示的内容支持html|`必填`|
  |time|`string`|定义提示框显示的时间 单位毫秒<font color='#e4393c'>注：如果这个值为0 则弹框不消失</font>|`5000`|
 | pos|`string`|定义提示框出现的位置 支持左上、左下、右上、右下、全屏上、全屏下(toast-top-left/toast-bottom-left/toast-top-right/toast-bottom-right/toast-top-full-width/toast-bottom-full-width/)|`toast-top-right`|



- **示例代码**  

```javascript
MSConfig.Toastr("success","这是一个简单了效果");
```

-  **效果展示**
![实例][Toastr-1]
- **如果你想让他常驻,请这样传递参数**
```javascript
MSConfig.Toastr("success",'0',"这是一个顶部常驻效果",'toast-top-full-width');
```
-  **效果展示**
![实例][Toastr-2]

*******************************************************************************************************************

###MSConfig.SwalConfirm  方法
`方法介绍`

***用作弹框的确认*** [详细的封装代码][code-2]
```javascript
    Config.SwalConfirm = function(state, title, content, fn1) {
        
    };
```
-  **参数说明**

>|参数|  参数类型| 参数说明 |缺省值|
  |:---------------|:------------:|---------------------------------------------------:|:--------------------------|
  |state             | `string`|代表当前弹框的状态 分别是成功、失败、警告、提示(success/error/warning/info)                                                                    |`友情提示`                  |
  |title              |`string`|定义提示框的title                                           |`必填`                        |
  |content         |`string`|定义提示框内容                                             |null                            |
  | fn1               |`obj`      |点击确定(ok)以后的回调函数                        |null                            |



- **示例代码**  

```javascript
MSConfig.SwalConfirm("success","成功",'删除成功');
```

-  **效果展示**
![实例][Swal-1]
- **如果你有后续的操作可以定义一个回调函数**
```javascript
function suc(){
	console.log("哈哈终于删除了你")
}
MSConfig.SwalConfirm("success","成功",'删除成功',suc);
```
-  **效果展示**
![实例][Swal-2]
**************************************************************************************************************

###MSConfig.SwalAlert  方法
`方法介绍`

***用作自动消失弹框***  [详细的封装代码][code-3]
```javascript
    Config.SwalAlert = function(state, title, content, time) {
       
    };
```
-  **参数说明**

>|参数|  参数类型| 参数说明 |缺省值|
  |:---------------|:------------:|---------------------------------------------------:|:--------------------------|
  |state             | `string`|代表当前弹框的状态 分别是成功、失败、警告、提示(success/error/warning/info)                                                                     |`success`                |   
  |title              |`string`|定义提示框的title                                           |`必填`                        |
  |content         |`string`|定义提示框内容                                             |`必填`                        |
  | time             |`number`|代表消失的时间，单位毫秒                         |`2000`                         |



- **示例代码**  

```javascript
MSConfig.SwalAlert("info","成功",'2s后我会自动消失');
```

-  **效果展示**
![实例][Swal-3]

*******************************************************************************************************

###MSConfig.Gdt  方法
`方法介绍`

***用作初始化滚动条*** [详细的封装代码][code-4]
```javascript
   Config.Gdt = function(dom, time) {
        
    };
```
-  **参数说明**

>|参数|  参数类型| 参数说明 |缺省值|
  |:---------------|:------------:|---------------------------------------------------:|:--------------------------|
   |dom            |`string`|代表当前要初始化滚动条的dom元素("#id"or".class")   |`必填`           |                                          
  | time            |`number`|代表延迟初始化的时间，视情况而定 单位毫秒                          |`100`                          |



- **示例代码**  

```javascript
MSConfig.Gdt('#defined-sel');
```

-  **效果展示**
![实例][gdt]

************************************************************************************************************
###MSConfig.Open 方法
`方法介绍`

***用作初始化layer 弹框(主要用于模板页面)` 注意:添加和编辑状态下有遮罩层`***  [详细的封装代码][code-6]
```javascript
   Config.Open = function(skin, html, width, height, defineTitle, pop) {
       
    };
```
-  **参数说明**

>|参数|  参数类型| 参数说明 |缺省值|
  |:---------------|:------------:|---------------------------------------------------:|:--------------------------|
   |skin            |`string`|用于确定弹框的类型(增加(add)、编辑(edit)、查看(look)、自定义(others))   |`必填`           |                                          
   | html            |`string`|用于确定弹框的地址                          |`必填`                         |
   |width            |`number`|用于确定弹框的宽度(实际应用中视情况而定)   |`800`       |                                              
   | height          |`number`|用于确定弹框的高度 (实际应用中视情况而定)                         |`$(window).height() - 300)`         |
   |defineTitle           |`string`|用于个性化的传入自定义的title(例如:'张三的寻滩轨迹'而不传'寻滩轨迹')   |null     |                                          
  |pop           |`string`|用于弹框是否全屏化                          |null                      |



- **示例代码**  

```javascript
 MSConfig.Open("edit","component/tpl/more.html")
```

-  **效果展示**
![实例][open-1]

- **如果你要区分title 传递如下参数**  

```javascript
MSConfig.Open("others","component/tpl/single.html","","","你好世界")
```

-  **效果展示**
![实例][open-2]

**************************************************************************************************************
###MSConfig.FormAjax  方法
`方法介绍`

***用作表单的提交和验证*** [详细的封装代码][code-5]
```javascript
   Config.FormAjax = function(formDom, closeInfo) {
       

    };
```
-  **参数说明**

>|参数|  参数类型| 参数说明 |缺省值|
  |:---------------|:------------:|---------------------------------------------------:|:--------------------------|
   |formDom|`string`|传入表单form的唯一标识(最好为id("#id")   |`必填`           |                                          
  | closeInfo            |`string`|根据不同的业务场景确定是否要手动触发关闭                         |null                          |



- **示例代码**  

```javascript
MSConfig.FormAjax("#testForm");
```

-  **效果展示**
![实例][formAjax]
**************************************************************************************************************
###MSConfig.ResizeIframeHeight  方法
`方法介绍`

***用作调整iframe的高度*** [详细的封装代码][code-7]
```javascript
   Config.ResizeIframeHeight=function(){
       
    };
```
-  **参数说明**

>|参数|  参数类型| 参数说明 |缺省值|
  |:---------------|:------------:|---------------------------------------------------:|:--------------------------|
   |null|`null`|null   |null          |                                          
  | null         |`null`|null                       |null                        |



- **示例代码**  

```javascript
 MSConfig.ResizeIframeHeight();
```
******************************************************************************************************

###MSConfig.Ajax  方法
`方法介绍`

***工具类ajax 的分装 支持链式调用*** [详细的封装代码][code-8]
```javascript
   Config.Ajax = function(reqUrl, reqData, reqType, resType, contentType, reqTime) {
       
    };
```
-  **参数说明**

>|参数|  参数类型| 参数说明 |缺省值|
  |:---------------|:------------:|---------------------------------------------------:|:--------------------------|
   |reqUrl|`string`|请求的url地址   |`必填`       |                                     
  | reqData|`obj`|请求传递的参数对象                       |null                        |
   |reqType|`string`|请求类型    |`GET`       |                                          
  | resType|`string`|返回的数据格式                      |`json`                       |
	   |contentType|`string`|请求头文件格式   |  `application/x-www-form-urlencoded`   |                             
  | reqTime|`number`|超时时间 单位(毫秒)                     |`3000   `                  |


- **示例代码**  

```javascript
   var url = "test/json/1.json";
    MSConfig.Ajax(url, {}, "POST")
```

























<!-->
引用的内容地址
[Toastr-1]:http://p20ez4smj.bkt.clouddn.com/toastr-1.png
[Toastr-2]:http://ww1.sinaimg.cn/large/006uNFWmgy1fo4pa1e2q1j31d60otn92.jpg
[Swal-1]:http://p20ez4smj.bkt.clouddn.com/swal-1.png
[Swal-2]:http://ww1.sinaimg.cn/large/006uNFWmgy1fo4qc6nahaj31d60meq8l.jpg
[Swal-3]:http://p20ez4smj.bkt.clouddn.com/swal-3.png
[gdt]:http://p20ez4smj.bkt.clouddn.com/gdt.png
[open-1]:http://p20ez4smj.bkt.clouddn.com/open-1.png
[open-2]:http://p20ez4smj.bkt.clouddn.com/open-2.png
[formAjax]:http://p20ez4smj.bkt.clouddn.com/form.png
[code-1]:http://p20ez4smj.bkt.clouddn.com/code-1.png
[code-2]:http://p20ez4smj.bkt.clouddn.com/code-2.png
[code-3]:http://p20ez4smj.bkt.clouddn.com/code-3.png
[code-4]:http://p20ez4smj.bkt.clouddn.com/code-4.png
[code-5]:http://p20ez4smj.bkt.clouddn.com/code-5.png
[code-6]:http://p20ez4smj.bkt.clouddn.com/code-6.png
[code-7]:http://p20ez4smj.bkt.clouddn.com/code-7.png
[code-8]:http://p20ez4smj.bkt.clouddn.com/code-8.png
<-->
