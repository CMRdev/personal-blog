# 杂记

## 1、当 fixed 元素写在 overflow 元素中时，滑动页面，fixed 元素会跟着滑动然后归位，如果 fixed 元素是图片则会出现图片闪动的现象

- 解决：将 fixed 元素写在 overflow 元素的外面。

## 2、阻塞浏览器渲染进程的情况

- js 执行、alert、css 渲染

## 3、nextTick

- 在`created()`函数中进行的 dom 操作要放在`Vue.nextTick`的回调函数中
- 在数据变化后要执行的某个操作，而这个操作需要使用随数据改变而改变的 DOM 结构的时候，这个操作都应该放进`Vue.nextTick()`的回调函数中。

## 4、js 知识

- const、let 在同一作用域下不能声明同名常量/变量
- const 一旦声明必须赋值，不能使用 null 占位，声明后不能修改
- 实例属性：实例属性是指在构造函数方法中定义的属性
- 原型属性`prototype`：

  > 原型属性指的是不在构造函数中定义的属性（多用于定义全局变量，不污染全局作用域）
  > prototype 属性的作用：解决构造函数的对象实例之间无法共享属性的缺点。原型对象上的所有属性和方法，都会被对象实例所共享。对于构造函数来说，prototype 是作为构造函数的属性；对于对象实例来说，prototype 是对象实例的原型对象。所以 prototype 即是属性，又是对象。

- 序列化
  > 类的对象会随着程序的终止而被垃圾收集器销毁，如果要在不重新创建对象的情况下调用该类，该怎么做？ `通过序列化将数据转换为字节流`。
  > 可将此字节流保存到磁盘文件中或通过网络发送到任何其他程序。从字节流创建对象的过程称为反序列化。创建的字节流是与平台无关的，在一个平台上序列化的对象可以在不同平台上反序列化。
  > Serializable 接口：一个类只有实现了 serializable 接口，他的对象才能被序列化
  > `序列化是将对象状态转换为可保持或可传输格式的过程。`这个接口是给 JVM 看的让 jvm 进行对象序列化。

## 5、promise

```js
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("foo");
  }, 300);
});
myPromise
  .then((value) => {
    console.log(value);
  })
  .catch((err) => {
    console.error(err);
  });
```

- Promise 对象只有：从 pending 变为 fulfilled 和从 pending 变为 rejected 的状态改变。只要处于 fulfilled 和 rejected ，状态就不会再变了即 resolved（已定型）。
- 使用 promise 我们可以用同步的方式写异步代码
- then 方法接收两个函数作为参数，`resolve（）`执行 then，`reject（）`执行 catch
- `reject和catch的区别`： then 的第一个函数出错了，后面的 catch 可以捕获，写到 then 的第二个函数则捕获不到 ；reject 是用来抛出异常的，catch 才是用来处理异常的，类比传统的 try catch 写法，reject 就相当于 throw，【reject 是 Promise 的方法，而 catch 是 Promise 实例的方法】

## 6、为什么“this”上可以直接挂载未声明的变量？

- 首先，如果这样写你还困惑吗：let p = { name: 'Jone' } p.age = 18
- 可以将 this 看成一个 vue 示例，
- 分析：编程语言大体可以分为两种：
  - 静态类型语言：在编译时就确定了变量的类型，不能更改，如 c、c++、java...
  - 动态类型语言：在程序运行时才确定变量的类型，如 js（弱类型）、python（强类型：变量确定类型后会持有这个类型）
