# Git 基础命令

## 初始化与配置
- `git init [<目录>]`：在当前目录或指定目录初始化一个新的 Git 仓库。
- `git clone <仓库地址> [<目录>]`：克隆远程仓库到本地。
- `git config --global user.name "<姓名>"`：设置全局用户名。
- `git config --global user.email "<邮箱>"`：设置全局邮箱。
- `git config --list`：查看所有 Git 配置。

## 查看状态与历史
- `git status [-sb]`：查看当前工作区与暂存区状态，`-sb` 提供简洁视图。
- `git log [--oneline] [--graph] [--decorate]`：查看提交历史，常配合选项获得紧凑视图或图形化分支结构。
- `git show <提交>`：查看指定提交的详细信息（内容、作者、时间等）。
- `git diff [<提交A> <提交B>]`：比较工作区、暂存区或任意两个提交之间的差异。

## 添加与提交
- `git add <文件>`：将指定文件的更改加入暂存区。
- `git add -A`：一次性将所有修改（包含删除和新增）加入暂存区。
- `git commit`：打开编辑器撰写提交信息并提交暂存区的更改。
- `git commit -m "<信息>"`：以单行信息快速提交。
- `git commit --amend [--no-edit]`：修正最近一次提交，可添加新更改或修改提交信息。

## 撤销与回滚
- `git restore <文件>`：还原工作区文件到最近一次暂存或提交状态。
- `git restore --staged <文件>`：将暂存区中的文件移除暂存，保留在工作区。
- `git reset --soft <提交>`：将当前分支指向旧提交，保留暂存和工作区。
- `git reset --mixed <提交>`（默认）：保留工作区，将暂存区重置到指定提交。
- `git reset --hard <提交>`：彻底重置到指定提交，工作区和暂存区的修改都会被丢弃。
- `git revert <提交>`：创建一个新的“反向提交”来撤销历史提交，保持历史线性。

## 忽略文件
- `echo <模式> >> .gitignore`：向忽略文件中追加模式。
- `git rm -r --cached <路径>`：停止跟踪已经提交的文件或目录，使其遵循 `.gitignore` 规则。
