## 1、什么是 SCP？

> `scp（Secure Copy Protocol）`是一个用于在本地计算机和远程计算机之间进行文件传输的命令行工具，它基于` SSH（Secure Shell）`协议，提供了加密和安全的文件传输功能。scp 可以用于将文件和目录从一台计算机复制到另一台计算机，也可以用于从远程计算机复制文件到本地计算机。

> 例如，如果你想将文件复制到 Linux 系统，并且你担心网络上的窥探者可能会访问你的文件，则可以轻松使用 SCP 命令。SCP 在 SSH（安全外壳）连接上进行加密，这确保即使数据被截获，它仍然受到保护。

## 2、使用示例

```bash
scp [选项] [源文件/目录] [目标]

#上传docker到服务器目录/opt/
scp -r C:\...\docker-19.03.9.tgz  root@192.168.2.30:/opt/

scp -i F:/cmr/saver.pem -r dist/ root@114.55.166.40:/home/target-display

# -r：递归复制，用于复制目录及其内容。
# -i：指定身份验证密钥文件。
# -P：指定远程 SSH 端口号。
# -v：详细模式，显示详细的传输信息。
# -q：安静模式，减少输出信息。
# -C：开启压缩传输，可以减少数据传输量。
# -p：保留文件属性（权限、时间戳等）。

```

## 3、公网之间

> scp 最初设计用于在`本地网络或局域网`中进行文件传输，但它也可以用于在互联网上远程计算机之间进行文件传输。

- 通过公网 IP 地址或域名访问远程计算机：如果你知道远程计算机的公网 IP 地址或域名，并且你具有远程计算机的 SSH 登录权限，你可以使用 scp 通过互联网将文件传输到远程计算机或从远程计算机获取文件。

```bash
scp localfile.txt username@remote_ip_or_domain:/remote/path/
```

- 使用 SSH 跳转主机：如果你需要通过一个中间主机（跳转主机）来访问目标远程计算机，你可以使用 scp 的 -J 选项来实现。这个一般用于跨越多个网络层次的访问。

```bash
scp -J jump_host_username@jump_host_ip localfile.txt username@remote_ip_or_domain:/remote/path/
# jump_host_username 和 jump_host_ip 是跳转主机的用户名和IP地址。
```
