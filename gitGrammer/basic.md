# git远程操作

## 远程	

```shell
git init 
git clone <repository_url>
cd <directory>
git add.
git add <file_name>
git diff (+commit id)
git commit -m "some_message"
git commit -a

git log#修改日志
git checkout -- <file_name>#撤销工作区的修改
git reset HEAD <file_name>#暂存区修改


##分支操作
git branch -a/-r #所有，本地，远程
git checkout <branch_name>
git checkout -b <branch_name>#创建并修改
git branch -d/-D <branch_name>#删除


##远程分支仓库操作
git remote -v
git remote 
git remote remove <remote_name>#删除远程仓库
git remote set-url  <remote_name> <new_repository_url>

##远程操作
git remote add <remote_name> <repository_url>
git pull <remote_name> <branch_name>#拉取并合并
git push <remote_name> <branch_name>
git push <remote_name> -delete <branch_name> #delete remote branch
git fetch <remote_name> <branch_name> #拉取更新，但不合并
git merge <remote_name>/<branch_name>#手动合并


#addition
git status 
git config --global user.name
git config --global user.email
git config --global user.name "your_name"
git config --global user.email "your_email@example.com"

#sometimes use'q' to quit (end)
```

