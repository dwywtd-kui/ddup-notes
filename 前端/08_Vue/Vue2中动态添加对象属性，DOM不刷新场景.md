## 添加属性的问题
```vue
<template>
  <div>
    <p v-for="(value,key) in obj" :key="key">
      {{ value }}
    </p>
    <button @click="addProperty">动态添加新属性</button>
  </div>
</template>


<script>
  export default {
    data:()=>{
      obj:{
        oldProperty:"旧值"
      }
    },
    methods:{
      addProperty(){
        this.obj.newProperty = "新值"  // 为items添加新属性
        console.log(this.items)  // 输出带有newProperty的items
      }
    }

  };
</script>
```

这时候我们会遇到一个问题：在方法中修改变量时，log 打印结果了，对象数据是正确的，但是 dom 并没有重新渲染。
## 问题分析
出现这种情况的原因是由于vue2.x的基本原理决定的。vue2的基本原理是通过Object.defineProperty在初始化时重写data中定义的变量的get和set方法来实现监听变量的改变和通知页面重新渲染的。

> Object.defineProperty() 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。
> Object.defineProperty(obj, prop, descriptor)
> obj: 要定义属性的对象。
> prop: 要定义或修改的属性的名称或 Symbol 。
> descriptor: 要定义或修改的属性描述符。


假如你在vue中定义了一个对象：`obj: {name: "test"}`，vue在created之前会重写`objTest`对象中name的 get 和 set :
```javascript
// 先把原来的obj深拷贝一份
var obj_copy = JSON.parse(JSON.stringfy(this.obj));
var newObjTest = Object.defineProperty(objTest, 'name', {
        get: function () {
            // 返回objCopy的name，如果返回obj.name会死循环
            return objCopy.name;
        },
        set: function (newValue) {
            // 把objCopy的name属性重新赋值
            objCopy.name = newValue;
            // 去通知页面obj的name的值变了，该渲染页面了
            ......
        }
    })
```
当我们给obj.name属性赋值的时候，会走我们重新定义的set方法，并让页面重新渲染，但是为什么有时候却不行呢？这就是Object.defineProperty的不足之处了，因为在vue中它只会遍历已有的对象及其属性，未定义的属性vue是不会重写get和set的方法的。
所以如果你在data中没有定义某个对象属性，而在后续的操作中添加了新的属性时，页面是不会重新渲染的。

## 解决方案
由于 Vue 已经不允许在已经创建的实例上添加新的响应式属性，所有可以采用以下三种方法：

-  Vue.set() 
-  Object.assign() 
-  $forcecUpdated() 
### Vue.set()
Vue.set(target, propertyName/index, value)

- 参数 1：target：要修改的对象或数组
- 参数 2：propertyName/index：属性或下标
- 参数 3：value：修改后的 value 值

还可以使用 vm.$set 实例方法，这也是全局 Vue.set 方法的别名：
this.$set(target, propertyName/index, valu)

> Vue.set() 方法会调用 defineReactive 方法，给新增属性设置成响应式，内部还是通过 Vue.defineProperty 实现属性拦截。

```javascript
function set (target: Array<any> | Object, key: any, val: any): any {
  ...
  defineReactive(ob.value, key, val)
  ob.dep.notify()
  return val
}
```
使用示例：
```javascript
this.$set(this.obj, 'newProperty', '新值')
```
### Object.assign()

- 参数 1：一个空对象，用来存放新增属性与原对象混合之后的对象
- 参数 2：原来的对象
- 参数 3：需要给对象新增的属性

```javascript
this.item = Object.assign({},this.obj,{newProperty:'新值'})
```
### 使用  $forcecUpdated 方法强制刷新
在 Vue 实例添加这个方法，强制 Vue 实例进行重新渲染
this.$forcecUpdated()

## 小结

- 如果需要添加少量属性，可直接采用 Vue.set()
- 如果需要添加大量属性，就采用 Object.assign()
- 强制刷新采用 $forcecUpdated()（不推荐）

PS：vue3 是用过 proxy 实现数据响应式的，直接动态添加新属性仍可以实现数据响应式
