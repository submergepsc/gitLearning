# 分支与合并命令

## 分支管理
- `git branch`：列出本地分支，当前分支前有 `*` 标记。
- `git branch -a`：显示本地和远程跟踪分支。
- `git branch <分支名>`：基于当前提交创建新分支。
- `git branch -d <分支名>`：删除已经合并的分支。
- `git branch -D <分支名>`：强制删除未合并的分支。
- `git branch -m <旧名> <新名>`：重命名分支。

## 切换与检出
- `git checkout <分支>`：切换到指定分支。
- `git checkout -b <分支>`：创建并切换到新分支。
- `git switch <分支>`：切换分支的现代替代命令。
- `git switch -c <分支>`：创建并切换到新分支。
- `git switch -`：快速返回上一个分支。

## 合并与重写历史
- `git merge <分支>`：将指定分支合并到当前分支。
- `git merge --no-ff <分支>`：强制生成合并提交，保留分支历史。
- `git merge --squash <分支>`：将分支提交压缩为单个提交合并。
- `git rebase <基准分支>`：将当前分支的提交基于目标分支重新播放。
- `git rebase -i <基准分支>`：交互式变基，可重排、合并或删除提交。
- `git cherry-pick <提交>`：将指定提交的更改应用到当前分支。

## 解决冲突
- `git status`：查看冲突文件列表。
- `git diff`：查看冲突细节。
- 编辑冲突文件：手动保留需要的内容并删除冲突标记。
- `git add <文件>`：解决冲突后将文件重新加入暂存。
- `git merge --continue` / `git rebase --continue`：继续合并或变基流程。
- `git merge --abort` / `git rebase --abort`：放弃当前合并或变基操作。
