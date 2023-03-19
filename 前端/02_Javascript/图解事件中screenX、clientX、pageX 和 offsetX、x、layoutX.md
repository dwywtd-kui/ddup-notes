## screenX、clientX、pageX 和 offsetX
### screenX 和screenY
参照点：电脑屏幕左上角
screenX：鼠标点击位置相对于电脑屏幕左上角的水平偏移量
screenY：鼠标点击位置相对于电脑屏幕左上角的垂直偏移量

### clientX和clientY
参照点：浏览器内容区域左上角
clientX：鼠标点击位置相对于浏览器可视区域的水平偏移量（不会计算水平滚动的距离）
clientY：鼠标点击位置相对于浏览器可视区域的垂直偏移量（不会计算垂直滚动条的距离）

### pageX和pageY
参照点：网页的左上角
pageX：鼠标点击位置相对于网页左上角的水平偏移量，也就是clientX加上水平滚动条的距离
pageY：鼠标点击位置相对于网页左上角的垂直平偏移量，也就是clientY加上垂直滚动条的距离

### offsetX和offsetY
offsetX：鼠标点击位置相对于触发事件对象的水平距离
offsetY：鼠标点击位置相对于触发事件对象的垂直距离

![](https://img2022.cnblogs.com/blog/1703406/202210/1703406-20221030143056014-930212584.png#id=sitdz&originHeight=768&originWidth=1366&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

## event.x
event.x 代表点击的点距离可视区左边框的距离，而它在不同浏览器处理结果是不一样的，首先看以下代码
```html
<body>
    <div>
        外
        <div  id="content" style="margin-top:50px;padding:15px;height:20px">
            内
        </div>
    </div>
</body>
```

这种情况，event.x在谷歌和IE结果是一样的，但是如果在外层div加上定位:
```html
<body>
    <div style="position:relative">
        外
        <div  id="content" style="margin-top:50px;padding:15px;height:20px">
            内
        </div>
    </div>
</body>
```

这时候，谷歌还是不变的，但是IE就不同了，它的event.x返回的是点击位置到外层div的距离，如下图所示：
![](https://img2022.cnblogs.com/blog/1703406/202210/1703406-20221030143511157-967442716.png#id=KfCRt&originHeight=768&originWidth=1366&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

考虑到兼容性，event.x不建议使用，event.x可以用event.clientX 代替

## event.layerX

layerX/Y获取到的是触专发点相对被触发dom左上角的距离，数值与offsetX/Y相同，这个变量就是firefox用来替代offsetX/Y的，基准点为边框左上角，但是有个条件就是，被触发的dom需要设置为position:relative或者position:absolute，否则会返回相对html文档区域左上角的距离:
![](https://img2022.cnblogs.com/blog/1703406/202210/1703406-20221030143638613-1618957290.png#id=Tv2TS&originHeight=768&originWidth=1366&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
**考虑到兼容性，layerX不建议使用，layerX可以用offsetX代替**

参考：
1、[https://blog.csdn.net/qq_38128179/article/details/84647298](https://blog.csdn.net/qq_38128179/article/details/84647298)
2、[https://blog.csdn.net/qq_39816673/article/details/106018053](https://blog.csdn.net/qq_39816673/article/details/106018053)

