## 1、多个组件共享一个共同的状态
- 一个简单直接的解决方案是抽取出组件间的共享状态，放在一个全局单例中来管理。
```js
// store.js
import { reactive } from 'vue'
 // 也可使用其他形式的响应式api：ref、computed或一个组合式函数来定义共享状态
export const store = reactive({
  count: 0,
  increment() { // 内聚更改共享状态的方法，使代码易于维护
    this.count++
  }
})
```
```html
<!-- 在多个组件中共享 -->
<script setup>
import { store } from './store.js'
</script>

<template>
  <button @click="store.increment()">{{ store.count }} </button>
</template>
```
## 2、更好的解决方案：Pinia
- 更强的团队协作约定
- 与 Vue DevTools 集成，包括时间轴、组件内部审查和时间旅行调试
- 模块热更新 (HMR)
- 服务端渲染支持
***

### 2.0、安装、引入

```powershell
yarn add pinia
# 或者使用 npm
npm install pinia
```
```js
import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'

const pinia = createPinia()
const app = createApp(App)

app.use(pinia)
app.mount('#app')
```
***
- Pinia已经移除vuex(version<=4)中的 `mutation`
- Pinia 的目录一般被命名为 `stores` 而不是 `store`。这是为了强调 Pinia 可以使用多个 store，而不是 Vuex 的单一 store。
***
- `Store (如 Pinia)` 是一个保存状态和业务逻辑的实体。它有三个概念，`state`、`getter` 和 `action`，我们可以假设这些概念相当于组件中的 data、 computed 和 methods。

```js
import { defineStore } from 'pinia'
// 第一个参数是你的应用中 Store 的唯一 ID。
// 第二个参数可接受两类值：Setup 函数或 Option 对象
export const useAlertsStore = defineStore('alerts', {
  // 其他配置...
})
```

### 2.1、Option Store (state、getters、action)
```js
export const useCounterStore = defineStore('counter', {
  state: () => ({ count: 0 }),
  getters: {
    double: (state) => state.count * 2
  },
  actions: {
    increment() {
      this.count++
    }
  }
})
```
### 2.2、Setup Store【我们推荐使用这个模式】
- `ref()` 就是 state 属性
- `computed()` 就是 getters
- `function()` 就是 actions
```js
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  const doubleCount = computed(() => count.value * 2)
  function increment() {
    count.value++
  }

  return { count, doubleCount, increment }
})
```
- `Setup store` 也可以依赖于全局提供的属性，比如路由。任何`应用层面提供的属性`都可以在 store 中使用 inject() 访问，就像在组件中一样.
```js
import { inject } from 'vue'
import { useRoute } from 'vue-router'

export const useSearchFilters = defineStore('search-filters', () => {
  const route = useRoute()
  // 这里假定 `app.provide('appProvided', 'value')` 已经调用过
  const appProvided = inject('appProvided')

  return {
    // ...
  }
})
```
- 创建store实例
- `store` 是一个用 `reactive` 包装的对象，这意味着不需要在 getters 后面写 `.value`。就像 setup 中的 props 一样，我们不能对其进行解构.
```html
<script setup>
import { useCounterStore } from '@/stores/counter'
// ✨
const store = useCounterStore()
// ❌ 这将不起作用，因为它破坏了响应性
// 这就和直接解构 `props` 一样
const { name, doubleCount } = store
// ✅ 这样写是响应式的
// 💡 当然你也可以直接使用 `store.doubleCount`
const doubleValue = computed(() => store.doubleCount)
// ...
</script>
```
- 如何解构？ `storeToRefs`
```html
<script setup>
import { storeToRefs } from 'pinia'
const store = useCounterStore()
// `name` 和 `doubleCount` 是响应式的 ref
const { name, doubleCount } = storeToRefs(store)
// 作为 action 的 increment 可以直接解构
const { increment } = store
</script>
```


  