# 关联 Gitlab

## 1、方式一

1. 在 gitLab 中创建一个空项目
2. 进入本地电脑中一个文件目录，右击鼠标选择“ Git Bash Here” git 命令窗口(本机电脑要安装好 git)
3. 在“ Git Bash Here” git 命令窗口输入命令：

```bash
git clone 项目地址
```

4. cd 进入项目，把需要上传的文件都移动到该目录下
5. 在“ Git Bash Here” git 命令窗口输入命令：

```bash
git add .   # 加入到暂存区
git commit -m "Initial commit"  #提交到本地仓库
git push -u origin master  #推送到远程仓库origin（git将远程仓库自动命名为origin）的master分支
# -u 是指在将当前分支与远程分支进行关联，关联后可简化命令：git push
```

## 2、方式二

1. 打开`Git Bash Here`命令窗口
2. `git init` - 初始化 git 项目
3. `git add .` - 添加到暂存区
4. `git commit -m 'message'` - 提交到本地仓库
5. `git remote add origin http://82.157.206.150/17s-situation/git-test` - 关联远程仓库
6. `git push -u origin master` - 推送到远程仓库 origin 的 master 分支

## 3、在 github 上下载了 zip 包

> 如何将 zip 包关联到 github 仓库？

- git init
- git add .
- git commit -m 'Initial commit'
- git remote add origin https://github.com/CesiumGS/cesium.git
- git remote -v
- git fetch origin main ## 单独 fetch 某个分支的更新
