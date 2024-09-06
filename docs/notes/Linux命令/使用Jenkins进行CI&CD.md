### 0、Jenkins卸载安装

- 【Jenkins卸载】

  ~~~bash
  # rpm卸载
  	rpm -e jenkins
  # 检查是否卸载成功
  	rpm -ql jenkins
  # 彻底删除残留文件
  	find / -iname jenkins | xargs -n 1000 rm -rf
  ~~~
  
- 【jenkins安装（rpm）：（先看7）】

    ~~~bash
    1、下载rpm地址：https://mirrors.tuna.tsinghua.edu.cn/jenkins/redhat/?C=M&O=A
      	jenkins-2.401.3-1.1.noarch.rpm
    2、cd /usr/local/jenkins 并输入rz命令上传rpm文件
    3、安装：rpm -ivh jenkins-........noarch.rpm   【查看安装是否成功：rpm -ql jenkins】
    4、修改配置：vim /etc/sysconfig/jenkins
      			JENKINS_PORT="8777"
    5、配置jenkins的java路径：
      	whereis java
      	vim /etc/init.d/jenkins
      	下拉到candidates字段，粘贴java的安装路径，:wq保存退出
      	刷新配置：systemctl daemon-reload
    6、启动：systemctl start jenkins
      	【报错了】：
      		systemctl status jenkins.service  查看错误
      	解决：
      		不使用systemctl的方式操作Jenkins, 直接用Jenkins自带的服务启动 (使用 systemctl 最终也是执行的这个命令)
      		切换到 Jenkins 脚本目录 cd /etc/init.d, 执行以下命令
      	# 启动
     		./jenkins start
     	# 停止
     		./jenkins stop
     	# 状态
     		./jenkins status
     	【又报错了】-Jenkins版本过高了，不支持java 8
     	Starting Jenkins Running with Java 8 from /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.262.b10-1.el7.x86_64/jre, which is older 	                         than the minimum required version (Java 11).
     	Supported Java versions are: [11, 17]
     	See https://jenkins.io/redirect/java-support/ for more information.
    
    7、尝试下载老版本Jenkins：https://jenkins.io/redirect/java-support/
    	“从 6 月 28 日发布的 Jenkins 2.357 和即将发布的 9 月 LTS 版本开始，Jenkins 最低需要 Java 11”
    
    	下载2.357以下的Jenkins版本：jenkins-2.346.3-1.1.noarch.rpm
    	重复上面五个步骤
    
    8、无法启动：jenkins通过systemctl start jenkins.service启动服务，端口不是配置文件里自定义的端口
    	vim /lib/systemd/system/jenkins.service
    	# 修改端口号
        Environment="JENKINS_PORT=8777"
    9、启动成功
    ~~~

### 1、Jenkins配置

- linux服务器需要配置maven环境、nodejs环境、npm环境，下载对应的包并安装

- Jenkins安装插件：manage jenkins --> plugins

  搜索maven、nodejs
  
- 全局工具配置：manage Jenkins --> Global Tool Configuration

  配置jdk：/usr/local/jdk1.8.0_181

  配置maven：/usr/local/soft/apache-maven-3.5.4

### 2、后台启动脚本startup.sh
```bash
#!/bin/bash
#定义启动的jar包或者war包程序
application_name=targetdisplay-admin.jar
#定义外部配置文件，若不使用外部配置文件则将nohup开头的两行命令注释互换，即打开下方被注释的nohup启动命令并注释当前nohup启动命令
#config_path=application.yml
#定义日志文件
DIR="/usr/local/soft/target_display_server"
application_port=18080
log_name=log.txt
echo Starting application ${application_name}... 
#nohup java -jar ${application_name} -Dspring.config.location=${config_path} > ${log_name} 2>&1 &
nohup java -jar ${DIR}/${application_name} --server.port=${application_port} > ${DIR}/${log_name} 2>&1 &
#nohup java -jar ${DIR}/${application_name} --server.port=${application_port} > /dev/null 2>&1 &
#tail -f ${DIR}/${log_name}
# (hack) sleep 1 minute，让项目跑起来 
# sleep 20
```

### 3、后台关闭脚本stop.sh

~~~bash
#!/bin/bash
#定义关闭的jar包或者war包程序
application_name=targetdisplay-admin.jar
PID=$(ps -ef | grep /usr/local/soft/target_display_server/${application_name} | grep -v grep | awk '{ print $2 }')
if [ -z "$PID" ]
then
    echo ${application_name} is already stopped
else
    echo ${application_name} has killed,pid is $PID
    kill $PID
fi
~~~

### 4、实时数据启动脚本startup.sh

```bash
#!/bin/bash
application_name=sendSocket.jar
DIR="/usr/local/soft/sendsocket"
application_port=18998
log_name=log.txt
echo Starting application ${application_name}... 
#nohup java -jar ${application_name} -Dspring.config.location=${config_path} > ${log_name} 2>&1 &
nohup java -jar ${DIR}/${application_name} --server.port=${application_port} > ${DIR}/${log_name} 2>&1 &
#nohup java -jar ${DIR}/${application_name} --server.port=${application_port} > /dev/null 2>&1 &
#tail -f ${DIR}/${log_name}
# (hack) sleep 1 minute，让项目跑起来 
# sleep 20
```

### 5、实时数据关闭脚本stop.sh

```bash
#!/bin/bash
application_name=sendSocket.jar
PID=$(ps -ef | grep /usr/local/soft/sendsocket/${application_name} | grep -v grep | awk '{ print $2 }')
if [ -z "$PID" ]
then
    echo ${application_name} is already stopped
else
    echo ${application_name} has killed,pid is $PID
    kill $PID
fi
```

### 6、jenkins制定完任务后，点击立即构建，控制台报错（...无法生成父级目录）

~~~bash
原因是：
jenkins 使用的 jenkins 用户和组，而  /data/maven/repository 的用户和组是 root。
解决方案：改变repository的用户组为Jenkins即可
chown -R jenkins:jenkins /data/maven/repository
~~~

### 7、Jenkins执行shell脚本权限不够

~~~bash
vim /usr/lib/systemd/system/jenkins.service
修改：
User=root
Group=root

systemctl daemon-reload
systemctl restart jenkins
~~~

### 8、构建好的jar包位置(可配置：vim /etc/sysconfig/jenkins)

~~~bash
/var/lib/jenkins/workspace/target-display-server/targetdisplay-admin/target/targetdisplay-admin.jar
~~~

### 9、target-display-front配置执行脚本

~~~bash
# remove dist
rm -rf /var/lib/jenkins/workspace/target-display-front/dist/*
npm install
npm run build
cd /var/lib/jenkins/workspace/target-display-front/dist
cp -rf ./index.html ./static /usr/local/soft/target_display_front
~~~

### 10.0、maven项目：Build -> Goals and options

~~~bash
clean package -Dmaven.test.skip=true
# maven 打包命令：
# mvn compile：编译
# mvn clean：清除target
# mvn package：项目编译、单元测试、打包
# mvn install：项目编译、单元测试、打包、将打好的包部署到本地仓库（在有多个项目互相依赖的情况下经常使用）
# mvn deploy：项目编译、单元测试、打包、将打好的包部署到本地仓库、将打好的包部署到远程仓库
# mvn [ package | install | deploy ] -DskipTests：不执行测试用例，但编译测试用例到对应的target下
# mvn [ package | install | deploy ] -Dmaven.test.skip：不执行测试用例，也不编译测试用例
~~~

### 10、target-display-server配置执行脚本

~~~bash
# stop jar
sh /usr/local/soft/target_display_server/stop.sh
# copy
cp -f /var/lib/jenkins/workspace/target-display-server/targetdisplay-admin/target/targetdisplay-admin.jar /usr/local/soft/target_display_server
# Jenkins默认会在Build结束后Kill掉所有的衍生进程
BUILD_ID=dontKillMe
# start jar
sh /usr/local/soft/target_display_server/startup.sh
~~~

### 11、send-socket配置执行脚本

~~~bash
# stop jar
sh /usr/local/soft/sendsocket/stop.sh
# copy
cp -f /var/lib/jenkins/workspace/send-socket/target/sendSocket.jar  /usr/local/soft/sendsocket
# Jenkins默认会在Build结束后Kill掉所有的衍生进程
BUILD_ID=dontKillMe
# start jar
sh /usr/local/soft/sendsocket/startup.sh
~~~





