# 进阶与排错命令

## 暂存工作
- `git stash`：暂存当前未提交的修改（包括暂存区和工作区）。
- `git stash push -m "<说明>"`：以说明信息保存当前修改，替代旧版 `save`。
- `git stash push -u`：同时暂存未跟踪文件。
- `git stash push -a`：暂存未跟踪与忽略的文件。
- `git stash list`：查看暂存栈中的记录。
- `git stash show [-p] [<stash>]`：查看暂存条目的变更摘要或详情。
- `git stash apply [<stash>]`：应用指定暂存但保留在栈中。
- `git stash pop [<stash>]`：应用并移除指定暂存。
- `git stash drop <stash>`：删除指定暂存。
- `git stash clear`：清空全部暂存条目。
- `git stash branch <分支> [<stash>]`：基于暂存内容快速创建新分支继续工作。

## 诊断与清理
- `git status --ignored`：连同被忽略文件一起显示状态。
- `git clean -n`：预览将被清理的未跟踪文件/目录。
- `git clean -fd`：强制删除未跟踪的文件和目录。
- `git clean -fdx`：连同忽略文件一并清理（慎用）。
- `git fsck`：检查仓库对象数据库的完整性。
- `git gc --prune=now --aggressive`：对仓库进行垃圾回收和压缩。
- `git count-objects -v`：统计对象数量、磁盘占用等信息。
- `git bisect start`：开始二分查找，用于定位引入 bug 的提交。
- `git bisect good <提交>` / `git bisect bad <提交>`：标记已知好/坏的提交。
- `git bisect run <命令>`：自动化二分查找过程。

## Reflog 与恢复
- `git reflog`：查看 HEAD、分支、标签引用的移动历史。
- `git reflog show <引用>`：查看特定引用的 reflog 记录。
- `git reset --hard HEAD@{<序号>}`：回到某个 reflog 记录指向的状态。
- `git merge --abort` / `git rebase --abort`：在异常操作时快速回滚。
- `git fsck --lost-found`：查找孤立对象并尝试恢复。

## 子模块与子树
- `git submodule add <仓库> [<路径>]`：添加子模块。
- `git submodule update --init --recursive`：初始化并更新所有子模块。
- `git submodule status`：查看子模块状态。
- `git submodule foreach '<命令>'`：在每个子模块中批量执行命令。
- `git subtree add --prefix=<目录> <远程> <分支>`：以子树方式引入外部仓库。
- `git subtree pull --prefix=<目录> <远程> <分支>`：同步子树的更新。
- `git subtree split --prefix=<目录> --branch <分支>`：将子树内容拆分为独立分支。

## 钩子与自动化
- `hooks` 目录位于 `.git/hooks/` 中，可加入 shell、Python 等脚本。
- 常见钩子：
  - `pre-commit`：提交前执行，常用于运行测试或格式化代码。
  - `prepare-commit-msg`：在提交信息编辑器打开前自动补充信息。
  - `commit-msg`：校验提交信息格式。
  - `pre-push`：推送前执行，适合运行最后检查。
- 复制示例钩子：`cp .git/hooks/pre-commit.sample .git/hooks/pre-commit && chmod +x .git/hooks/pre-commit`
- 在团队项目中，将钩子脚本放入仓库并通过 `core.hooksPath` 指向共享目录。

## 签名与安全
- `git config --global user.signingkey <GPG Key ID>`：设置默认 GPG 签名密钥。
- `git commit -S -m "<信息>"`：创建带 GPG 签名的提交。
- `git tag -s <标签名> -m "<说明>"`：为标签添加 GPG 签名。
- `git verify-commit <提交>` / `git verify-tag <标签>`：验证签名有效性。
- `git config --global commit.gpgsign true`：默认对所有提交进行签名。

## 常见排错思路
- 先使用 `git status`、`git branch -vv` 和 `git log --graph` 明确当前状态与历史。
- 如果误删提交，使用 `git reflog`、`git fsck --lost-found` 查找丢失的引用并恢复。
- 使用 `git blame <文件>` 定位每行代码的最后修改者。
- 借助 `git diff --stat` 或 `git log --stat` 快速查看变更范围。
- 发生冲突时保留备份，可通过 `git stash` 或临时分支保存现场。
- 遇到复杂合并/变基问题时，可使用 `git rerere` 复用曾经的冲突解决方案。
