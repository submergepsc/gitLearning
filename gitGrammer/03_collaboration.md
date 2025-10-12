# 远程协作与同步命令

## 远程仓库管理
- `git remote`：查看已配置的远程仓库列表。
- `git remote -v`：查看远程仓库与对应的抓取、推送地址。
- `git remote add <名称> <地址>`：添加新的远程仓库。
- `git remote rename <旧名称> <新名称>`：重命名远程仓库别名。
- `git remote remove <名称>`：移除远程仓库。

## 抓取与拉取
- `git fetch [<远程>] [<分支>]`：从远程获取更新但不合并。
- `git pull`：抓取远程更新并自动合并到当前分支。
- `git pull --rebase`：抓取更新后使用变基避免额外合并提交。
- `git fetch --prune`：清理远程已删除的分支引用。

## 推送
- `git push [<远程>] [<分支>]`：将当前分支推送到远程。
- `git push -u <远程> <分支>`：推送并设置上游，便于后续直接使用 `git push`/`git pull`。
- `git push --force-with-lease`：在确认远程没有其他人更新的情况下强制推送。
- `git push --tags`：推送所有本地标签。

## 标签管理
- `git tag`：列出所有标签。
- `git tag <标签名>`：在当前提交创建轻量标签。
- `git tag -a <标签名> -m "<说明>"`：创建带注释的标签。
- `git show <标签>`：查看标签指向的提交与说明。
- `git push <远程> <标签>`：推送指定标签到远程。
- `git push <远程> --tags`：一次性推送所有标签。
- `git tag -d <标签>`：删除本地标签。
- `git push <远程> :refs/tags/<标签>`：删除远程标签。

## 协作最佳实践
- 在推送前使用 `git pull --rebase` 同步远程提交，减少冲突。
- 使用 `git status` 确认工作区干净，再进行推送或合并。
- 使用分支（feature/hotfix/release）管理不同工作流。
- 编写清晰的提交信息，方便团队追踪历史。
