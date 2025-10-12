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





## ssh连接

  ```shell
ssh-keygen -t rsa -b 4096 -C "your_example@example.com"
# -t rsa 为密匙生成算法
#-b 4096 为密匙长度位数

Enter file in which to save the key (/your_home/.ssh/id_rsa):

enter passphrase(empty for no pw):
#找到密匙在	C:/Users/Username/.ssh/id_rsa

id_rsa私钥
id_rsa.pub:公钥
cat ~/.ssh/id_rsa.pub
#在github->settings->newssh->add
ssh -T git@github.com #检测，第一次链接，输入yes
  ```

1. 这时候输入`git remote -v`输出

   ```
   origin https://github.com/username/repository.git(fetch)
   origin https://github.con/username/reposigoty.git(push)
   ```

   ```shell
   git remote set-url origin git@github.com:username/repository.git
   ##更改远程URL为ssh
   ```

2. 验证`git remote -v`输出

   ```shell
   origin git@github.com:username/repository.git(fetch)
   origin git@github.com:username/repository.git(push)
   ```

   ```
   git pull origin main
   git push origin main
   git clone git@github.com:username/repository.git
   ```

   