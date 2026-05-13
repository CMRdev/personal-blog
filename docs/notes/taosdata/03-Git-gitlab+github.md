# 在 gitlab 和 github 同时开发

1. 配置自己的 `ssh public key` 到 `gitlab https://git.tdengine.net/rd-public/idmp`。

2. 在 gitlab idmp创建自己的分支 main-xx 和 dev-xx，并推送到远程。

3. 在 github 的 TDasset 本地仓库里面增加 gitlab 为新远程仓库。

```bash
cd TDasset
# 添加 GitLab 为新的远程仓库，别名为 "gitlab"
git remote add gitlab git@git.tdengine.net:rd-public/idmp.git
# 从 GitHub（origin）拉取所有分支信息
git fetch origin
# 从 GitLab（gitlab）拉取所有分支信息
git fetch gitlab
```

4. 在 TDasset 仓库下pull 自己 main-xx 分支最新代码，创建新的分支

```bash
gitlab-main-xx。
git checkout main-xx
git pull
# 基于远程分支 "gitlab/main" 创建新本地分支 "gitlab-main-xx"
git checkout -b gitlab-main-xx gitlab/main
# 把 main-xx 的改动合并到 gitlab-main-xx
git merge main-xx
```

5. 提交 gitlab-main-xx 到gitlab 的 main-xx。

```bash
# 把本地分支 "gitlab-main-xx" 推送到 GitLab 的 "main-xx"
# 格式：git push <远程名> <本地分支>:<远程分支>
git push gitlab gitlab-main-xx:main-xx
```

6. 在 gitlab 和 github 同时提交 pr 跑 CI。

7. dev 分支同上面流程，只是 main 换成 dev。

8. 迁移完成后，修改本地分支的上游跟踪

```bash
git branch --set-upstream-to=gitlab/dev-cmr gitlab-dev-cmr
```
