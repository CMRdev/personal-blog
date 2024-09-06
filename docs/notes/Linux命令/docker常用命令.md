## 1、Docker 控制命令

- 启动 Docker 服务

  ```bash
  sudo systemctl start docker
  ```

- 使 Docker 服务开机自启

  ```bash
  sudo systemctl enable docker
  ```

- 查看启动状态

  ```bash
  systemctl status docker
  ```

- 停止 docker
  ```bash
  systemctl stop docker
  ```

## 2、Docker 内部命令

- 将基础镜像导入到 docker 中

  ```bash
  docker load -i server7_docker_image.tar
  ```

- 查看镜像是否导入成功(查看所有镜像)

  ```bash
  docker images
  ```

- 启动容器

  ```bash
  docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
  # OPTIONS-包含了一些参数，用于配置和控制容器的各种方面。
  # IMAGE-是要使用的Docker镜像。
  # COMMAND-是在容器内执行的命令，
  # ARG-是该命令的参数。
  ```

- 查看当前运行的镜像及所在容器(列出所有容器)

  ```bash
  docker ps -a
  ```

- 停止容器

  ```bash
  docker stop 容器id|容器name
  ```

- 查看 docker 版本

  ```bash
  docker version
  ```

- 移除镜像

  ```bash
  docker rmi -f ...
  ```

- 移除容器

  ```bash
  docker rm -f 容器名/ID
  ```

- 进入容器 `bash`

  ```bash
  docker exec -it '容器 ID' bash
  ```

- 退出容器`bash`

  ```bash
  ctrl+Q+P
  ```

## 3、示例解析

```bash
#!/bin/bash -
set -o nounset                              # Treat unset variables as an error

CUR_DIR=$(cd $(dirname $0) && pwd)

docker run -d --name evserver7 --privileged --hostname ev7 --rm --entrypoint /opt/EV-Server7/bin/startup.sh --env LANG=zh_CN.utf8 -p 8888:8088 -v $CUR_DIR:/opt/EV-Server7 -v /opt/test:/opt/test  kylinv10-desktop-aarch64:base run

#docker run -itd --name evserver7 --hostname ev7 --rm --entrypoint /opt/EV-Server7/bin/startup.sh --env LANG=zh_CN.UTF-8 -v $CUR_DIR:/opt/EV-Server7 -v /home/data1:/opt/testdata -p 19088:8088     evserver7-gdal:base run

#docker run  -itd --name evserver7 --hostname ev7  --restart=always   --entrypoint /opt/EV-Server7/bin/startup.sh --env LANG=zh_CN.UTF-8 -v $CUR_DIR:/opt/EV-Server7 -v /home/data1:/opt/testdata -p 19088:8088    evserver7-gdal:base run
```

| 指令         | 说明                                                                                                          |
| ------------ | ------------------------------------------------------------------------------------------------------------- |
| docker run   | 创建一个新的容器并运行一个命令                                                                                |
| -itd         | i 表示一直运行，t 给容器分配一个伪终端（-it,允许我们对容器进行交互式操作），d 表示后台运行容器，并返回容器 id |
| -p           | 指定端口映射，格式为：主机端口:容器端口。-p 8888:8088 表示指定映射的主机端口为 8888，容器端口为 8088          |
| -v           | 表示绑定一个卷，即映射数据路径和程序路径，格式为：主机路径:容器路径                                           |
| --name       | 为容器指定一个名称，--name evserver7 表示指定容器名称为 evserver7                                             |
| --privileged | 使容器内的 root 拥有真正的 root 权限                                                                          |
| --hostname   | 设置容器内部的主机名，影响容器内部服务的网络配置和识别                                                        |
| --entrypoint | 设置运行的命令                                                                                                |
| --env        | 设置环境变量                                                                                                  |
| --rm         | 容器退出时，自动清除挂载的卷，以便清除数据，等价于在容器退出后执行`docker rm -v`命令                          |
