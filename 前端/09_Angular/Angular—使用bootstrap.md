[https://www.cnblogs.com/liyong-blackStone/p/10195169.html](https://www.cnblogs.com/liyong-blackStone/p/10195169.html)

由于 Bootstrap 官方目前并没有发布 Angular 的相关类库进行支持，当前 Angular 只能引用使用 Bootstrap 相关的样式。无法使用 Bootstrap 自带的脚本逻辑。以下以 Angular7 和 Bootsrap4.2 为例进行 demo 验证。

**环境搭建**

首先执行以下两个命令创建 angular 项目和组件

ng new AngularDemo //创建项目 
ng g c bootstrapdemo // 创建组件

然后执行
npm install bootstrap // 安装最新的bootstrap组件

![](https://img2018.cnblogs.com/blog/1307383/201812/1307383-20181229115428189-963650011.png#id=prkG3&originHeight=128&originWidth=707&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

执行过程中发现警告 bootstrap 以来 jquery 和 popper.js
npm i jquery popper.js

![](https://img2018.cnblogs.com/blog/1307383/201812/1307383-20181229115514233-1064041155.png#id=QiyZ7&originHeight=147&originWidth=960&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

**引入样式**

**方法一：**

找到 index.html 直接添加样式引用

```html
<link rel="stylesheet" href="http://cdn.bootcss.com/bootstrap/3.3.0/css/bootstrap.min.css">
```

![](https://img2018.cnblogs.com/blog/1307383/201812/1307383-20181229120032465-694825764.png#id=GqPwz&originHeight=282&originWidth=1113&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

**方法二：**

打开 Angular.json 文件找到 project->architect->builder->options 下的 style 和 scripts 两个配置节。并将 bootstrap 的样式引入到 styles 中。由于 angular 只能引用 bootstrap 样式，所以 scripts 不需要引用 bootstrap 相关脚本 (引用了也不生效)。

![](https://img2018.cnblogs.com/blog/1307383/201812/1307383-20181229120057276-224990776.png#id=ZF7Zr&originHeight=524&originWidth=645&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

**验证**

copy 一段最简单的 bootstrap 栅格做个验证。

```html
<!-- Stack the columns on mobile by making one full-width and the other half-width -->
    <div>
      <div>.col-12 .col-md-8</div>
      <div>.col-6 .col-md-4</div>
    </div>
    
    <!-- Columns start at 50% wide on mobile and bump up to 33.3% wide on desktop -->
    <div>
      <div>.col-6 .col-md-4</div>
      <div>.col-6 .col-md-4</div>
      <div>.col-6 .col-md-4</div>
    </div>
    
    <!-- Columns are always 50% wide, on mobile and desktop -->
    <div>
      <div>.col-6</div>
      <div>.col-6</div>
    </div>
```


![](https://img2018.cnblogs.com/blog/1307383/201812/1307383-20181229120143387-2146163399.png#id=xIS0e&originHeight=162&originWidth=1109&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=stroke&title=)
