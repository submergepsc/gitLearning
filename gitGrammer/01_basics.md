# Git 基础命令

## 初始化与配置
- `git init [<目录>]`：在当前目录或指定目录初始化一个新的 Git 仓库。
- `git clone <仓库地址> [<目录>]`：克隆远程仓库到本地。
- `git config --global user.name "<姓名>"`：设置全局用户名。
- `git config --global user.email "<邮箱>"`：设置全局邮箱。
- `git config --global core.editor "<编辑器>"`：指定默认提交信息编辑器。
- `git config --global init.defaultBranch <分支>`：配置新仓库的默认主分支名称。
- `git config --global alias.<别名> "<命令序列>"`：为常用命令创建别名。
- `git config --system --edit` / `git config --global --edit`：打开系统或全局配置文件进行编辑。
- `git config --list [--show-origin]`：查看所有配置及其来源。

## 查看状态与文件
- `git status [-sb]`：查看当前工作区与暂存区状态，`-sb` 提供精简视图。
- `git status --ignored`：连同被忽略的文件一起显示状态。
- `git ls-files`：列出 Git 正在跟踪的文件。
- `git ls-tree <提交> [<路径>]`：查看指定提交中某路径的文件结构。
- `git cat-file -p <对象>`：查看提交、树或 blob 对象的原始内容。

## 添加与提交
- `git add <文件>`：将指定文件的更改加入暂存区。
- `git add -A` / `git add .`：一次性将所有修改（包含删除和新增）加入暂存区。
- `git add -p [<文件>]`：以交互方式逐块挑选需要暂存的变更。
- `git commit`：打开编辑器撰写提交信息并提交暂存区的更改。
- `git commit -m "<信息>"`：以单行信息快速提交。
- `git commit --amend [--no-edit]`：修正最近一次提交，可添加新更改或修改提交信息。
- `git commit --amend --reset-author`：修正提交的同时更新作者信息。
- `git commit --allow-empty -m "<信息>"`：创建一个空提交，用于标记或触发流程。

## 比较差异
- `git diff`：查看工作区与暂存区的差异。
- `git diff --staged` / `git diff --cached`：查看暂存区与最近一次提交之间的差异。
- `git diff <提交>`：比较工作区与指定提交的差异。
- `git diff <提交A> <提交B>`：比较任意两个提交之间的差异。
- `git diff --stat`：以统计信息展示变更的文件数与增删行数。
- `git difftool`：调用外部 diff 工具查看差异。

## 查看历史
- `git log [--oneline] [--graph] [--decorate]`：查看提交历史，可配合选项获得简洁或图形化视图。
- `git log --stat`：在历史列表中显示各提交影响的文件与增删行数。
- `git log --author="<姓名或邮箱>"`：仅查看特定作者的提交。
- `git log --since="<时间>" --until="<时间>"`：限定时间范围内的提交。
- `git log <路径>`：仅查看某个文件或目录的变更历史。
- `git show <提交>`：查看指定提交的详细信息（内容、作者、时间等）。
- `git blame <文件>`：逐行追踪最后修改的提交与作者。

## 搜索与排查
- `git grep "<关键字>"`：在版本库中搜索关键字。
- `git grep -n "<关键字>" <分支>`：在特定分支中连同行号搜索。
- `git bisect`：二分查找导致缺陷的提交（详见进阶章节）。
- `git reflog`：查看 HEAD 与分支引用的历史移动，找回丢失的提交。

## 撤销与回滚
- `git restore <文件>`：还原工作区文件到最近一次暂存或提交状态。
- `git restore --staged <文件>`：将暂存区中的文件移除暂存，保留在工作区。
- `git reset --soft <提交>`：将当前分支指向旧提交，保留暂存和工作区。
- `git reset --mixed <提交>`（默认）：保留工作区，将暂存区重置到指定提交。
- `git reset --hard <提交>`：彻底重置到指定提交，工作区和暂存区的修改都会被丢弃。
- `git revert <提交>`：创建一个新的“反向提交”来撤销历史提交，保持历史线性。
- `git checkout -- <文件>`：还原单个文件到当前分支的最新提交（Git 2.23 前常用写法）。
- `git restore --source=<提交> <文件>`：从指定提交中还原文件。

## 忽略文件
- `echo <模式> >> .gitignore`：向忽略文件中追加模式。
- `git rm -r --cached <路径>`：停止跟踪已经提交的文件或目录，使其遵循 `.gitignore` 规则。
- `git check-ignore -v <文件>`：查看某个文件为什么会被忽略。
- `git update-index --skip-worktree <文件>`：保留文件本地修改但不再纳入提交（配置型文件常用）。
