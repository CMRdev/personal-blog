# SSH 连接到远程机器

## 1、SSH Client 的基本使用方法

- 我们可以通过`SSH Client`连接到运行了`SSH Server`的远程机器上
- `SSH Client`：Xshell、FinalShell、MobaXterm、OpenSSH、PuTTY......

```bash
ssh user@remote -p port
# user 是你在远程机器上的用户名，如果不指定的话默认为当前用户
# remote 是远程机器的地址，可以是 IP，域名，或别名
# port 是 SSH Server 监听的端口，如果不指定的话就为默认值 22
```

## 2、安装`OpenSSH Server`

```bash
local$ ssh user@remote -p port
ssh: connect to host remote port 22: Connection refused
```

- 当你遇到上面的消息，说明远程机器上没有安装`SSH Server`，如果你有`sudo`权限，可执行如下命令安装

```bash
sudo apt-get install openssh-server
```
