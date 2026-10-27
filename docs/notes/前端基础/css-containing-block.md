# Containing Block

## 问题

`position: absolute` 的定位参考系到底是什么？很多人第一反应是"最近的 `position: relative` 祖先"——**这个说法是错的。**

## 正确答案

`position: absolute` 的参考系是**最近的建立了 containing block（包含块）的祖先元素**。`position: relative` 只是建立 containing block 的**其中一种方式**，远非唯一。

## 什么是 Containing Block

Containing block 决定了一个元素在布局中的参考坐标系。具体影响：

- **绝对定位**：`top/right/bottom/left` 和百分比宽高相对于 containing block 计算
- **固定定位**：正常情况 `position: fixed` 相对于视口，但如果祖先有某些 CSS 属性，`fixed` 元素会"叛变"，以那个祖先作为参考系
- **百分比尺寸**：子元素的 `width: 50%`、`height: 100%` 相对于 containing block

## 哪些属性会创建 Containing Block

| 属性 | 触发条件 |
|------|---------|
| `transform` | 非 `none`（包括 `rotate(0deg)`、`translate(0)` 等视觉上等价于 `none` 的值） |
| `will-change: transform` | — |
| `perspective` | 非 `none` |
| `filter` | 非 `none` |
| `backdrop-filter` | 非 `none` |
| `contain` | `paint` / `layout` / `strict` / `content` |
| `container-type` | `size` / `inline-size` |
| `content-visibility` | `auto` |
| `position` | `absolute` / `relative` / `fixed` / `sticky` |

## transform 的特殊之处

CSS 规范明确规定：`transform` 值非 `none` 的元素会为其后代创建 containing block。

这里有一个微妙的陷阱：

```css
/* 视觉表现完全相同，但布局行为不同 */
.parent-a { transform: none; }        /* ❌ 不创建 containing block */
.parent-b { transform: rotate(0deg); } /* ✅ 创建！非 none 即触发 */
.parent-c { transform: translate(0); } /* ✅ 创建！即使位移为零 */
```

`rotate(0deg)` 和 `translate(0)` 在渲染结果上和 `none` 没有区别，但它们是**非 none 值**，所以会触发 containing block 的创建。这是"为什么我的布局突然坏了"的经典诱因——尤其是通过 `transform: translateZ(0)` 这种常见 GPU 加速 hack 意外触发时。

## position: fixed 的"叛变"

正常来说 `position: fixed` 相对于浏览器视口定位。但如果任意祖先元素触发了 containing block（比如设置了 `transform`），`fixed` 就会以那个祖先为参考，不再相对于视口：

```html
<div style="transform: translateZ(0)"> <!-- GPU 加速 hack -->
  <div style="position: fixed; top: 0">
    <!-- 这个元素不再固定在视口顶部，而是相对于上面的 div -->
  </div>
</div>
```

这是模态框、固定导航栏等组件最常遇到的布局异常。

## 结论

1. **`position: absolute` 不是在找 `relative`，是在找 containing block。**
2. `relative` 只是最轻量、最无副作用的 containing block 触发器，所以成为了"教科书式"写法。
3. `transform`、`filter`、`contain` 等属性也会建立 containing block，并且各有性能代价（合成层、GPU 内存等）。
4. 当你只想给子元素一个定位参考系时，`position: relative` 仍然是最佳选择——它不改变元素自身的布局，不创建合成层，不触发任何渲染副作用。
