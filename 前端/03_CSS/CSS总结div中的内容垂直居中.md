## 行高（line-height）法
如果要垂直居中的只有一行或几个文字，那它的制作最为简单，只要让文字的行高和容器的高度相同即可，比如：
```css
p { 
  height:30px; 
  line-height:30px;  // 设置行高
}
```
这段代码可以达到让文字在段落中垂直居中的效果。

## 内边距（padding）法
另一种方法和行高法很相似，它同样适合一行或几行文字垂直居中，原理就是利用padding将内容垂直居中，比如：
```css
p { 
  padding:20px 0; 
}
```
## 模拟表格法
将容器设置为display:table，然后将子元素也就是要垂直居中显示的元素设置为display:table-cell，然后加上vertical-align:middle来实现。遗憾的是IE7及以下不支持
html结构如下：
```html
<div id="wrapper">
    <div id="cell">
        <p>测试垂直居中效果测试垂直居中效果</p>
        <p>测试垂直居中效果测试垂直居中效果</p>
    </div>
</div>
```
css代码：
```css
#wrapper {
  display:table;
  width:300px;
  height:300px;
  background:#000;
  margin:0 auto;
  color:red;
}
#cell{
  display:table-cell; 
  vertical-align:middle;
}
```
实现效果：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/1039463/1641114375659-2092b3a3-66a4-44b6-99e8-1a1e6c310155.png#clientId=u53592e1f-7d38-4&from=paste&id=u22c10a03&name=image.png&originHeight=300&originWidth=298&originalType=url&ratio=1&size=4504&status=done&style=none&taskId=ufc9c8f32-66d0-4716-b0ed-2750bed8993)

## CSS3的transform来实现
```css
.center-vertical{
  position: relative;
  top:50%;
  transform:translateY(-50%);
}

.center-horizontal{
  position: relative;
  left:50%;
  transform:translateX(-50%); 
}
```
## CSS3的box方法实现水平垂直居中
```html
<div class="center">
  <div class="text">
    <p>我是多行文字</p>
    <p>我是多行文字</p>
    <p>我是多行文字</p>
  </div>
</div>
```
```css
.center {
  width: 300px;
  height: 200px;
  padding: 10px;
  border: 1px solid #ccc;
  background:#000;
  color:#fff;
  margin: 20px auto;


  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-pack: center;
  -webkit-box-align: center;
  
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-pack: center;
  -moz-box-align: center;
  
  display: -o-box;
  -o-box-orient: horizontal;
  -o-box-pack: center;
  -o-box-align: center;
  
  display: -ms-box;
  -ms-box-orient: horizontal;
  -ms-box-pack: center;
  -ms-box-align: center;
  
  display: box;
  box-orient: horizontal;
  box-pack: center;
  box-align: center;
}
```
结果：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/1039463/1641114548220-a9059fe2-9ad2-411b-8274-3a5b19a6c84a.png#clientId=u53592e1f-7d38-4&from=paste&id=ua9d094f1&name=image.png&originHeight=224&originWidth=324&originalType=url&ratio=1&size=3769&status=done&style=none&taskId=uf07cd78f-9869-4f80-8bb6-367b2349e0b)

## flex布局
```html
<div class="flex">
    <div>
       <p>我是多行文字我是多行文字我是多行文字我是多行文字</p>
      <p>我是多行文字我是多行文字我是多行文字我是多行文字</p>
    </div>
</div>
```
```css
.flex{
    /*flex 布局*/
    display: flex;
    /*实现垂直居中*/
    align-items: center;
    /*实现水平居中*/
    justify-content: center;
    
    text-align: justify;
    width:200px;
    height:200px;
    background: #000;
    margin:0 auto;
    color:#fff;
}
```
实现效果：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/1039463/1641114588210-00111a96-0275-4645-bde6-182557f14b09.png#clientId=u53592e1f-7d38-4&from=paste&id=u8bb27bc9&name=image.png&originHeight=213&originWidth=227&originalType=url&ratio=1&size=6003&status=done&style=none&taskId=ub8a7785a-c189-4580-82d8-07b9e2a0be8)

参考：[https://www.cnblogs.com/moqiutao/p/4807792.html](https://www.cnblogs.com/moqiutao/p/4807792.html)
