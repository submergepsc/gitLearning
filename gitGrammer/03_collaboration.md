# 远程协作与同步命令

## 远程仓库管理
- `git remote`：查看已配置的远程仓库列表。
- `git remote -v`：查看远程仓库与对应的抓取、推送地址。
- `git remote show <名称>`：查看远程仓库的详细信息（跟踪分支、抓取策略等）。
- `git remote add <名称> <地址>`：添加新的远程仓库。
- `git remote rename <旧名称> <新名称>`：重命名远程仓库别名。
- `git remote remove <名称>`：移除远程仓库。
- `git remote set-url <名称> <地址>`：修改远程仓库地址。
- `git remote update [<名称>]`：抓取全部远程的最新引用。
- `git remote prune <名称>`：删除已经在远程移除的引用。

## 抓取与拉取
- `git fetch [<远程>] [<分支>]`：从远程获取更新但不合并。
- `git fetch --all --prune`：获取所有远程更新并清理无效引用。
- `git fetch <远程> <引用说明>`：抓取特定分支、标签或自定义 refspec。
- `git pull`：抓取远程更新并自动合并到当前分支。
- `git pull --ff-only`：仅在可以快进时合并，防止产生额外合并提交。
- `git pull --rebase[=merges]`：抓取更新后使用变基（可保留合并历史）。
- `git pull --recurse-submodules`：拉取时同步更新子模块。

## 推送
- `git push [<远程>] [<分支>]`：将当前分支推送到远程。
- `git push -u <远程> <分支>`：推送并设置上游，便于后续直接使用 `git push`/`git pull`。
- `git push --set-upstream <远程> <分支>`：等价于 `-u`，用于首次推送新分支。
- `git push <远程> <本地分支>:<远程分支>`：将本地分支映射到不同的远程分支名称。
- `git push --force-with-lease`：在确认远程没有其他人更新的情况下安全地强制推送。
- `git push --force`：无条件强制推送（需谨慎）。
- `git push --follow-tags`：推送分支时同时推送与新提交关联的标签。
- `git push --tags`：推送所有本地标签。

## 标签管理
- `git tag`：列出所有标签。
- `git tag <标签名>`：在当前提交创建轻量标签。
- `git tag -a <标签名> -m "<说明>"`：创建带注释的标签。
- `git tag -s <标签名> -m "<说明>"`：使用 GPG 签名标签。
- `git show <标签>`：查看标签指向的提交与说明。
- `git push <远程> <标签>`：推送指定标签到远程。
- `git push <远程> --tags`：一次性推送所有标签。
- `git tag -d <标签>`：删除本地标签。
- `git push <远程> :refs/tags/<标签>`：删除远程标签。

## 协作与代码审查
- `git fetch origin pull/<ID>/head:<分支>`：在本地检出 GitHub PR 对应的提交进行审查。
- `git cherry-pick <提交>`：在审查后提取单独的修复提交到自己的分支。
- `git format-patch <起点>`：将提交导出为补丁文件，便于通过邮件共享。
- `git apply <补丁>`：应用补丁文件中的修改。
- `git request-pull <起点> <远程> <分支>`：生成请求拉取的摘要信息。

## 协作最佳实践
- 在推送前使用 `git pull --rebase` 或 `git fetch` + `git rebase` 同步远程提交，减少冲突。
- 使用 `git status` 确认工作区干净，再进行推送或合并。
- 使用分支（feature/hotfix/release）管理不同工作流，配合保护主干分支。
- 编写清晰的提交信息与 PR 描述，方便团队追踪历史。
- 利用 `git tag`、发布说明和版本号管理生产发布。
