## 1、props
- 在使用 `<script setup>` 的单文件组件中，props 可以使用 defineProps() 宏来声明
```js
const props = defineProps({
  propE: {
    type: Object,
    // 对象或数组的默认值必须从一个工厂函数返回。
    // 该函数接收组件所接收到的原始 prop 作为参数。
    default(rawProps) {
      return { message: 'hello' }
    }
  },
  // 自定义类型校验函数
  // 在 3.4+ 中完整的 props 作为第二个参数传入
  propF: {
    validator(value, props) {
      return ['success', 'warning', 'danger'].includes(value)
    }
  },
  // 函数类型的默认值
  propG: {
    type: Function,
    // 不像对象或数组的默认，这不是一个工厂函数。这会是一个用来作为默认值的函数
    default() {
      return 'Default function'
    }
  }
})
```
- 当一个 prop 被声明为允许多种类型时，有一种边缘情况——只有当 Boolean 出现在 String 之前时，Boolean 转换规则才适用
```js
// disabled 将被解析为空字符串 (disabled="")
defineProps({
  disabled: [String, Boolean]
})
```
## 2、事件
- 组件触发的事件没有冒泡机制
- 和对 `props` 添加类型校验的方式类似，所有触发的事件也可以使用对象形式来描述
```js
const emit = defineEmits({
  // 没有校验
  click: null,
  // 校验 submit 事件
  submit: ({ email, password }) => {
    if (email && password) {
      return true
    } else {
      console.warn('Invalid submit event payload!')
      return false
    }
  }
})
function submitForm(email, password) {
  emit('submit', { email, password })
}
```
## 3、v-model
- `defineModel()`返回的值是一个ref
```js
<script setup>
const model = defineModel()
</script>

<template>
  <input v-model="model" />
</template>
```
- v-model 也可以接受一个参数
```js
// 父组件
<MyComponent v-model:title="bookTitle" />
// 子组件
const title = defineModel('title', { required: true })
```

## 4、透传attributes【不是响应式的】
- 如果你不想要一个组件自动地继承 `attribute`，可以直接在 `<script setup>` 中使用 defineOptions
```html
<script setup>
defineOptions({ inheritAttrs: false })
// ...setup 逻辑
</script>
```
- 最常见的需要禁用 `attribute` 继承的场景就是 `attribute` 需要应用在根节点以外的其他元素上。通过设置 `inheritAttrs` 选项为 `false`，你可以完全控制透传进来的 `attribute` 被如何使用。
```html
<script setup>
defineOptions({ inheritAttrs: false })
</script>

<div class="btn-wrapper">
  <button class="btn" v-bind="$attrs">click me</button>
</div>
```
- 在 `JavaScript` 中访问透传 `Attributes`
```html
<script setup>
import { useAttrs } from 'vue'

const attrs = useAttrs()
</script>
```

## 5、插槽
- `v-slot` 有对应的简写 `#`，因此 `<template v-slot:header>` 可以简写为 `<template #header>`
```html
<!-- 子组件BaseLayOut -->
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```
```html
<!-- 父组件 -->
<BaseLayout>
  <template #header>
    <h1>Here might be a page title</h1>
  </template>

  <!-- 隐式的默认插槽 -->
  <p>A paragraph for the main content.</p>
  <p>And another one.</p>

  <template #footer>
    <p>Here's some contact info</p>
  </template>
</BaseLayout>
```
- 父组件调取子组件中的内容
```html
<!-- 子组件 -->
<div>
  <slot :text="greetingMessage" :count="1"></slot>
</div>
```
```html
<!-- 父组件调用子组件中内容 -->
<MyComponent v-slot="slotProps">
  {{ slotProps.text }} {{ slotProps.count }}
</MyComponent>
<!-- 也可使用解构语法 -->
<MyComponent v-slot="{ text, count }">
  {{ text }} {{ count }}
</MyComponent>
```

## 6、依赖注入
- 当提供 / 注入响应式的数据时，建议尽可能将任何对`响应式状态`的变更都保持在供给方组件中
```html
<!-- 在供给方组件内 -->
<script setup>
import { provide, ref } from 'vue'
const location = ref('North Pole')
function updateLocation() {
  location.value = 'South Pole'
}
provide('location', {
  location,
  updateLocation
})
</script>
```
```html
<!-- 在注入方组件 -->
<script setup>
import { inject } from 'vue'
const { location, updateLocation } = inject('location')
</script>

<template>
  <button @click="updateLocation">{{ location }}</button>
</template>
```
## 7、异步组件

- 得到的 `AsyncComp` 是一个外层包装过的组件，仅在页面需要它渲染时才会调用加载内部实际组件的函数。它会将接收到的 props 和插槽传给内部组件，所以你可以使用这个异步的包装组件无缝地替换原始组件，同时实现延迟加载。
```js
import { defineAsyncComponent } from 'vue'

const AsyncComp = defineAsyncComponent(() =>
  import('./components/MyComponent.vue')
)
```
