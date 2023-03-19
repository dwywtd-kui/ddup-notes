## 下载插件 svg
```powershell
npm install svg-sprite-loader
```
##  配置 vue.config.js 文件
```javascript
const path = require('path')

function resolve(dir) {
  return path.join(__dirname, dir)
}
module.exports = {
  //3.0版本
  chainWebpack: config => {
    const svgRule = config.module.rule('svg')
    // 清除已有的所有 loader。
    svgRule.uses.clear()
    svgRule
      .test(/\.svg$/)
      .include.add(path.resolve(__dirname, './src/icons/svg')) //svg文件路径
      .end()
      .use('svg-sprite-loader')
      .loader('svg-sprite-loader')
      .options({
        symbolId: 'icon-[name]'
      })
    const fileRule = config.module.rule('file')
    fileRule.uses.clear()
    fileRule
      .test(/\.svg$/)
      .exclude.add(path.resolve(__dirname, './src/icons/svg')) //svg文件路径
      .end()
      .use('file-loader')
      .loader('file-loader')
  },
}
```

## 写一个 Svg 的组件
```vue
<template>
  <svg :class="svgClass" aria-hidden="true">
    <use :xlink:href="iconName"></use>
  </svg>
</template>
  <script>
/**
 * icon-svg 组件（展示所有的svg）
 */
export default {
  name: "SvgIcon",
  props: {
    iconClass: { type: String },
    className: { type: String },
  },
  computed:{
    iconName(){
      return this.iconClass ? `#icon-${this.iconClass}` : "#icon";
    },
    svgClass(){
      return this.className ? "svg-icon " + this.className : "svg-icon";
    },
  }
};
</script>
  <style scoped>
.svg-icon {
  width: 1em;
  height: 1em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}
</style>
  
  
```
## 在 main.js 中全局注册
```javascript
import { createApp } from 'vue'
import App from './App.vue'
// 导入SvgIcon组件
import SvgIcon from '@/components/SvgIcon.vue' //这是组件路径
const req = require.context('@/icons/svg', false, /\.svg$/)  //这是svg文件路径
req.keys().map(req)
// 创建全局组件，以便任何地方使用

createApp(App).component('svg-icon', SvgIcon).mount('#app')


```

## 使用组件
```vue
<template>
  <div class="about">
    <h1>This is an about page</h1>
    <!-- layout_fold 组件文件名称 -->
    <div class="svg_Error">
      <svg-icon icon-class="Error" class="Error"/>
    </div>
  </div>
</template>

<style scoped>

</style>
```
## 项目结构
![image.png](https://cdn.nlark.com/yuque/0/2022/png/1039463/1666542932694-b350c449-d562-40e0-913c-6ae856dda90b.png#clientId=u98863517-dbbb-4&errorMessage=unknown%20error&from=paste&height=485&id=ub5e3ec14&name=image.png&originHeight=485&originWidth=360&originalType=binary&ratio=1&rotation=0&showTitle=false&size=22177&status=error&style=none&taskId=u1057a5ec-a343-4287-a516-1dc42d24a36&title=&width=360)

参考：
[https://blog.csdn.net/qq_45874251/article/details/120003316](https://blog.csdn.net/qq_45874251/article/details/120003316)
[https://www.cnblogs.com/xjd-6/articles/15608337.html](https://www.cnblogs.com/xjd-6/articles/15608337.html)

项目地址：[https://gitee.com/xiarikui/vue3-test-svgicon](https://gitee.com/xiarikui/vue3-test-svgicon)


