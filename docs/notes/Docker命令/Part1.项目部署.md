# 项目部署

## 1、修改前后端配置文件

- embeddedservices/config/ServicesConfig.xml
- embeddedservices/dist/systemConfig.js

## 2、项目部署更新

- 连接服务器：`ssh root@192.168.16.2`
- 获取 docker 容器 id：`docker ps -a`
- 进入容器 bash：`docker exec -it 容器ID /bin/bash`
- 配置环境变量：`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH: /usr/local/lib/python3.7/site-packages/dmpython-2.4.4-py3.7-1inux-aarch4.egg/`
- 刷新系统配置：`source /etc/profile`
- 查看环境变量：`env`
- 杀死 docker 中的 python 进程：`pkill -9 python`
- 将待部署项目传输到 docker 容器中：`scp -r root@192.168.16.2:/home/ev/sjfxpg/embeddedservices ./`
  - `等价于`在宿主机中将项目拷贝到 docker 容器中：`docker cp ./embeddedservices 容器ID:/root/`
- 在 docker 容器中启动项目：`cd embeddedservices` + `python manage.py`
  - `也可`后台运行项目：`nohup python manage.py &`

## 3、打开达梦数据库

- `cd /home/gz/dmdbms/tool/` 或 `cd /home/dmdba/dm7/tool/`
- `./manager`

## 4、使用镜像

- 将更改过的容器生成新的镜像：`docker commit 容器ID sjfxpg:202412`
  - 查看生成的镜像：`docker images`
- 将镜像打包保存（发给他人）：`docker save -o sjfxpg.tar sjfxpg:202412`
- 加载镜像：`docker load --input sjfxpg.tar`
  - `--input` 可以换成 `-i`

## 5、解决 docker 时间问题

- `‌date -R` 命令用于显示当前时区信息 ‌
- `docker run -v /etc/timezone:/etc/timezone:ro -v /etc/localtime:/etc/localtime:ro your_image`
  - `-v` 参数用于挂载宿主机上的目录或文件到容器内，格式为`宿主机路径:容器内路径:模式`
  - `ro` 为 `readonly` 只读模式
