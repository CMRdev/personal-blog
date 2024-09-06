## 1、script 标签根据加载顺序分为：常规加载、async 加载、defer 加载

- 常规加载

```js
<script src="xxx.js"></script>
// 加载过程：中断网页渲染 -> 下载 -> 解析 -> 执行 -> 网页继续渲染
```

- defer 加载

```js
<script src="xxx.js" defer></script>
// 加载过程：下载 -> 等网页渲染结束 -> 解析 -> 执行
```

- async 加载

```js
<script src="xxx.js" async></script>
// 下载 -> 中断网页渲染 -> 解析 -> 执行 -> 网页继续渲染
```

## 2、type="module"的模块会默认使用 defer 加载方式
