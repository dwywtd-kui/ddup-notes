## 不想生成.map 文件
如果不想生成.map 文件，执行  ng build --sourceMap=false
## 避免浏览器缓存问题
我们打包的时候运行命令 ng build --output-hashing all 这个时候打包的文件都是带有hash值。文件名属于唯一的，和缓存的不一样，所以会去服务器获取最新的资源。

## angular ng build打包后路径错误导致页面404
![](https://cdn.nlark.com/yuque/0/2022/png/1039463/1644474293248-882194df-5e7c-4e84-a9c7-3303de458eeb.png#clientId=u0395be6f-ff35-4&from=paste&id=u12880fcb&originHeight=202&originWidth=844&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=stroke&taskId=uc6de8ef1-30e4-4f89-b6e5-e184bd84c41&title=)
##### 解决：
~~打包时在ng build后加上--base-href ./~~

![image.png](https://cdn.nlark.com/yuque/0/2022/png/1039463/1644476211700-3345dde5-1ff3-4b57-83ea-f9079e9b63ee.png#clientId=u0395be6f-ff35-4&from=paste&height=341&id=u5cb6b300&name=image.png&originHeight=341&originWidth=810&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27792&status=done&style=none&taskId=u30115f17-13d2-4e2e-891b-cbb961b9c4f&title=&width=810)
