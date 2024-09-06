1. 打开 git GUI

```bash
gitk
```

2. 常用 git 命令

```bash
	git pull <远程仓库名> <分支名>		#拉取（会合并）
	git fetch <远程仓库名> <分支名>		#获取（不会合并）

	git init	#初始化主分支
	git clone ...		#克隆远程仓库
	git clone -b dev ...	# 克隆dev分支
	git status		#查看状态
	git add xxx		#将文件xxx存入暂存区
	git add b c 	#把b和c存入暂存区
	git add .			#将所有文件提交到暂存区
	git checkout -- xxx 	#撤销工作区的修改（eg. git checkout -- readme.md	#将本次readme.md在工作区的修改撤销掉）
	git commit -m 备注信息	#提交到仓库
	git commit -am 备注信息	#若仓库中已有若干文件，再次提交可简化为此步
	git stash -u -k 	#提交部分内容到仓库。如有a、b、c三个文件，只想提交a、b到远程仓库：
				#git add a b
				#git stash -u -k
				#git commit -m 备注信息
				#git push
				#git stash pop	#把之前放入堆栈的c拿出来
```

3. 其他

```bash
	git helper -a	#查看全部git子命令
	git blame xxx	#逐行查看文件xxx的修改历史
	git blame -L 100,10 xxx	#查看从100行开始的10行文件xxx的修改历史

	#删除放入暂存区文件的方法（已commit）
	git rm 文件名	#将该文件从commit后撤回到add后

	git diff	#工作区与暂存区的差异
	git diff --cached	#暂存区与提交版本的差异
	git show HEAD	#查看最后一次提交修改的详细信息

```

4. 合并 dev 分支代码到 master

```bash
	git checkout master
	git merge dev
	git push origin master # 将当前更改推送到远程的master分支

```

5. 打 tag

```bash
	git tag -a v1.0.0 -m "..."
	git push origin v1.0.0
```
