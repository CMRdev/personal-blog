# windows-redis

## 1、windows 版 redis 启动

```bash
# 安装好后，后台启动 redis
./redis-server &

# 检查是否启动成功（返回 PONG 则成功）
./redis-cli ping

# 连接到 redis
./redis-cli

# 使用 redis 中的命令
keys *
set key "helloworld"
get key

# 关闭 redis 客户端
redis-cli shutdown
或：kill -9 PID
```

## 2、windows 安装 redis

- 下载解压：`https://github.com/MicrosoftArchive/redis/releases`
- cmd 进入文件夹输入：运行 redis-server.exe 文件启动服务【6379 端口】
- 打开新的 cmd 窗口执行【安装 redis 在 windows 下的服务】：`.\redis-server.exe --service-install redis.windows.conf`
- services.msc 打开服务，启动 redis 服务

- 测试：Redis 使用

  ```bash
  卸载服务：redis-server --service-uninstall
  开启服务：redis-server --service-start
  停止服务：redis-server --service-stop
  ```

- 开启远程访问：

  ```bash
  redis-cli.exe
  info 【查看版本等信息】
  修改 redis 的配置文件：`redis.windows.conf` #【1、注释掉本地连接：bind 127.0.0.1 2、将默认的守护关闭：protected-mode yes 改为 protected-mode no】
  重启 redis 服务
  ```
