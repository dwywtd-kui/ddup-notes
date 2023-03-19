## 概述
### 什么是AJAX?
AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。	是一种用于创建快速动态网页的技术。
AJAX 最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容。传统的网页（不使用 AJAX）如果需要更新内容，必需重载整个网页面。
### AJAX工作原理
![image.png](https://cdn.nlark.com/yuque/0/2022/png/1039463/1660445666880-9dd1cffd-84fa-46bf-bf5e-e7f4b987ca7d.png#averageHue=%23f4f4f4&clientId=u84eeed3e-8fd6-4&errorMessage=unknown%20error&from=paste&id=u0c0800e2&name=image.png&originHeight=304&originWidth=576&originalType=url&ratio=1&rotation=0&showTitle=false&size=19068&status=error&style=none&taskId=u62581cb5-af8f-4608-8d86-587de5242ee&title=)

## XHR 对象
所有现代浏览器均支持 XMLHttpRequest 对象（IE5 和 IE6 使用 ActiveXObject）。XMLHttpRequest 用于在后台与服务器交换数据。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。
所有现代浏览器（IE7+、Firefox、Chrome、Safari 以及 Opera）均内建 XMLHttpRequest 对象。创建 XMLHttpRequest 对象的语法：
`variable=new XMLHttpRequest();`
老版本的 Internet Explorer （IE5 和 IE6）使用 ActiveXObject 对象：
`variable=new ActiveXObject("Microsoft.XMLHTTP");`
为了应对所有的现代浏览器，包括 IE5 和 IE6，请检查浏览器是否支持 XMLHttpRequest 对象。如果支持，则创建 XMLHttpRequest 对象。如果不支持，则创建 ActiveXObject ：
```javascript
var xmlhttp;
if (window.XMLHttpRequest)
{
    //  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
    xmlhttp=new XMLHttpRequest();
}
else
{
    // IE6, IE5 浏览器执行代码
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
}
```
## XHR 请求
XMLHttpRequest 对象用于和服务器交换数据。使用 XMLHttpRequest 对象的 open() 和 send() 方法将请求发送到服务器：

| 方法 | 描述 |
| --- | --- |
| open(_method_,_url_,_async_) | 规定请求的类型、URL 以及是否异步处理请求。
- _method_：请求的类型；GET 或 POST
- _url_：文件在服务器上的位置
- _async_：true（异步）或 false（同步）
 |
| send(_string_) | 将请求发送到服务器。
- _string_：仅用于 POST 请求
 |

### GET请求
```javascript
xmlhttp.open("GET","/try/ajax/demo_get.php",true);
xmlhttp.send();
```
在上面的例子中，您可能得到的是缓存的结果。为了避免这种情况，请向 URL 添加一个唯一的 ID：
```javascript
xmlhttp.open("GET","/try/ajax/demo_get.php?t=" + Math.random(),true);
xmlhttp.send();
```

### POST 请求
```javascript
xmlhttp.open("POST","/try/ajax/demo_post.php",true);
xmlhttp.send();
```

### 添加HTTP Header
如果需要像 HTML 表单那样 POST 数据，请使用 setRequestHeader() 来添加 HTTP 头。然后在 send() 方法中规定您希望发送的数据：
```javascript
xmlhttp.open("POST","/try/ajax/demo_post2.php",true);
// 设置header信息
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("fname=Henry&lname=Ford");
```

`setRequestHeader(header,value)` 向请求添加 HTTP 头。`header`: 规定头的名称。`value`: 规定头的值。
### 是否异步
AJAX 指的是异步 JavaScript 和 XML（Asynchronous JavaScript and XML）。XMLHttpRequest 对象如果要用于 AJAX 的话，其 open() 方法的 async 参数必须设置为 true：
对于 web 开发人员来说，发送异步请求是一个巨大的进步。很多在服务器执行的任务都相当费时。AJAX 出现之前，这可能会引起应用程序挂起或停止。通过 AJAX，JavaScript 无需等待服务器的响应，而是：

- 在等待服务器响应时执行其他脚本
- 当响应就绪后对响应进行处理

当使用 async=true 时，请规定在响应处于 onreadystatechange 事件中的就绪状态时执行的函数：
```javascript
// 响应就绪后，会执行此函数
xmlhttp.onreadystatechange=function()
{
	if (xmlhttp.readyState==4 && xmlhttp.status==200)
	{
		document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
	}
}
xmlhttp.open("GET","/try/ajax/ajax_info.txt",true);
xmlhttp.send();
```

## XHR 服务端响应
获得来自服务器的响应，请使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性。

- responseText  获得字符串形式的响应数据。
- responseXML  获得 XML 形式的响应数据。

responseText 属性返回字符串形式的响应，因此可以这样使用：
```javascript
document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
```

如果来自服务器的响应是 XML，而且需要作为 XML 对象进行解析，请使用 responseXML 属性：
```javascript
xmlDoc=xmlhttp.responseXML;
txt="";
x=xmlDoc.getElementsByTagName("ARTIST");
for (i=0;i<x.length;i++)
{
    txt=txt + x[i].childNodes[0].nodeValue + "<br>";
}
document.getElementById("myDiv").innerHTML=txt;
```
示例xml文件：[https://www.runoob.com/try/demo_source/cd_catalog.xml](https://www.runoob.com/try/demo_source/cd_catalog.xml)
## XHR read state
当请求被发送到服务器时，我们需要执行一些基于响应的任务。每当 readyState 改变时，就会触发 onreadystatechange 事件。
readyState 属性存有 XMLHttpRequest 的状态信息。下面是 XMLHttpRequest 对象的三个重要的属性：
下面是 XMLHttpRequest 对象的三个重要的属性：

| 属性 | 描述 |
| --- | --- |
| onreadystatechange | 存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。 |
| readyState | 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。
- 0: 请求未初始化
- 1: 服务器连接已建立
- 2: 请求已接收
- 3: 请求处理中
- 4: 请求已完成，且响应已就绪
 |
| status | 200: "OK"
404: 未找到页面 |

在 onreadystatechange 事件中，我们规定当服务器响应已做好被处理的准备时所执行的任务。当 readyState 等于 4 且状态为 200 时，表示响应已就绪：
```javascript
xmlhttp.onreadystatechange=function()
{
    if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
}
```

注意： onreadystatechange 事件被触发 4 次（0 - 4）, 分别是： 0-1、1-2、2-3、3-4，对应着 readyState 的每个变化。
```javascript
function loadXMLDoc()
{
	var xmlhttp;
	if (window.XMLHttpRequest)
	{
		//  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
		xmlhttp=new XMLHttpRequest();
	}
	else
	{
		// IE6, IE5 浏览器执行代码
		xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
	}
	xmlhttp.onreadystatechange=function()
	{
    // 会弹出4次提示
		alert('xmlhttp.readyState:'+xmlhttp.readyState);
		if (xmlhttp.readyState==4 && xmlhttp.status==200)
		{
			document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
		}
	}
	xmlhttp.open("GET","/try/ajax/ajax_info.txt",true);
	xmlhttp.send();
}
```
![GIF 2022-8-14 11-36-07.gif](https://cdn.nlark.com/yuque/0/2022/gif/1039463/1660448236658-f35bacbf-10f2-47d8-adec-c9fcfe8100c9.gif#averageHue=%23f9f7f5&clientId=u84eeed3e-8fd6-4&errorMessage=unknown%20error&from=paste&height=702&id=u13e605bf&name=GIF%202022-8-14%2011-36-07.gif&originHeight=878&originWidth=1286&originalType=binary&ratio=1&rotation=0&showTitle=false&size=307518&status=error&style=none&taskId=u6dce4759-b795-4308-afd7-56786ed18d1&title=&width=1028.8)

## JQuery AJAX
jQuery 提供多个与 AJAX 有关的方法。通过 jQuery AJAX 方法，您能够使用 HTTP Get 和 HTTP Post 从远程服务器上请求文本、HTML、XML 或 JSON - 同时您能够把这些外部数据直接载入网页的被选元素中。
### jQuery load() 方法
jQuery load() 方法是简单但强大的 AJAX 方法。load() 方法从服务器加载数据，并把返回的数据放入被选元素中。语法:
```javascript
$(selector).load(URL,data,callback);
```

- 必需的 URL 参数规定您希望加载的 URL。
- 可选的 data 参数规定与请求一同发送的查询字符串键/值对集合。
- 可选的 callback 参数是 load() 方法完成后所执行的函数名称。

**这是示例文件（"demo_test.txt"）的内容：**
> <h2>jQuery AJAX 是个非常棒的功能！</h2>
> <pid="p1">这是段落的一些文本。</p>

下面的例子会把文件 "demo_test.txt" 的内容加载到指定的 <div> 元素中：
```javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>测试jQuery ajax load</title>
<script src="https://cdn.staticfile.org/jquery/1.10.2/jquery.min.js">
</script>
<script>
$(document).ready(function(){
	$("button").click(function(){
		$("#div1").load("/try/ajax/demo_test.txt");
	});
});
</script>
</head>
<body>

<div id="div1"><h2>使用 jQuery AJAX 修改文本内容</h2></div>
<button>获取外部内容</button>

</body>
</html>
```
	
![GIF 2022-8-14 12-16-33.gif](https://cdn.nlark.com/yuque/0/2022/gif/1039463/1660450608928-b581fda0-977e-414d-ad25-ab613a026733.gif#averageHue=%23fafafa&clientId=u84eeed3e-8fd6-4&errorMessage=unknown%20error&from=paste&height=385&id=u3d86b2b3&name=GIF%202022-8-14%2012-16-33.gif&originHeight=481&originWidth=733&originalType=binary&ratio=1&rotation=0&showTitle=false&size=31420&status=error&style=none&taskId=u7436dfd5-92a6-48dc-8c96-1238162d10f&title=&width=586.4)
也可以把 jQuery 选择器添加到 URL 参数。
下面的例子把 "demo_test.txt" 文件中 id="p1" 的元素的内容，加载到指定的 <div> 元素中：
```javascript
$("#div1").load("demo_test.txt #p1");
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/1039463/1660450778892-6f784441-1c14-480b-aa1e-e34ea96c20ff.png#averageHue=%23faf9f9&clientId=u84eeed3e-8fd6-4&errorMessage=unknown%20error&from=paste&height=113&id=u10fb8f7b&name=image.png&originHeight=141&originWidth=444&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4751&status=error&style=none&taskId=u2a366783-ea43-4042-934c-67615990676&title=&width=355.2)
可选的 callback 参数规定当 load() 方法完成后所要允许的回调函数。回调函数可以设置不同的参数：

- responseTxt - 包含调用成功时的结果内容
- statusTXT - 包含调用的状态
- xhr - 包含 XMLHttpRequest 对象

下面的例子会在` load()` 方法完成后显示一个提示框。如果 load() 方法已成功，则显示"外部内容加载成功！"，而如果失败，则显示错误消息：
```javascript
$("button").click(function(){
  $("#div1").load("demo_test.txt",function(responseTxt,statusTxt,xhr){
    if(statusTxt=="success")
      alert("外部内容加载成功!");
    if(statusTxt=="error")
      alert("Error: "+xhr.status+": "+xhr.statusText);
  });
});
```
### jQuery get() 和 post() 方法
jQuery `get() `和 `post() `方法用于通过 HTTP GET 或 POST 请求从服务器请求数据。
#### jQuery $.get() 方法
`$.get() `方法通过 HTTP GET 请求从服务器上请求数据。
语法：
`$.get(URL,callback);`
或
`$.get( URL [, data ] [, callback ] [, dataType ] )`

- URL：发送请求的 URL字符串。
- data：可选的，发送给服务器的字符串或 key/value 键值对。
- callback：可选的，请求成功后执行的回调函数。
- dataType：可选的，从服务器返回的数据类型。默认：智能猜测（可以是xml, json, script, 或 html）。

下面的例子使用 `$.get() `方法从服务器上的一个文件中取回数据：
```javascript
$("button").click(function(){
  $.get("demo_test.php",function(data,status){
    alert("数据: " + data + "\n状态: " + status);
  });
});
```
`$.get() `的第一个参数是我们希望请求的 URL（"demo_test.php"）。
第二个参数是回调函数。第一个_回调参数存有被请求页面的内容，第二个回调参数存有请求的状态。_
### jQuery $.post() 方法
`$.post()` 方法通过 HTTP POST 请求向服务器提交数据。
语法:
`$.post(URL,callback);`
或
`$.post( URL [, data ] [, callback ] [, dataType ] )`

- URL：发送请求的 URL字符串。
- data：可选的，发送给服务器的字符串或 key/value 键值对。
- callback：可选的，请求成功后执行的回调函数。
- dataType：可选的，从服务器返回的数据类型。默认：智能猜测（可以是xml, json, script, 或 html）。

下面的例子使用 `$.post()` 连同请求一起发送数据：
```javascript
$("button").click(function(){
    $.post("/try/ajax/demo_test_post.php",
    {
        name:"菜鸟教程",
        url:"http://www.runoob.com"
    },
    function(data,status){
        alert("数据: \n" + data + "\n状态: " + status);
    });
});
```
`$.post() `的第一个参数是我们希望请求的 URL ("demo_test_post.php")。第二个参数是我们连同请求（name 和 url）一起发送数据。第三个参数是回调函数，_第一个回调参数存有被请求页面的内容，而第二个参数存有请求的状态。_
## 参考

- AJAX：[https://www.runoob.com/ajax/ajax-tutorial.html](https://www.runoob.com/ajax/ajax-tutorial.html)
- jQuery AJAX： [https://www.runoob.com/jquery/jquery-ajax-intro.html](https://www.runoob.com/jquery/jquery-ajax-intro.html)

