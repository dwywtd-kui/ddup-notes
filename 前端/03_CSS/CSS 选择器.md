## 后代选择器
**后代选择器可以选择作为某元素后代的元素。**
举例来说，如果您希望只对 p 元素中的 span 元素应用样式，可以这样写：
```css
p span {
  color:red;
}
```
示例：
```html
<!DOCTYPE HTML>
<html>

<head>
    <style type="text/css">
        div p {
            color: red;
            margin-left: 50px;
            font-weight: bolder;
        }
    </style>
</head>

<body>
    <div>0</div>
    <div>
        <p>11</p>
        <span>
            <p>121</p>
            <p>122</p>
        </span>
        <span>13</span>
        <div>14</div>
        <p>15</p>
    </div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
  
</body>

</html>
```
效果：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1039463/1632537035184-37640ba2-75b9-4688-a97a-ddd6315a8d3e.png#clientId=u2100d14b-e9ad-4&from=paste&height=199&id=u7114f4d8&name=image.png&originHeight=397&originWidth=413&originalType=binary&ratio=1&size=7043&status=done&style=stroke&taskId=u45b6d536-6b94-4278-90f5-b8239dfa511&width=206.5)
## 子代选择器
如果您不希望选择任意的后代元素，而是希望缩小范围，只选择某个元素的子元素，请使用子元素选择器（Child selector）。
与后代选择器相比，子元素选择器（Child selectors）只能选择作为某元素子元素的元素。
```css
<!DOCTYPE HTML>
<html>

<head>
    <style type="text/css">
        div > p {
            color: red;
            margin-left: 50px;
            font-weight: bolder;
        }
    </style>
</head>

<body>
    <div>0</div>
    <div>
        <p>11</p>
        <span>
            <p>121</p>
            <p>122</p>
        </span>
        <span>13</span>
        <div>14</div>
        <p>15</p>
    </div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
  
</body>

</html>
```
效果：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1039463/1632537300635-e15ccbb4-08da-4f41-b65c-7a2c43c701e9.png#clientId=u2100d14b-e9ad-4&from=paste&height=191&id=ufbe58d33&name=image.png&originHeight=381&originWidth=404&originalType=binary&ratio=1&size=6377&status=done&style=stroke&taskId=ud7b3ef78-eeec-454e-9bf2-fd795f2754a&width=202)
## 相邻兄弟选择器
如果需要选择紧接在另一个元素后的元素，而且二者有相同的父元素，可以使用相邻兄弟选择器（Adjacent sibling selector）。
例如，如果要增加紧接在 h1 元素后出现的段落的上边距，可以这样写：
```css
h1 + p {margin-top:50px;}
```
这个选择器读作：“选择紧接在 h1 元素后出现的段落，h1 和 p 元素拥有共同的父元素”。
```html
<!DOCTYPE HTML>
<html>

<head>
    <style type="text/css">
        h1+p {
            color: red
        }
    </style>
</head>

<body>
    <h1>This is a heading.</h1>
    <p>This is paragraph.</p>
    <p>This is paragraph.</p>
    <p>This is paragraph.</p>
    <p>This is paragraph.</p>
    <p>This is paragraph.</p>
</body>

</html>
```
效果：
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1039463/1632536193422-944dd1e7-c3d4-4ea6-86ea-61f64d9131ed.png#clientId=u2100d14b-e9ad-4&from=paste&height=156&id=ua7858278&name=image.png&originHeight=312&originWidth=718&originalType=binary&ratio=1&size=16480&status=done&style=stroke&taskId=u9d83653a-4b4c-48a5-82d3-b22f51a5d51&width=359)
## 后续兄弟选择器
选取所有指定元素之后的相邻兄弟元素。与相邻兄弟元素选择器 相比：

- 相邻兄弟元素选择器 只是选择紧跟着的兄弟元素，
- 后续元素选择器  选择所有符合条件的兄弟元素

实例：（选取h1元素后的所有，相邻的兄弟元素p元素）
```html
<!DOCTYPE HTML>
<html>

<head>
    <style type="text/css">
        h1~p {
            color: red;
            background-color: aqua;
        }
    </style>
</head>

<body>
    <h1>This is a heading.</h1>
    <p>This is paragraph.</p>
    <p>This is paragraph.</p>
    <p>This is paragraph.</p>
    <p>This is paragraph.</p>
    <p>This is paragraph.</p>
</body>

</html>
```
![image.png](https://cdn.nlark.com/yuque/0/2021/png/1039463/1632536346956-ddafeeab-8f9c-4c6c-b6c9-3c0641448d85.png#clientId=u2100d14b-e9ad-4&from=paste&height=170&id=u727ba961&name=image.png&originHeight=339&originWidth=723&originalType=binary&ratio=1&size=17409&status=done&style=stroke&taskId=uac92fb74-9825-46ee-a307-14fd2a9d682&width=361.5)
