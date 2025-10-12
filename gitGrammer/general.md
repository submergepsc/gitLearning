# Git 远程协作命令大全

> 本文专注于远程仓库相关操作，覆盖远程地址管理、抓取与同步、推送、追踪分支、标签与子模块同步等常见场景，帮助你高效维护本地与远程的版本一致性。

## 1. 远程仓库管理

### 1.1 查看与维护远程列表
```bash
git remote                     # 列出已配置远程名称
git remote -v                  # 列出远程及其 fetch/push 地址
git remote show origin         # 查看远程分支、跟踪关系与抓取策略
git remote rename origin upstream   # 远程重命名
git remote remove upstream          # 删除远程（慎用）
```

### 1.2 添加与修改远程地址
```bash
git remote add origin https://github.com/owner/repo.git
git remote set-url origin git@github.com:owner/repo.git         # 修改远程 URL
git remote set-url --add origin git@github.com:owner/repo.git   # 为 push 添加额外 URL（镜像场景）
git remote set-url --delete origin https://github.com/owner/repo.git
```

### 1.3 配置 fetch/push 行为
```bash
git config remote.origin.fetch "+refs/heads/*:refs/remotes/origin/*"   # 设置默认抓取引用
git config remote.origin.push   "+refs/heads/main:refs/heads/main"       # 限制 push 范围
git remote set-head origin --auto                                  # 自动跟踪远程默认分支
git remote update                                                   # 更新所有远程引用
```

## 2. 抓取与同步

### 2.1 基本抓取
```bash
git fetch origin                  # 抓取远程更新但不合并
git fetch --all                    # 抓取所有远程
git fetch --prune origin           # 同步删除远程已删除分支
git fetch origin main:main-backup  # 将远程 main 抓取到本地 main-backup 分支
```

### 2.2 跟踪远程分支
```bash
git branch -vv                         # 查看本地分支跟踪状态
git branch --track feature origin/feature   # 建立跟踪分支
git checkout --track origin/feature        # 直接检出远程分支
git branch --unset-upstream               # 取消跟踪关系
```

### 2.3 合并远程更新
```bash
git pull origin main                 # 抓取并合并
git pull --rebase origin main        # 变基远程更新，保持线性历史
git pull --ff-only                   # 仅允许 fast-forward 合并
git pull --autostash                 # 拉取前自动 stash 工作目录改动
```

## 3. 推送与发布

### 3.1 基本推送
```bash
git push origin main                     # 推送 main 分支
git push -u origin feature/my-branch      # 推送并建立跟踪关系
git push origin --force-with-lease        # 带保护的强制推送
git push origin --delete feature/old      # 删除远程分支
git push origin HEAD                      # 推送当前 HEAD 到远程跟踪分支
```

### 3.2 高级推送技巧
```bash
git push origin main:refs/heads/staging   # 推送到远程不同名称分支
git push origin --set-upstream main       # 为已有分支补建跟踪关系
git push origin --atomic main feature/foo # 多分支原子推送
git push --mirror origin                  # 镜像推送所有引用（慎用）
```

### 3.3 标签推送
```bash
git push origin v1.0.0             # 推送单个标签
git push origin --tags             # 推送所有标签
git push origin :refs/tags/v1.0.0  # 删除远程标签
```

## 4. 远程引用与检索

### 4.1 查阅远程信息
```bash
git ls-remote origin                   # 查看远程引用及其哈希
git ls-remote --tags origin             # 仅查看标签引用
git ls-remote --heads origin            # 仅查看分支引用
git remote show origin                  # 总览远程跟踪状态
```

### 4.2 远程分支检索与比较
```bash
git diff origin/main..origin/develop    # 比较远程分支差异
git log origin/main..HEAD                # 查看本地与远程差异提交
git log HEAD..origin/main                # 查看远程领先的提交
git cherry -v origin/main                # 列出本地独有的提交
```

## 5. Fork 与多远程协作

### 5.1 典型远程设置
```bash
git remote add origin git@github.com:yourname/repo.git
git remote add upstream https://github.com/owner/repo.git
```

### 5.2 同步上游更新
```bash
git fetch upstream
git rebase upstream/main             # 或 git merge upstream/main

git push origin main                 # 更新 fork 的 main
```

### 5.3 在 fork 中提交流程
```bash
git checkout -b feature/topic
git push -u origin feature/topic     # 推送到自己 fork
# 在 GitHub 上从 origin/feature/topic 向 upstream/main 创建 PR
```

## 6. 子模块与子树远程同步

### 6.1 子模块
```bash
git submodule add https://github.com/owner/lib.git libs/lib
git submodule update --init --recursive           # 初始化并拉取
git submodule update --remote --merge             # 跟踪上游并合并
git push origin --recurse-submodules=on-demand    # 推送父仓库时按需推送子模块
```

### 6.2 子树
```bash
git subtree add --prefix=libs/lib https://github.com/owner/lib.git main
git subtree pull --prefix=libs/lib https://github.com/owner/lib.git main
```

## 7. 常见故障排查

```bash
git remote prune origin                # 清理已失效的远程引用
git config credential.helper store     # 持久保存凭据
git credential-cache exit              # 清空凭据缓存
git config --global http.postBuffer 524288000   # 调整大仓库推送缓冲
git push --no-verify                   # 跳过 pre-push 钩子（慎用）
git push origin HEAD:refs/for/main     # 提交到 Gerrit 审核分支
```

> 提示：涉及强制推送或镜像操作前务必确认团队约定，避免误删远程历史。
