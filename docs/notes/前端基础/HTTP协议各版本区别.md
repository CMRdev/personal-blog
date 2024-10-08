# HTTP 协议各版本区别

[HTTP 的前世今生](https://coolshell.cn/articles/19840.html)

> HTTP 协议经过多次版本更迭，主要有：`HTTP/1.0`、`HTTP/1.1`、`HTTP/2.0`、`HTTP/3.0`版本

## HTTP/1.0

- 浏览器与服务器只保持`短连接`，浏览器的每次请求都要与服务器建立一个 TCP 连接。并且是`串行接口`。
- 由于浏览器必须等待响应完成才能发起下一个请求，造成`队头阻塞`（高延迟，导致页面加载速度的降低）。

## HTTP/1.1（目前使用最广泛的版本）

- 支持`长连接`，通过`connection: keep-alive`保持 HTTP 连接不断开，避免重复建立 HTTP 连接

  - 注意 `keep-alive` 不会永远保持，它有一个持续时间，一般在服务器中配置（如 apache），另外长连接需要客户端和服务器都支持才有效。

- 支持`管道化传输`，通过长连接实现一个 TCP 连接中同时处理多个 HTTP 请求，第一个请求发出去了，不必等其回来就可以发第二个请求，可以减少整体响应时间。

- 服务器会按照请求的顺序去返回响应的内容，`无法存在并行响应`。HTTP 请求返回顺序按照服务器响应速度来排序，这里会引入`promise.then`和`async await`来控制接口请求顺序

- 新增了一些请求方法、请求头、响应头
  - 支持`断点续传`，新增 Range 和 Content-Range 头表示请求和响应的部分内容
  - 加入`缓存处理`，新增响应头 Expires、Cache-Control
  - 增加`Host`字段，为了支持多虚拟主机的场景，使用同一个 IP 可以托管多个域名，访问的都是同一个服务器，从而满足 HTTP 协议发展所需的更高级特性
  - 增加请求方法：put、delete、options...

## HTTP/2.0

- 采用`二进制`格式，而非之前的文本格式，更安全。
- `多路复用`，在同一个 TCP 连接上`同时`传输多条信息，每个请求和响应都被分配了唯一的标识符，称为`“流stream”`，这样每条信息可以独立地在网络上传输。`没有了对头阻塞`
- 使用`HPACK算法`进行报头压缩，降低开销
- `服务器推送`，支持服务器主动将相关资源预测性地推送给客户端，以减少后续地请求和延迟（如 HTML、CSS、JS、图像和视频等文件）。

## HTTP/3.0

- 是 HTTP/3 中的底层支撑协议，该协议基于 UDP，又取了 TCP 中的精华，实现了`既快又可靠`的功能
- 运输层由 TCP 改成`使用 UDP 传输`
- `队头堵塞问题解决地更彻底`
- `切换网络时的连接保持`，基于 TCP 协议在切换网络时 IP 会改变，因而之前的连接不可能继续保持；而基于 UDP 的 QUIC 协议，则可以内建与 TCP 中不同的连接标识方法，从而在网络完成切换之后，恢复之前与服务器的连接。
- 升级新的压缩算法

> 在 HTTP/2 和 HTTP/3 协议中，数据传输和页面渲染可并行进行
