## 1、Linux 系统 nginx 项目部署

- 文件传输工具 lrzsz
  ```bash
  # lrzsz工具可以使xshell工具方便地上传下载文件，比使用scp命令方便些
  # 有资料说lrzsz工具仅支持4GB以下的文件上传
  # 使用root用户进行安装
  yum install -y lrzsz
  # sz：将选定的文件发送到本地机器，运行命令后会弹出保存位置窗口（send）
  # rz：运行该命令会弹出一个文件选择窗口，从本地选择文件上传到服务器(receive)
  ```
- 安装 nginx

  > [官网下载：http://nginx.org/en/download.html](http://nginx.org/en/download.html)

  ```bash
  # 解压
  tar -zxvf 资源包
  # 在解压后的包路径下配置
  ./configure --prefix=/usr/local/nginx-1.20.2 --with-http_ssl_module --with-http_stub_status_module
  # --prefix 代表安装的路径
  # --with-http_ssl_module 安装ssl
  # --with-http_stub_status_module查看nginx的客户端状态

  # 编译安装
  make & make install
  # 找到安装路径：/usr/local/nginx-1.20.2，执行sbin下的nginx命令：
  ./nginx
  # 修改配置后重新加载nginx
  ./sbin/nginx -s reload
  # 访问ip
  172.16.0.43:80
  ```

- nginx 发布项目

  ```bash
  # 删除旧版本项目数据
  rm -rf /usr/local/nginx-1.24.0/html/dist  # -r：递归、-f：强制
  # xshell中使用 rz 命令上传文件并解压dist
  rz
  unzip dist.zip
  ```

- 其他

  ```bash
  # 查看端口状态
  netstat -nltp
  # 查看端口是否开放（有显示则开放）
  lsof -i:8084
  # 开放 8084 端口
  systemctl start firewalld
  firewall-cmd --zone=public --add-port=8084/tcp --permanent
  firewall-cmd --reload

  # 检查nginx配置
  sudo nginx -t
  # 重新加载配置文件
  nginx -s reload

  # linux 本机访问端口
  curl localhost:8084

  # 进入/etc/ssh/sshd_config 文件进行权限修改
  PermitRootLogin yes # root 可以登录
  PasswordAuthentication yes # 允许用户以密码认证的方式登录
  systemctl restart sshd # 重启 sshd 服务
  ```
