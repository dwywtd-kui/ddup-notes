## 如何在vs code中运行js文件

### code runner
使用插件“code runner”运行js：
1. 在vs code右侧工具栏的 extensions 里搜索 “code runner”，并安装；
2. vs code右上角有一个 三角形状 按钮，是运行js文件用的，点击即可运行；

[https://www.jianshu.com/p/64627ec33008](https://www.jianshu.com/p/64627ec33008)

### 常见问题
问题1：code runner 默认是不会清除之前的输出结果的，并且每次运行之前需要自己手动保存刚才编辑的js文件才能使得修改生效；
```
file -> preferences ->settings->选择workspace ->找到 Run Code configuration -> 找到"Clear previous output"并勾选，找到 “Save all files before run”并勾选 ->关闭Settings ->再次修改js文件然后运行发现设置生效。
```

问题2：VSCode Code Runner输出中文乱码：
```
通过设置，可以把代码放到 VS Code 内置的 Terminal 来运行，那么问题就能迎刃而解了。

选择 文件 -> 首选项 -> 设置，打开 VS Code 设置页面，

找到 Run Code configuration，勾上 Run In Terminal 选项。设置之后，代码就会在 Terminal 中运行即可。
```

