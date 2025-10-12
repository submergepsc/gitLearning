# 进阶与排错命令

## 暂存工作
- `git stash`：暂存当前未提交的修改（包括暂存区和工作区）。
- `git stash save "<说明>"`：以说明信息保存当前修改。
- `git stash list`：查看暂存栈中的记录。
- `git stash show [-p] [<stash>]`：查看暂存条目的变更摘要或详情。
- `git stash apply [<stash>]`：应用指定暂存但保留在栈中。
- `git stash pop [<stash>]`：应用并移除指定暂存。
- `git stash drop <stash>`：删除指定暂存。
- `git stash clear`：清空全部暂存条目。

## 诊断与清理
- `git status --ignored`：连同被忽略文件一起显示状态。
- `git clean -n`：预览将被清理的未跟踪文件/目录。
- `git clean -fd`：强制删除未跟踪的文件和目录。
- `git fsck`：检查仓库对象数据库的完整性。
- `git gc --prune=now --aggressive`：对仓库进行垃圾回收和压缩。
- `git bisect start`：开始二分查找，用于定位引入 bug 的提交。
- `git bisect good <提交>` / `git bisect bad <提交>`：标记已知好/坏的提交。
- `git bisect run <命令>`：自动化二分查找过程。

## 子模块与子树
- `git submodule add <仓库> [<路径>]`：添加子模块。
- `git submodule update --init --recursive`：初始化并更新所有子模块。
- `git submodule status`：查看子模块状态。
- `git subtree add --prefix=<目录> <远程> <分支>`：以子树方式引入外部仓库。
- `git subtree pull --prefix=<目录> <远程> <分支>`：同步子树的更新。

## 钩子与自动化
- `hooks` 目录位于 `.git/hooks/` 中，可加入 shell、Python 等脚本。
- 常见钩子：
  - `pre-commit`：提交前执行，常用于运行测试或格式化代码。
  - `commit-msg`：校验提交信息格式。
  - `pre-push`：推送前执行，适合运行最后检查。
- 复制示例钩子：`cp .git/hooks/pre-commit.sample .git/hooks/pre-commit && chmod +x .git/hooks/pre-commit`

## 常见排错思路
- 先使用 `git status` 和 `git log` 明确当前状态与历史。
- 如果误删提交，使用 `git reflog` 查找丢失的引用并恢复。
- 使用 `git blame <文件>` 定位每行代码的最后修改者。
- 借助 `git diff --stat` 快速查看变更范围。
- 发生冲突时保留备份，可通过 `git stash` 或临时分支保存现场。
