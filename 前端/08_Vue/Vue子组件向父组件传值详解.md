## 子组件向父组件传递一个值
子组件：
```vue
this.$emit('change', this.value);
```
父组件：
```vue
<!-- 在父组件中使用子组件 -->
<editable-cell :text="text" :inputType="inputType" @change="change($event)" />
```

```vue
// 事件处理函数
async changee(value) {
	console.log(value)
}
```

在使用子组件时，绑定 change 函数的事件处理函数也可以写成如下格式：
```vue
<editable-cell :text="text" :inputType="inputType" @change="change" />
```
绑定事件处理函数时，可以不带括号，形参则默认为事件对象，如果绑定时带上了括号，再想使用事件对象则需要传入 $event 作为实参。
## 子组件向父组件传递一个值，并携带额外参数
> 说明：record为额外参数( 本文的额外参数都拿record做举例 )

子组件：
```vue
this.$emit('change', this.value);
```
父组件：
```vue
<!-- 插槽 -->
<template slot="planned_amount" slot-scope="text, record">
  <!-- 在父组件中使用子组件 -->
  <editable-cell :text="text" :inputType="inputType" @change="change(record,$event)" />
</template>
```

```vue
  // 事件处理函数
  async costPlannedAmountChange(record,value) {
  console.log(record,value)
  },
```
绑定事件处理函数时，record和$event的顺序不做要求，但是按照vue事件绑定的习惯，event 通常放在实参列表末尾。
## 子组件向父组件传递多个值
子组件：
```vue
// 向父组件传递了两个值
    this.$emit('change', this.value,this.text);
```
父组件：
```vue
<editable-cell :text="text" :inputType="inputType" @change="change" />
```

```vue
// 事件处理函数
    async change(param1,param2) {
    console.log(param1,param2)
    },
```
**绑定事件处理函数时，不要携带括号!!!，如果携带括号并且在括号内加了 $event，只能拿到子组件传递过来的第一个参数。**

## 子组件向父组件传递多个值，并携带额外参数
> 说明record为额外参数( 本文的额外参数都拿record做举例 )。

子组件：
```vue
// 向父组件传递了两个值
    this.$emit('change', this.value,this.text);
```
父组件：
```vue
<template slot="planned_amount" slot-scope="text, record">
  <!-- 在父组件中使用子组件 -->
  <editable-cell :text="text" :inputType="inputType" @change="change(record,arguments)" />
  </template>
```
`arguments`是方法绑定中的一个关键字，内部包括了所有方法触发时传递过来的实参。
`arguments` 和额外参数的位置谁先谁后不做要求，建议 `arguments `放后面。

查看 args 的打印结果：
![](https://img-blog.csdnimg.cn/20200831171051700.png#pic_center#id=kWQyR&originHeight=163&originWidth=932&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=stroke&title=)

原文地址：[https://blog.csdn.net/weixin_43242112/article/details/108324304](https://blog.csdn.net/weixin_43242112/article/details/108324304)

