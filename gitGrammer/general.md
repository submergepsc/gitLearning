# Git 远程协作常用命令

> 本指南聚焦日常远程仓库协作中最常用、最实用的命令，覆盖远程地址管理、抓取同步、推送发布、Fork 协作以及基础排错。

## 1. 远程仓库管理

### 1.1 查看远程信息
```bash
git remote -v                 # 列出远程名称与对应 URL
git remote show origin        # 了解跟踪分支、抓取策略等详情
```

### 1.2 添加或修改远程
```bash
git remote add origin https://github.com/owner/repo.git
# 若改用 SSH，可调整远程地址
git remote set-url origin git@github.com:owner/repo.git
```

### 1.3 同步远程引用
```bash
git remote update             # 更新所有远程的引用信息
git remote prune origin       # 清理远程已删除的分支引用
```

## 2. 抓取与同步

### 2.1 拉取远程更新
```bash
git fetch origin              # 获取远程最新提交，不修改工作区
git fetch --prune origin      # 抓取并同步删除远程已删分支
```

### 2.2 跟踪远程分支
```bash
git branch -vv                # 查看本地分支与远程跟踪状态
git checkout --track origin/feature   # 直接检出远程分支并跟踪
git branch --set-upstream-to=origin/main main   # 为已有分支建立跟踪关系
```

### 2.3 合并远程更新
```bash
git pull origin main          # 抓取并合并远程 main
git pull --rebase origin main # 以变基方式同步远程，保持线性历史
```

## 3. 推送与发布

### 3.1 推送分支
```bash
git push origin main          # 推送本地 main 到远程
```

### 3.2 推送并建立跟踪
```bash
git push -u origin feature/login   # 推送新分支并建立跟踪
```

### 3.3 安全处理历史重写
```bash
git push origin --force-with-lease  # 强制推送但确保不覆盖他人更新
```

### 3.4 标签发布
```bash
git push origin v1.0.0        # 推送单个标签
git push origin --tags        # 推送当前仓库的所有标签
```

## 4. Fork 多远程协作

### 4.1 典型远程配置
```bash
git remote add origin git@github.com:yourname/repo.git
git remote add upstream https://github.com/owner/repo.git
```

### 4.2 同步上游与提交 PR
```bash
git fetch upstream
git rebase upstream/main          # 或使用 git merge upstream/main

git push origin main              # 推送更新后的 main 到自己的 fork
git push -u origin feature/topic  # 推送功能分支并在 GitHub 上发起 PR
```

## 5. 常见远程问题排查
```bash
git status                       # 首先确认本地状态是否干净
git branch -r                    # 查看远程分支列表是否更新
git config credential.helper store  # 持久化凭据，避免频繁输入账号
```

> 提示：进行强制推送或修改远程设置前，请与团队确认，避免造成历史丢失或冲突。
