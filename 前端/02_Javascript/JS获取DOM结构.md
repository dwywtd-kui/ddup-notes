## 获取DOM 元素
### 通过类名获取DOM元素
(method) Document.getElementsByClassName(classNames: string): **HTMLCollectionOf<Element>**
### 通过ID获取DOM元素
(method) Document.getElementById(elementId: string): **HTMLElement**
### 通过标签名获取DOM元素
(method) Document.getElementsByTagName<"p">(qualifiedName: "p"): **HTMLCollectionOf<HTMLParagraphElement>**
### 通过name属性获取DOM元素

### querySelector

### querySelectorAll

### matches

### 代码演示
代码测试01
```javascript
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>JavaScipt-DOM之查找HTML</title>
</head>

<body>

    <p class="intro">111</p>
    <p id="p2">222</p>
    <p class="intro">333</p>
    <p>444</p>
    <script>

        // 通过类名找到 HTML 元素
        var introElements = document.getElementsByClassName("intro");
        for(var x of introElements){
            x.style.background='blue';
        }

        // 通过 id 查找 HTML 元素
        var p2 = document.getElementById('p2');
        if(p2!=undefined){
            p2.style.background = 'yellow';
        }

        // 通过标签名查找 HTML 元素
        var ps = document.getElementsByTagName('p');
        for(var x of ps){
            x.style.color='red';
        }

    </script>
</body>

</html>
```
效果：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/1039463/1659973680148-7bd2dd55-c1c7-4a6d-a0d1-f261f14bf36c.png#clientId=u010acc72-9f50-4&from=paste&height=146&id=u343ef36d&name=image.png&originHeight=182&originWidth=635&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2394&status=done&style=stroke&taskId=uaa76ae41-897a-42a1-915e-7dc3f62ce23&title=&width=508)

参考：

1. 深入理解javascript选择器API系列第一篇——4种元素选择器 [https://www.bbsmax.com/A/obzbyLjdED/](https://www.bbsmax.com/A/obzbyLjdED/)
2. 深入理解javascript选择器API系列第二篇——getElementsByClassName [https://www.bbsmax.com/A/kjdwxW6zNp/](https://www.bbsmax.com/A/kjdwxW6zNp/)
3. 深入理解javascript选择器API系列第三篇——HTML5新增的3种selector方法 [https://www.bbsmax.com/A/RnJWOa9YJq/](https://www.bbsmax.com/A/RnJWOa9YJq/)
4. JS之DOM篇-选择器  [https://www.cnblogs.com/yesyes/p/15352397.html](https://www.cnblogs.com/yesyes/p/15352397.html)
5. 菜鸟教程-JS查找HTML [https://www.runoob.com/js/js-htmldom.html](https://www.runoob.com/js/js-htmldom.html)


