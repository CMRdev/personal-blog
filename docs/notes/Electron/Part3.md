# knowledge

- Electron 继承了来自 Chromium 的`多进程`架构

## 1、命名规范

- (PascalCase) 命名可实例化的类
- (camelCase) 命名不可实例化的函数、变量等

## 2、nodejs 概念

- `__dirname` 字符串指向当前正在执行的脚本的路径。
- `path.join` API 将多个路径联结在一起，创建一个跨平台的路径字符串。

## 3、进程间通信

- 进程间通信 (IPC)。可以使用 Electron 的 `ipcMain 模块`和 `ipcRenderer 模块`来进行进程间通信。 为了从你的网页向主进程发送消息，你可以使用 ipcMain.handle 设置一个主进程处理程序（handler），然后在预处理脚本中暴露一个被称为 ipcRenderer.invoke 的函数来触发该处理程序（handler）

- 预加载脚本`preload.js`包含在浏览器窗口加载网页之前运行的代码。 其可访问 `DOM` 接口和 `Node.js` 环境，并且经常在其中使用 `contextBridge` 接口将特权接口暴露给渲染器。

- 由于主进程和渲染进程有着完全不同的分工，Electron 应用通常使用预加载脚本`preload.js`来设置进程间通信 (IPC) 接口以在两种进程之间传输任意信息。

## 4、搭建 electron+vite+vue 框架

- `npm create electron-vite`

  // "dev": "vite",
  // "build": "vue-tsc && vite build && electron-builder",
  // "preview": "vite preview",
