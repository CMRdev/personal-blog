# Linux 常用命令

## 1、Linux 目录解释

- /boot/ 系统启动
- /bin/ 系统命令
- /sbin/ 系统环境设置命令，只有 root 用户可用
- /dev/ 设备文件
- /etc/ 配置文件（系统内所有采用 rpm 安装的服务配置文件，如用户信息、服务的启动脚本、常用服务的配置文件）
- /home/ 普通用户的主目录（家目录）
- /root/ root 用户的主目录
- /lib/ 系统调用的函数库
- /media/ 挂载媒体设备，软盘、光盘
- /mnt/ 挂载目录，U 盘、移动硬盘、其他操作系统的分区
- /misc/ 挂载目录，挂载 NFS 服务的共享目录
- /opt/ 第三方软件安装目录【也可安装到/usr/local 下】
- /srv/ 服务数据目录
- /tmp/ 临时目录，不要保存重要数据，最好每次开机都把该目录清空

## 2、修改 jar 包里面的内容

```bash
jar -tf zhts-admin.jar # 查找配置文件所在路径
jar -xvf zhts-admin.jar B00T-INF/classes/application-linux.yml # 提取配置文件, 会在当前目录下生成BOOT-INF文件夹
jar -uvf zhts-admin.jar B00T-INF/classes/application-linux.yml # 更新jar的配置文件
docker build -t zhts-admin . # 使用当前目录下的dockerfile文件打包镜像
```

- `jar -txuvf`

```bash
-t # list
-x # extract 解压，从jar文件中提取内容
-u # update
-v # verbose 详细输出
-f # file 指定文件
```

- `docker build -t <镜像名>:<版本> <上下文路径（dockerfile文件所在路径）>`

```bash
-t # tag 为构建的docker镜像指定一个名称和可选标签
```

## 3、Linux 常用命令解析

- `tar -zxvf archive.tar.gz` 【-z:使用 gzip 解压缩文件】
- `tar -cvf archive.tar.gz file.txt`【将 file.text 文件压缩为 archive.tar.gz】【-c:create，创建新的归档文件】
- `ls -lh /data`【-l:long-fommat，长格式，显示文件和目录的详细信息】【-h:human-readable，人类可读(KB\MB\GB)】
- `touch file.txt`【创建文件】
- `rm -rf` 【-r:recursive,逆归】【-f: force】
- `which cat`【查看 cat 命令存放的位置】
- `find /data-name "test.txt"`【查找文件位置】
- `grep "a" file.txt`【从 file.txt 文件中过滤出带有“a”的行】
- `ls -l | grep "test"`【管道符左边命令的结果作为右边的输入】
- `echo "test add" >> file.txt`【追加】
- `echo "test add" > file.txt`【覆盖】
- `tail -f log.txt`【自动显示 log.txt 文件中新增的内容默认 10 条】【-f:follow，实时跟踪文件的更新】
- `vim`

```bash
  # 命令模式下:
      移动光标:h左、j下、k上、l右
      0当前行开头、$当前行结尾
      nyy复制当前行下的n行、p粘贴、u撤销修改
      gg跳到首行、G跳到未尾
      d$删除到本行的末尾、d0删除到本行开头
  # 底线命令模式下:
      :set nu 显示行号
```

- `权限`

```bash
# d rwx r-x r-X
文件类型|用户的权限|用户组的权限|其他用户的权限
-表示文件、d表示文件夹、l表示软连接
rwx:读、写、执行
chmod 777 file.exe
```

- `查看历史命令`

```bash
ctrl+r #搜索历史命令
history # 查看历史命令
!+命令 #自动执行上一次匹配前缀的命令
```
