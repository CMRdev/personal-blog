# Linux常用命令

## 1、查看配置信息

- 查看系统版本号
  ```bash
  uname -r
  cat /etc/os-release
  ```
- 查看系统型号是不是 x86

  ```bash
  uname -a
  ```

- 查看系统时间
  ```bash
  date
  ```
- 查看硬件时间
  ```bash
  hwclock
  ```

## 2、基础命令

- 解压

  ```bash
  tar -zxvf  xxx
  ```

- 查看 U 盘盘符

  ```bash
  fdisk -l
  ```

- U 盘挂载到/mnt

  ```bash
  ntfs-3g /dev/sda1 /mnt
  ```

- 取消挂载

  ```bash
  umount /mnt
  ```

- 设置文件格式

  ```bash
  :set ff=unix
  ```

- 查看文件大小

  ```bash
  du -h filename
  ```

- 列出所有 TCP、UDP 协议的监听状态的套接字

  ```bash
  ss - tuln
  # -t表示TCP
  # -u表示UDP
  # -l表示仅列出正在监听的套接字
  # -n表示以数字形式显示端口号，而不是使用服务名称
  ```

- 添加执行权限
  ```bash
  chmod +x /usr/lib/systemd/system/docker.service
  ```

## 3、防火墙控制

- 麒麟系统开启防火墙状态
  ```bash
  systemctl start firewalld
  ```
- 麒麟系统关闭防火墙
  ```bash
  systemctl stop firewalld
  ```
- 麒麟系统查看防火墙状态
  ```bash
  systemctl status firewalld
  ```
- 重新加载配置文件
  ```bash
  systemctl daemon-reload
  ```

## 4、linux 安装 nodejs

- 将 nodejs 解压到任意位置
- 创建 node 和 npm 快捷方式到对应的 /usr/bin 文件夹下【注意使用绝对路径】
  ```bash
  ln -s /node-v16.8.0-linux-arm64/bin/node /usr/bin/node
  ln -s /node-v16.8.0-linux-arm64/bin/npm /usr/bin/npm
  ```
