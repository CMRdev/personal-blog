# git 

## 1、本地有变动的情况下拉取代码

```bash
# 用于暂时保存当前工作目录的未提交更改，使工作区恢复到上一次提交的状态
git stash
# 区别于merge，保持提交历史线性、整洁，多用于同步主分支代码
# 但是这个会导致你的commitId里面有其他人的代码，不利于代码review
git config pull.rebase true
git pull origin dev
git stash pop
```


## 2、当前分支与远程分支太久没合并了，出现了大量冲突

```bash
git cherry-pick commitId
git push --set-upstream origin dev-cmr
git log | grep MingRen -A 1 -B 1
git rebase --abort
```

## 3、回退
```bash
# 查看提交记录
git reflog
# 将HEAD重置到某次提交
git reset --hard HEAD{25}
# 更新远程仓库
git push --force-with-lease
```

