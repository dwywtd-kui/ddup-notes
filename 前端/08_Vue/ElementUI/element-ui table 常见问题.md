## 监听表格下拉滚动事件
### 背景
做管理平台的项目, 用到了 element-ui，需要通过监听 el-table 滚动的位置来获取最新的数据，那么怎么样监听 el-table 的滚动呢？
### 解决
```vue
mounted() {
  // 获取需要绑定的table
  this.dom = this.$refs.table.bodyWrapper
  this.dom.addEventListener('scroll', () => {
     // do some thing...
  })
}
```
参考文档：[https://segmentfault.com/a/1190000018648004](https://segmentfault.com/a/1190000018648004)
