## 1、script 标签根据加载顺序分为：常规加载、async 加载、defer 加载

- 常规加载

```js
<script src="xxx.js"></script>
// 加载过程：中断网页渲染 -> 下载 -> 解析 -> 执行 -> 网页继续渲染
```

- defer 加载

```js
<script src="xxx.js" defer></script>
// 加载过程（渲染完再执行）：下载 -> 等网页渲染结束 -> 解析 -> 执行
```

- async 加载

```js
<script src="xxx.js" async></script>
// 加载过程（下载完就执行）：下载 -> 中断网页渲染 -> 解析 -> 执行 -> 网页继续渲染
// 多个async脚本不能保证加载顺序，因为不确定脚本什么时候能下载完
```

## 2、type="module"的模块会默认使用 defer 加载方式
