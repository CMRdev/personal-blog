# Git 常用命令

## 1、配置

```bash
git help config #打开html查看帮助文档
git config -h #控制台查看简易版帮助文档

git config user.name #查看配置【--show-origin 显示文件目录】
git config --global user.name #查看全局配置
git config --global --list #查看所有配置项【--show-origin显示目录】

# 安装完 Git 之后，要做的第一件事就是设置你的用户名和邮件地址。
# 这一点很重要，因为每一个 Git 提交都会使用这些信息，它们会写入到你的每一次提交中，不可更改
git config --global user.name '用户名'
git config --global user.email '邮箱'

# 如果不想在每一次推送时都输入用户名与密码（http）：
git config --global credential.helper cache #【15min】
git config --global credential.helper store #【永久】
```

## 2、生成.git 仓库

```bash
# 方式一
git init #初始化本地git仓库，主分支默认为master
# 方式二（clone后自动生成.git目录）
git clone ... #克隆远程仓库
git clone -b dev ... #克隆 dev 分支
```

## 3、常规命令

```bash
git fetch <远程仓库名> <分支名> #获取（不会合并）
git pull <远程仓库名> <分支名> #拉取（会合并 = fetch + merge）
git add . #将所有文件提交到暂存区
git add b c #把 b 和 c 存入暂存区
git commit -m 备注信息 #提交到本地仓库
git commit -a -m 备注信息 #可以跳过git add的暂存步骤，前提是已跟踪文件
git push -u origin master` #推送到远程仓库 origin 的 master 分支(-u 是指在将当前分支与远程分支进行关联，下次推送直接git push)
```

```bash
gitk #打开GUI
git diff #工作区与暂存区的差异
git diff --cached #暂存区与提交版本的差异
git show HEAD #查看最后一次提交修改的详细信息
git status #查看当前分支状态
git reset HEAD readme/a.md #将文件移出暂存区
git checkout -- readme/a.md #放弃修改（从 git 本地仓库检出这个文件覆盖当前的修改）
git rm readme/a.md #将该文件从暂存区和工作区中删除
```

## 4、分支合并

```bash
# 合并 dev 分支代码到 master
git checkout master
git merge dev
git push origin master #将当前更改推送到远程的 master 分支
git checkout dev
```

## 5、打 tag

```bash
git tag v1.0.0 #适用于内部版本控制
git tag -a v1.0.0 -m "..." #创建有附注的标签（annotated tag），公开发行
git push origin v1.0.0
```
