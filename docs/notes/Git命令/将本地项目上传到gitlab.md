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
	git push -u origin master  #将本地master推送到远程origin分支
```

6. 小组其他成员不可以修改 master 分支，所以记得再创建 dev 分支【或者修改 master 分支保护权限】
