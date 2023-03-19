## 安装 `vue-cli`
cnpm install -g @vue/cli
## 安装 `webpack`
webpack 是 JavaScript 打包器 (module bundler)
cnpm install -g webpack
## 使用 vue-cli 创建项目
vue create hello-world
## 常见问题
### 用户命令行权限不足
| 错误提示 | vue : 无法加载文件 D:\\Program Files\\nodejs\\node_global\\vue.ps1，因为在此系统上禁止运行脚本。 |
| --- | --- |
| 报错原因 | 由于用户权限不足，无法加载文件，以管理员身份运行cmd也可以解决此问题。 |
| 解决方法 | 
1. 在终端中继续输入Set-ExecutionPolicy -Scope CurrentUser，执行命令后会显示如下
```powershell
位于命令管道位置 1 的 cmdlet Set-ExecutionPolicy
请为以下参数提供值:
ExecutionPolicy:
```

2. 继续输入 `RemoteSigned`，回车
3. 选择更改执行策略
 |
| 操作示例 | ![image.png](https://cdn.nlark.com/yuque/0/2022/png/1039463/1666507678497-30ec18bf-360c-4090-9481-699e507f9cad.png#averageHue=%23131313&clientId=u2be0913e-77ba-4&from=paste&height=326&id=HqFvB&name=image.png&originHeight=326&originWidth=986&originalType=binary&ratio=1&rotation=0&showTitle=false&size=18499&status=done&style=none&taskId=u0c0d1872-cc78-4db8-bd6d-debc646687f&title=&width=986) |


