# linux 常用命令

## 1、常用命令一

- 查看磁盘使用情况：`df -h`
- 查看当前文件夹下的文件占用大小：`du -sh *`
- 重新启动 redis: `nohup ./redis-server &`
- 赋予脚本执行权限：`chmod +x startup.sh stop.sh`

- 查看日志文件鼠标定位到最后一行：`G`
- 查看日志文件鼠标定位到文件头：`gg`
- 删除文件： `rm filename`
- 进程查看：`ps -aux|grep sendSocket.jar`
- 查看后台运行的进程【当前终端】：`jobs -l`
- 进程查看命令：`ps -aux|grep chat.js`
  - a：显示所有
  - u：以用户为主的形式来显示
  - x：显示所有程序，不以终端机来区分
- 查看使用某端口的进程：`lsof -i:8090`
- 根据进程 id 查看进程占用的端口：`netstat -nap|grep 5156`

## 2、手动跑 jar 包

- 查看 jar 包占用的 pid：`ps -ef|grep xxx.jar`
- 杀死进程：`kill -9 pid`
- 启动进程：`nohup java -jar xxx.jar`
- 更换后台 jar 包端口为 18080：`nohup java -jar targetdisplay-admin.jar --server.port=18080 >log.txt 2>&1 &`
- 指定配置文件：`nohup java -Dserver.port=8086  -Dspring.config.additional-location=./application-dev.yml -jar ./springboot.jar> nohup.out 2>&1 &`

## 3、基础知识

- linux 下的软件包分两种：

  - 源码包（安装慢，需要编译）
  - 二进制包（安装快）

- 二进制包管理系统：`RPM（CentOS）、DPKG（Ubuntu）`
  - `yum`是改进型的 RPM 软件管理器，解决了 rpm 所面临的软件包依赖问题
  - 查看 yum 是否安装：`rpm -qa | grep yum`

## 4、命令解析

- `nohup sh test.sh /dev/null 2>&1`
  - `nohup`：no hang up【不挂起】
  - `&0`：键盘输入
  - `&1`：屏幕输出
  - `&2`：错误输出
  - `2>1`：错误重定向到一个文件 1 中
  - `2>&1`：标准输出
  - `总结`：后台执行 test.sh 这个脚本，把标准错误重定向到标准输出，然后扔到/dev/null 中去，即把所有标准输出和错误输出都扔到垃圾桶里。
- `command > out.txt 2>&1 &`
  - `command > out.txt`：将 command 的输出重定向到`out.txt`文件中【不是将输出内容打到屏幕上】
  - `2>&1`： 是将标准出错（2）重定向到标准输出（1），而这里的标准输出已经重定向到了`out.txt`文件，所以标准出错也会输出到`out.txt`文件中。最后一个`&`，是让该命令在后台执行
- `command > out.txt 2>file 和 command > out.txt 2>&1 有什么不同`

  - `command > out.txt 2>file` 的意思是将 command 产生的所有`stdout`和`stderr`信息都送到 out.txt 中，out.txt 会被打开两次，这样 stdout 和 stderr 信息会互相覆盖
  - `command > out.txt 2>&1` 是将`stdout`直接写入 out.txt，stderr【继承】了 stdout 的管道后，再被送往 out.txt，此时 out.txt 只被打开了一次

- `-z` 在 if 里的意思是 “空”，`[ -z “$1” ]`这是需要返回一个值 0 或者 1。如果地址为空则...

  ```bash
  ADDRESS=$1
  if [ -z $ADDRESS ]; then
    ADDRESS="localhost:9200"
  fi
  ```

- `curl`命令作用是发出网络请求然后获取数据显示在标准输出上，`curl -s` 不输出统计信息

  ```bash
  curl -s "http://$ADDRESS" 2>&1 > /dev/null
  ```

- `$?` 是一个特殊的 shell 变量，用于存储上一个命令的执行状态。当一个 shell 命令执行完毕后，它会返回一个状态值，表示该命令执行的结果。
- `$?` 变量会自动保存该状态值，以便后续的脚本代码可以根据该状态值来判断命令是否执行成功。
- 状态值是一个整数，它的取值范围通常为 `0` 到 `255`。其中，状态值为 `0` 表示命令执行成功，而非零状态值则表示命令执行失败或出现错误

  ```bash
  if [ $? != 0 ]; then
      echo ‘...’
  fi
  ```
