## 0、重用代码的方式：组件、组合式函数、自定义指令、插件

## 1、组合式函数
- 组合式函数约定用驼峰命名法命名，并以“use”作为开头
```js
// mouse.js
import { ref, onMounted, onUnmounted } from 'vue'
// 按照惯例，组合式函数名以“use”开头
export function useMouse() {
  const x = ref(0)
  const y = ref(0)
  function update(event) {
    x.value = event.pageX
    y.value = event.pageY
  }
  // 一个组合式函数也可以挂靠在所属组件的生命周期上,来启动和卸载副作用
  onMounted(() => window.addEventListener('mousemove', update))
  onUnmounted(() => window.removeEventListener('mousemove', update))

  return { x, y }
}
```
- 我们推荐的约定是组合式函数始终返回一个包含多个 `ref` 的普通的非响应式对象，这样该对象在组件中被解构为 `ref` 之后仍可以保持响应性
- 从组合式函数返回一个响应式对象会导致在对象解构过程中丢失与组合式函数内状态的响应性连接
```js
import { useMouse } from './mouse.js'
// x 和 y 是两个 ref
const { x, y } = useMouse()
```
```js
// 如果你更希望以对象属性的形式来使用组合式函数中返回的状态，你可以将返回的对象用 reactive() 包装一次，这样其中的 ref 会被自动解包
const mouse = reactive(useMouse())
// mouse.x 链接到了原来的 x ref
console.log(mouse.x)
```

- 如果你正在编写一个可能被其他开发者使用的组合式函数，最好处理一下输入参数是 `ref` 或 `getter` 而非原始值的情况。可以利用 toValue() 工具函数来实现
```js
import { toValue } from 'vue'

function useFeature(maybeRefOrGetter) {
  // 如果 maybeRefOrGetter 是一个 ref 或 getter，将返回它的规范化值。否则原样返回。
  const value = toValue(maybeRefOrGetter)
}
```
- `组合式函数`不会产生额外的组件实例开销，`无渲染组件`会产生额外的组件实例开销。
- 我们推荐在纯逻辑复用时使用`组合式函数`，在需要同时复用逻辑和视图布局时使用`无渲染组件`。

## 2、自定义指令
- 自定义指令主要是为了重用涉及普通元素的底层 `DOM` 访问的逻辑。
- 在 `<script setup>` 中，任何以 `v` 开头的驼峰式命名的变量都可以被用作一个自定义指令。
```html
<script setup>
const vFocus = {
  mounted: (el) => el.focus()
}
</script>

<template>
  <input v-focus />
</template>
```
- 指令勾子
```js
const myDirective = {
  created(el, binding, vnode, prevVnode) {
    // el:指令绑定到的元素。这可以用于直接操作 DOM
    // bingding:一个对象 {value,oldValue,arg,modifiers,instance,dir}
    // vnode:绑定元素的底层VNode
    // preVnode:代表之前的VNode。仅在 beforeUpdate 和 updated 钩子中可用。
  },
  beforeMount(el, binding, vnode, prevVnode) {},
  mounted(el, binding, vnode, prevVnode) {},
  beforeUpdate(el, binding, vnode, prevVnode) {},
  updated(el, binding, vnode, prevVnode) {},
  beforeUnmount(el, binding, vnode, prevVnode) {},
  unmounted(el, binding, vnode, prevVnode) {}
}
```

- 简化形式：在 `mounted` 和 `updated` 上实现相同的行为，除此之外并不需要其他钩子
```html
<div v-color="color"></div>
```
```js
app.directive('color', (el, binding) => {
  // 这会在 `mounted` 和 `updated` 时都调用
  el.style.color = binding.value
})
```
- 不推荐在组件上使用自定义指令.

## 3、插件
- 插件 (Plugins) 是一种能为 Vue 添加 `全局功能` 的工具代码
- 一个插件可以是一个拥有 `install()` 方法的对象，也可以直接是一个安装函数本身。安装函数会接收到安装它的应用实例和传递给 `app.use()` 的额外选项作为参数
```js
import { createApp } from 'vue'
const app = createApp({})
app.use(myPlugin, {
  /* 可选的选项 */
})
```
```js
const myPlugin = {
  install(app, options) {
    // 配置此应用
  }
}
```
- 插件发挥作用的常见场景：
```bash
（1）通过 app.component() 和 app.directive() 注册一到多个全局组件或自定义指令。
（2）通过 app.provide() 使一个资源可被注入进整个应用。
（3）向 app.config.globalProperties 中添加一些全局实例属性或方法。
```
- 示例
```js
// plugins/i18n.js
export default {
  install: (app, options) => {
    // 注入一个全局可用的 $translate() 方法
    app.config.globalProperties.$translate = (key) => {
      // 获取 `options` 对象的深层属性
      // 使用 `key` 作为索引
      return key.split('.').reduce((o, i) => {
        if (o) return o[i]
      }, options)
    }
  }
}
```
```js
// 全局注册
import i18nPlugin from './plugins/i18n'
app.use(i18nPlugin, {
  greetings: {
    hello: 'Bonjour!'
  }
})
```
```html
<!-- 使用 -->
<h1>{{ $translate('greetings.hello') }}</h1>
```
