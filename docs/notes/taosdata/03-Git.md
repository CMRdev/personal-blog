# Git 常用操作

## 1、本地有变动的情况下拉取代码

- `git stash` — 暂时保存当前工作目录的未提交更改，使工作区恢复到上一次提交的状态
- `git config pull.rebase true` — 区别于 merge，保持提交历史线性、整洁，多用于同步主分支代码（但会导致 commitId 混入他人代码，不利于 code review）
- `git pull origin dev`
- `git stash pop` — 恢复暂存的更改

## 2、当前分支与远程分支太久没合并，出现大量冲突

- `git cherry-pick <commitId>` — 选取指定提交应用到当前分支
- `git push --set-upstream origin dev-cmr`
- `git log | grep MingRen -A 1 -B 1` — 过滤查看指定人的提交记录（`-A 1` — After，匹配行的后 1 行;`-B 1` — Before，匹配行的前 1 行）
- `git rebase --abort` — 放弃 rebase 操作，回到原始状态

## 3、回退

- `git reflog` — 查看所有提交记录（包括已回退的）
- `git reset --hard HEAD{25}` — 将 HEAD 重置到某次提交
- `git push --force-with-lease` — 强制推送到远程仓库（比 `--force` 更安全）

## 4、merge 冲突

- `git pull origin dev` — 拉取远程分支
- `git merge --abort` — 冲突后不想合并了，回到 pull 之前的状态

## 5、删除分支

- `git branch -D dev-cmr` — 强制删除本地分支
- `git push origin --delete dev-cmr` — 删除远程分支
- `git branch dev-cmr` — 重新创建本地分支
- `git checkout dev-cmr` — 切换到该分支
- `git push --set-upstream origin dev-cmr` — 推送并关联远程分支

## 6、上一次 commit 未 push，如何回退

- `git reset --soft HEAD~1` — 撤销最近一次提交，保留修改内容到暂存区

## 7、worktree

- `git worktree list` — 列出所有 worktree
- `git worktree add <path> <branch>` — 添加 worktree
- `git worktree remove <path>` — 删除 worktree
- `git worktree prune` — 清理过期的 worktree 信息

## 8、其他

- `gitk` 命令还未生效：`brew install git-gui`

## 合并 dev 分支代码到 dev-mingrenchen

- `git checkout dev-mingrenchen`
- `git fetch origin dev`
- `git merge origin/dev`
- 解决冲突后：`git add <file>`
- `git commit`
- `git push origin dev-mingrenchen`

## 将当前分支main-cmr和main分支对齐

- 场景：提交main-cmr的mr时发现当前分支上有之前提交的内容A（这个内容已经通过dev分支合并到main分支了），这个时候没必要再次将A提交一次

```bash
git pull origin main
git reset --hard origin/main
git push --force-with-lease
git cherry-pick commitID
git push
```
