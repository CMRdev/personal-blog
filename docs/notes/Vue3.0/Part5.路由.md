## 1、简单路由
- 通过监听浏览器 `hashchange` 事件或使用 `History API` 来更新当前组件
```html
<script setup>
import { ref, computed } from 'vue'
import Home from './Home.vue'
import About from './About.vue'
const routes = {
  '/': Home,
  '/about': About
}
const currentPath = ref(window.location.hash)
window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
})
const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/']
})
</script>
<template>
  <a href="#/">Home</a> |
  <a href="#/about">About</a>
  <component :is="currentView" />
</template>
```
## 2、Vue Router

[参见VueRouter官方文档](https://router.vuejs.org/zh/)
