# 回滚代码

## reset 重置代码到某次提交

- 回退代码到`commitId`提交时的状态
- 工作区、暂存区以及`commitId`后面提交的内容将会被完全清除，包括提交记录

  ```bash
  git log # 查看提交ID
  git reset --hard 'commitId'
  git push -f # 强制推送
  ```

## revert 回滚某次提交

- `revert`会产生新的`commit`记录，是通过一次新的`commit`来恢复到之前旧的`commit`
- `revert`会保留`恢复的该次提交`后面的其他提交内容，假如后面的提交与要恢复的提交更改了同一个地方，此时用 revert 会产生冲突

  ```bash
  git log # 查看提交ID
  git revert 'commitId'
      # 若冲突，打开冲突文件，手动解决冲突
      # git add 冲突的文件
      # git revert --continue
      # git commit -m 'resolve conflicts'
  git push
  ```

## commit 后还未 push，如何撤回 commit?

- `git reset --soft HEAD~1` 撤销最近的提交，保留工作区和暂存区的内容【`HEAD~1`表示上一个提交】
- `git reset --mixed HEAD~1` 撤销最近的提交，并且重置暂存区，但保留工作区的内容
- `git reset --hard HEAD~1` 撤销最近的提交，并且重置工作区和暂存区【注意：会丢失未提交的改动】
