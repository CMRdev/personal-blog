# 修改 jar 中的配置文件

## 1、步骤

```bash
# 1 查找配置文件
jar -tvf xxx.jar/application-linux.yml

# 2 提取配置文件
jar -xvf xxx.jar BOOT-INF/classes/application-linux.yml

# 3 修改配置文件
vim application-linux.yml

# 4 更新jar的配置文件
jar -uvf xxx.jar application-linux.yml
```

## 2、使用 dockerfile 打包镜像

```bash
# 打包项目为镜像image-name，到当前目录下
docker build -t image-name .
```
