
## Vue2中使用
> 2.2.0+ 新增

一个组件上的 v-model 默认会利用名为 value 的 prop 和名为 input 的事件，但是像单选框、复选框等类型的输入控件可能会将 value attribute 用于不同的目的。model 选项可以用来避免这样的冲突：
```vue
Vue.component('base-checkbox', {
model: {
  prop: 'checked',
  event: 'change'
},
props: {
	checked: Boolean
},
template: <input type="checkbox" v-bind:checked="checked" v-on:change="$emit('change', $event.target.checked)" >
})
```

现在在这个组件上使用 v-model 的时候：
```html
<base-checkbox v-model="lovingVue"></base-checkbox>
```

这里的 lovingVue 的值将会传入这个名为 checked 的 prop。同时当 触发一个 change 事件并附带一个新的值的时候，这个 lovingVue 的 property 将会被更新。

> 注意你仍然需要在组件的 props 选项里声明 checked 这个 prop。

## Vue3中使用
### v-model 使用 modelValue
自定义事件可以用于开发支持 v-model 的自定义表单组件。回忆一下 v-model 在原生元素上的用法：
```html
<input v-model="searchText" />
```
上面的代码其实等价于下面这段 (编译器会对 v-model 进行展开)：
```html
<input
  :value="searchText"
  @input="searchText = $event.target.value"
/>
```
而当使用在一个组件上时，v-model 会被展开为如下的形式：
```html
<CustomInput
  :modelValue="searchText"
  @update:modelValue="newValue => searchText = newValue"
/>
```
要让这个例子实际工作起来，<CustomInput> 组件内部需要做两件事：

1. 将内部原生 input 元素的 value attribute 绑定到 modelValue prop
2. 输入新的值时在 input 元素上触发 update:modelValue 事件

这里是相应的代码：
```vue
<!-- CustomInput.vue -->
<script>
  export default {
    props: ['modelValue'],
    emits: ['update:modelValue']
  }
</script>

<template>
  <input
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    />
  </template>
```
现在 v-model 也可以在这个组件上正常工作了：
```html
<CustomInput v-model="searchText" />
```

另一种在组件内实现 v-model 的方式是使用一个可写的，同时具有 getter 和 setter 的计算属性。get 方法需返回 modelValue prop，而 set 方法需触发相应的事件：
```vue
<!-- CustomInput.vue -->
<script>
export default {
  props: ['modelValue'],
  emits: ['update:modelValue'],
  computed: {
    value: {
      get() {
        return this.modelValue
      },
      set(value) {
        this.$emit('update:modelValue', value)
      }
    }
  }
}
</script>

<template>
  <input v-model="value" />
</template>
```

### 自定义 v-model 的使用的参数
默认情况下，v-model 在组件上都是使用 modelValue 作为 prop，并以 update:modelValue 作为对应的事件。我们可以通过给 v-model 指定一个参数来更改这些名字：
```html
<MyComponent v-model:title="bookTitle" />
```
在这个例子中，子组件应声明一个 title prop，并通过触发 update:title 事件更新父组件值：
```vue
<!-- MyComponent.vue -->
<script>
export default {
  props: ['title'],
  emits: ['update:title']
}
</script>

<template>
  <input
    type="text"
    :value="title"
    @input="$emit('update:title', $event.target.value)"
  />
</template>
```

### 多个 v-model 绑定
利用刚才在 v-model 参数小节中学到的技巧，我们可以在一个组件上创建多个 v-model 双向绑定，每一个 v-model 都会同步不同的 prop：
```vue
<UserName
  v-model:first-name="first"
  v-model:last-name="last"
/>
<script>
export default {
  props: {
    firstName: String,
    lastName: String
  },
  emits: ['update:firstName', 'update:lastName']
}
</script>

<template>
  <input
    type="text"
    :value="firstName"
    @input="$emit('update:firstName', $event.target.value)"
  />
  <input
    type="text"
    :value="lastName"
    @input="$emit('update:lastName', $event.target.value)"
  />
</template>
```

### 自定义v-model 的修饰符
在学习输入绑定时，我们知道了 v-model 有一些内置的修饰符，例如 .trim，.number 和 .lazy。在某些场景下，你可能想要一个自定义组件的 v-model 支持自定义的修饰符。

我们来创建一个自定义的修饰符 capitalize，它会自动将 v-model 绑定输入的字符串值第一个字母转为大写：
```html
<MyComponent v-model.capitalize="myText" />
```

组件的 v-model 上所添加的修饰符，可以通过 modelModifiers prop 在组件内访问到。在下面的组件中，我们声明了 modelModifiers 这个 prop，它的默认值是一个空对象：
```vue
<script>
export default {
  props: {
    modelValue: String,
    modelModifiers: {
      default: () => ({})
    }
  },
  emits: ['update:modelValue'],
  created() {
    console.log(this.modelModifiers) // { capitalize: true }
  }
}
</script>

<template>
  <input
    type="text"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>
```

注意这里组件的 `modelModifiers` prop 包含了 `capitalize `且其值为 true，因为它在模板中的 v-model 绑定上被使用了。

有了 `modelModifiers `这个 prop，我们就可以在原生事件侦听函数中检查它的值，然后决定触发的自定义事件中要向父组件传递什么值。在下面的代码里，我们就是在每次 <input> 元素触发 input 事件时将值的首字母大写：
```html
<script>
export default {
  props: {
    modelValue: String,
    modelModifiers: {
      default: () => ({})
    }
  },
  emits: ['update:modelValue'],
  methods: {
    emitValue(e) {
      let value = e.target.value
      if (this.modelModifiers.capitalize) {
        value = value.charAt(0).toUpperCase() + value.slice(1)
      }
      this.$emit('update:modelValue', value)
    }
  }
}
</script>

<template>
  <input type="text" :value="modelValue" @input="emitValue" />
</template>
```

对于又有参数又有修饰符的 v-model 绑定，生成的 prop 名将是 arg + "Modifiers"。举例来说：
```html
<MyComponent v-model:title.capitalize="myText">
```

相应的声明应该是：
```vue
export default {
  props: ['title', 'titleModifiers'],
  emits: ['update:title'],
  created() {
    console.log(this.titleModifiers) // { capitalize: true }
  }
}
```

参考：
[https://cn.vuejs.org/guide/components/events.html#events-validation](https://cn.vuejs.org/guide/components/events.html#events-validation)
[https://v2.cn.vuejs.org/v2/guide/components-custom-events.html](https://v2.cn.vuejs.org/v2/guide/components-custom-events.html)

