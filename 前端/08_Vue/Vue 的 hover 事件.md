## 需求
对于所遍历的数据都加上一个 hover 事件，当鼠标放在某条数据上时，做一些操作，当鼠标移开时，停止这些操作。
## 问题
vue中没有hover
## 解决方案

- 使用css伪类：hover  
- 使用事件监听 @mouseenter    @mouseleave   @mouseover  @mouseout 等处理类似需求
## 示例
这里记录下使用事件监听处理的使用：
@mouseenter 是值元素获得鼠标焦点后执行的方法
@mouseleave 是当元素执行了 @mouseenter 离开之后执行的方法
```vue
<div id="app">
    <p @mouseenter="enter" @mouseleave="leave">{{ message }}</p>
</div>

var vm = new Vue({
    el: '#app',
    data: {
        message: '默认值'
    },
    methods: {
        enter: function(e){
            console.log(e);
            this.message = '修改值';
        },
        leave: function(e){
            this.message = '默认值111';
        }
    }
});
```

