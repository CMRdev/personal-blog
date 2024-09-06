## windows 版 redis 启动

- 安装好后，后台启动 redis

  ```bash
  ./redis-server &
  ```

- 检查是否启动成功（返回 PONG 则成功）

  ```bash
  ./redis-cli ping
  ```

- 连接到 redis：
  ```bash
  ./redis-cli
  ```
- 使用 redis 中的命令

  ```bash
  keys *
  set key "helloworld"
  get key
  ```

- 关闭 redis 客户端
  ```bash
  redis-cli shutdown
  或：kill -9 PID
  ```
