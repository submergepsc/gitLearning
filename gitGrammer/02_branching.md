# 分支与合并命令

## 分支管理
- `git branch`：列出本地分支，当前分支前有 `*` 标记。
- `git branch -vv`：显示本地分支及其上游关系和最新提交信息。
- `git branch -a`：显示本地和远程跟踪分支。
- `git branch <分支名>`：基于当前提交创建新分支。
- `git branch <分支名> <起点>`：基于指定提交创建新分支。
- `git branch --set-upstream-to=<远程>/<分支>`：为当前分支设置/调整上游分支。
- `git branch --merged [<分支>]`：列出已经合并到指定分支的分支。
- `git branch --no-merged [<分支>]`：列出尚未合并的分支。
- `git branch --contains <提交>`：列出包含某个提交的分支。
- `git branch -d <分支名>`：删除已经合并的分支。
- `git branch -D <分支名>`：强制删除未合并的分支。
- `git branch -m <旧名> <新名>`：重命名分支。

## 切换与检出
- `git checkout <分支>`：切换到指定分支。
- `git checkout -b <分支>`：创建并切换到新分支。
- `git checkout <提交> -- <文件>`：在不切换分支的情况下查看或恢复历史文件。
- `git switch <分支>`：切换分支的现代替代命令。
- `git switch -c <分支>`：创建并切换到新分支。
- `git switch -c <分支> <起点>`：从指定提交创建并切换到新分支。
- `git switch -`：快速返回上一个分支。
- `git worktree add <目录> <分支>`：在新工作树中检出分支，实现多分支并行开发。

## 合并与重写历史
- `git merge <分支>`：将指定分支合并到当前分支。
- `git merge --ff-only <分支>`：仅在能快进合并时才执行，否则终止。
- `git merge --no-ff <分支>`：强制生成合并提交，保留分支历史。
- `git merge --squash <分支>`：将分支提交压缩为单个提交合并。
- `git merge -X ours/theirs <分支>`：冲突时偏向当前分支或目标分支的内容。
- `git rebase <基准分支>`：将当前分支的提交基于目标分支重新播放。
- `git rebase <新基底> <分支>`：将指定分支变基到新的基底上。
- `git rebase --onto <新基底> <旧基底> <分支>`：仅迁移某段提交到新的基底。
- `git rebase -i <基准分支>`：交互式变基，可重排、合并或删除提交。
- `git rebase --autosquash`：在交互式变基时自动配对 `fixup!/squash!` 提交。
- `git cherry-pick <提交>`：将指定提交的更改应用到当前分支。
- `git cherry-pick -n <提交>`：应用提交但不立即创建新提交，方便合并多个更改。
- `git cherry-pick --abort`：在拣选过程中放弃操作。

## 解决冲突
- `git status`：查看冲突文件列表。
- `git diff`：查看冲突细节。
- `git diff --name-only --diff-filter=U`：快速列出存在冲突的文件。
- 编辑冲突文件：手动保留需要的内容并删除冲突标记。
- `git add <文件>`：解决冲突后将文件重新加入暂存。
- `git merge --continue` / `git rebase --continue`：继续合并或变基流程。
- `git merge --abort` / `git rebase --abort`：放弃当前合并或变基操作。
- `git rerere status`：查看自动记录的冲突解决方案（需开启 `rerere`）。
- `git rerere enable`：启用重复冲突自动记忆功能。
