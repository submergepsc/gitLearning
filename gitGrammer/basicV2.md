# git远程操作

## 远程	

```shell
git init 
git clone <repository_url>#clone使用的是url，fetch，pull和merge是远程仓库名
#gitclone会自动创建origin关联（但是ssh没成功）
##注意如果在/codex/大目录下面clone了一个gitLearning仓库，那么在进入gitLearning仓库之后会自动生成一个origin的远程仓库别名
git clone -b main git@github.com:submergepsc/JuniorPT.git

cd <directory>
git add.
git add <file_name>
git diff (+commit id)
git commit -m "some_message"
git commit -a

git log#修改日志
git checkout -- <file_name>#撤销工作区的修改
git reset HEAD <file_name>#暂存区修改


##本地分支操作
git branch -a/-r #所有，本地，远程
git branch <branch_name>#创建分支
git checkout -b <branch_name>#创建并修改
git branch -m master main#改名master->main
git branch -d/-D <branch_name>#删除


##远程分支仓库操作
#只能在github，gitlab，gitee，等上面创建和删除仓库
git remote -v
git remote 
git remote remove <remote_name>#删除远程仓库
#首先创建本地分支git checkout -b feature	
git push origin feature#创建远程分支feature
git push <remote_name> -delete <branch_name> #delete remote branch
git remote set-url  <remote_name> <new_repository_url>#更改远程仓库别名





##远程操作
git remote add <remote_name> <repository_url>
git pull <remote_name> <branch_name>#拉取并合并
git push <remote_name> <branch_name>
git fetch <remote_name> <branch_name> #拉取更新，但不合并，但是必须要远程有新的更新才会拉取，所以还是需要clone下来
git merge <remote_name>/<branch_name>#手动合并


#addition
git status 
git config --global user.name
git config --global user.email
git config --global user.name "your_name"
git config --global user.email "your_email@example.com"

#sometimes use'q' to quit (end)
```



### 其他

```shell
#克隆特定分支
1.
# 格式：git clone -b 分支名 仓库URL
git clone -b develop https://github.com/username/repository.git
2.
#先克隆在切换
git clone https://github.com/username/repository.git
cd  repository
git checkout 目标分支名
#或者使用更规范的
git switch 目标分支名




#远程更改本地怎么同步
git status #检查有没有修改没有提交
#如果输出 nothing to commit, working tree clean，说明工作区干净，可以继续。
git pull origin main#拉取远程代码并合并到当前分支
#origin 是远程仓库的默认别名（可通过 git remote 查看）。
#main 是远程的目标分支（如果你的远程默认分支是 master，则替换为 master）。

#tip
#如果提示 “fatal: refusing to merge unrelated histories”
#如果本地分支和远程分支历史不关联（比如本地是新建仓库，远程已有代码），可添加 --allow-unrelated-histories 强制合并：
git pull origin main --allow-unrelated-histories
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
cat C:/Usres/15056/.ssh/id_rsa.pub
#在github->settings->newssh->add
ssh -T git@github.com #检测，第一次链接，输入yes
  ```

1. 这时候输入`git remote -v`输出

   ```shell
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

   ```shell
   git pull origin main
   git push origin main
   git clone git@github.com:username/repository.git
   ```

   



### tips

`git clone`不仅会下载远程项目，还会自动创建关联

```shell
git clone <repository_url>
#在克隆的目录下面会有origin的远程别名
#此外克隆的时候要使用ssh的地址
```



而`git init`+`git pull`并不会创建关联

```shell
git init
git remote add origin https://github.com/username/repository.git
git pull origin main 
```



此外

```shell
git clone git@github:submergepsc.git：不仅克隆了远程仓库的内容，还会自动将 origin 设置为远程仓库的 URL，并且将本地仓库的默认分支与远程分支关联起来。

git remote add origin git@github:submergepsc.git：仅仅是手动将一个远程仓库地址与本地仓库关联起来，并不会克隆任何内容。适用于你已经有了本地仓库，并希望与远程仓库进行连接的情况。

也就是说，如果使用clone的话会直接克隆仓库，并且创建的origin会在克隆后的本地仓库配置好
但是使用remote add 的话需要在本地仓库内部使用，不然会将整个仓库作为远程仓库的一个目录（理解）
```



tips2

```shell
git pull 会将已经关闭的窗口（但是有远程连接重新建立联系）#git fetch 做不到
```

