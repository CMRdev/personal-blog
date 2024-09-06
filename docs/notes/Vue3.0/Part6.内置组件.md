## 1、Transition

- 组件进入和离开 DOM 时应用动画
- 触发条件：v-if、v-show、`<component>`动态组件、改变特殊的 key 属性
- 插槽仅支持单个 DOM
- 大多数的现代浏览器都可以在执行 transform 动画时利用 GPU 进行硬件加速
- 像 `height` 或者 `margin` 这样的属性会触发 `CSS` 布局变动，因此需要谨慎使用
- [更多内容 >>](https://cn.vuejs.org/guide/built-ins/transition.html)
- transition 动画执行过程图：
  ![](./image/transition动画class.png)

```html
<!-- 可设置name属性 -->
<Transition name="bounce">
  <p v-if="show" style="text-align: center;">Hello here is some bouncy text!</p>
</Transition>
```

```css
.bounce-enter-active {
  animation: bounce-in 0.5s;
}
.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.25);
  }
  100% {
    transform: scale(1);
  }
}
```

## 2、TransitionGroup

- 用于对 `v-for` 列表中的元素或组件的插入、移除和顺序改变添加动画效果
- CSS 过渡 `class` 会被应用在列表内的元素上，而不是容器元素上
- 列表中的每个元素都必须有一个独一无二的 `key` attribute

```html
<!-- 设置 tag="ul"，将在外面渲染一个ul容器 -->
<TransitionGroup name="list" tag="ul">
  <li v-for="item in items" :key="item">{{ item }}</li>
</TransitionGroup>
```

```css
.list-move, /* 对移动中的元素应用的过渡，防止周围元素跳动 */
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

/* 确保将离开的元素从布局流中删除
  以便能够正确地计算移动的动画。 */
.list-leave-active {
  position: absolute;
}
```

## 3、KeepAlive

- 在多个组件间动态切换时缓存被移除的组件实例
- 可使用`include\exclude`来定制要缓存的组件

```html
<!-- 以英文逗号分隔的字符串 -->
<KeepAlive include="a,b">
  <component :is="view" />
</KeepAlive>

<!-- 正则表达式 (需使用 `v-bind`) -->
<KeepAlive :include="/a|b/">
  <component :is="view" />
</KeepAlive>

<!-- 数组 (需使用 `v-bind`) -->
<KeepAlive :include="['a', 'b']">
  <component :is="view" />
</KeepAlive>
```

```html
<script setup>
  import { onActivated, onDeactivated } from "vue";
  onActivated(() => {
    // 调用时机为首次挂载
    // 以及每次从缓存中被重新插入时
  });
  onDeactivated(() => {
    // 在从 DOM 上移除、进入缓存
    // 以及组件卸载时调用
  });
</script>
```

## 4、Teleport

- 可以将一个组件内部的一部分模板`“传送”`到该组件的 DOM 结构外层的位置去

```html
<!-- to 的值可以是一个 CSS 选择器字符串，也可以是一个 DOM 元素对象 -->
<Teleport to="body">
  <div v-if="open" class="modal">
    <p>Hello from the modal!</p>
    <button @click="open = false">Close</button>
  </div>
</Teleport>
```
