# 大厂研发常用 Git 命令手册

这份手册按“先速查、后解释”的方式组织。每章上半部分列出常用命令并在行尾说明功能，下半部分逐条解释使用场景。

## 0. Git 的基本模型

```text
工作区 -> 暂存区 -> 本地仓库 -> 远程仓库
          git add    git commit   git push
远程仓库 -> 本地远程追踪记录：git fetch
本地分支 + origin/main -> 合并：git merge / git rebase
```

- 工作区：你正在编辑的文件。
- 暂存区：下一次提交准备包含的内容。
- 本地仓库：已经 commit 的历史。
- 远程仓库：GitHub、Gitee 等服务器上的仓库。
- `origin`：远程地址的本地别名。
- `origin/main`：本地保存的远程 `main` 最新已知状态。

## 1. 配置和创建

### 常用命令

```bash
git config --global user.name "Your Name"       # 设置全局提交作者姓名
git config --global user.email "you@example.com" # 设置全局提交作者邮箱
git config --global --list                       # 查看全局配置
git init                                         # 在当前目录创建 Git 仓库
git init -b main                                 # 创建仓库并指定初始分支
git clone <url>                                  # 克隆远程仓库
git clone -b develop <url>                      # 克隆后切换到指定分支
git clone --depth 1 <url>                        # 只克隆最近历史
```

### 逐条解释

#### `git config --global user.name "Your Name"`

作用：这条命令的核心作用是：设置全局提交作者姓名。

什么时候用：新电脑、新仓库或排查提交身份异常时使用。

注意：`--global` 影响当前用户所有仓库；不加 `--global` 通常只影响当前仓库。

#### `git config --global user.email "you@example.com"`

作用：这条命令的核心作用是：设置全局提交作者邮箱。

什么时候用：新电脑、新仓库或排查提交身份异常时使用。

注意：`--global` 影响当前用户所有仓库；不加 `--global` 通常只影响当前仓库。

#### `git config --global --list`

作用：这条命令的核心作用是：查看全局配置。

什么时候用：新电脑、新仓库或排查提交身份异常时使用。

注意：`--global` 影响当前用户所有仓库；不加 `--global` 通常只影响当前仓库。

#### `git init`

作用：这条命令的核心作用是：在当前目录创建 Git 仓库。

什么时候用：从一个普通文件夹开始创建新仓库时使用。

注意：不要在已经包含 Git 仓库的外层目录乱执行，避免嵌套仓库。

#### `git init -b main`

作用：这条命令的核心作用是：创建仓库并指定初始分支。

什么时候用：从一个普通文件夹开始创建新仓库时使用。

注意：不要在已经包含 Git 仓库的外层目录乱执行，避免嵌套仓库。

#### `git clone <url>`

作用：这条命令的核心作用是：克隆远程仓库。

什么时候用：第一次把远程仓库拿到本机时使用。

注意：克隆后通常会自动生成 `origin` remote 和默认分支的 upstream。

#### `git clone -b develop <url>`

作用：这条命令的核心作用是：克隆后切换到指定分支。

什么时候用：第一次把远程仓库拿到本机时使用。

注意：克隆后通常会自动生成 `origin` remote 和默认分支的 upstream。

#### `git clone --depth 1 <url>`

作用：这条命令的核心作用是：只克隆最近历史。

什么时候用：第一次把远程仓库拿到本机时使用。

注意：克隆后通常会自动生成 `origin` remote 和默认分支的 upstream。

## 2. 查看状态和历史

### 常用命令

```bash
git status                                      # 查看当前状态
git status --short                              # 用紧凑格式查看状态
git log                                         # 查看完整提交历史
git log --oneline --graph --decorate --all      # 用短格式查看所有分支图
git log -n 10                                   # 只查看最近 10 条提交
git show HEAD                                   # 查看当前提交详情
git blame <file>                                # 查看每一行最后由谁修改
git reflog                                      # 查看本地指针移动记录
```

### 逐条解释

#### `git status`

作用：这条命令的核心作用是：查看当前状态。

什么时候用：任何 Git 操作前后都可以使用，尤其是不知道当前仓库发生了什么时。

注意：它只查看状态，不会修改文件。

#### `git status --short`

作用：这条命令的核心作用是：用紧凑格式查看状态。

什么时候用：任何 Git 操作前后都可以使用，尤其是不知道当前仓库发生了什么时。

注意：它只查看状态，不会修改文件。

#### `git log`

作用：这条命令的核心作用是：查看完整提交历史。

什么时候用：当你需要。执行前如果不确定，先用 git status 看当前状态。

注意：注意目标分支、文件名或提交号要写对；涉及删除、覆盖、强推的命令要先确认。

#### `git log --oneline --graph --decorate --all`

作用：这条命令的核心作用是：用短格式查看所有分支图。

什么时候用：当你需要。执行前如果不确定，先用 git status 看当前状态。

注意：注意目标分支、文件名或提交号要写对；涉及删除、覆盖、强推的命令要先确认。

#### `git log -n 10`

作用：这条命令的核心作用是：只查看最近 10 条提交。

什么时候用：当你需要。执行前如果不确定，先用 git status 看当前状态。

注意：注意目标分支、文件名或提交号要写对；涉及删除、覆盖、强推的命令要先确认。

#### `git show HEAD`

作用：这条命令的核心作用是：查看当前提交详情。

什么时候用：想看某个提交或标签具体内容时使用。

注意：可以把 `HEAD` 换成提交哈希、分支名或标签名。

#### `git blame <file>`

作用：这条命令的核心作用是：查看每一行最后由谁修改。

什么时候用：想追踪某行代码最后一次是谁在什么提交里修改时使用。

注意：它是找上下文的工具，不是开发协作里的甩锅工具。

#### `git reflog`

作用：这条命令的核心作用是：查看本地指针移动记录。

什么时候用：误删、误 reset、误 rebase 后想找回旧位置时使用。

注意：reflog 是本地记录，不等同于远程历史。

## 3. 查看差异、暂存和提交

### 常用命令

```bash
git diff                                       # 查看未暂存修改
git diff --cached                              # 查看已暂存修改
git diff HEAD                                  # 查看相对最近提交的全部修改
git add <file>                                 # 暂存指定文件
git add .                                      # 暂存当前目录修改
git add -A                                     # 暂存整个仓库新增、修改和删除
git add -p                                     # 交互式选择部分修改
git commit -m "feat: add login"               # 创建提交
git commit --amend --no-edit                   # 修改最近提交但保留说明
```

### 逐条解释

#### `git diff`

作用：这条命令的核心作用是：查看未暂存修改。

什么时候用：提交前、恢复前、解决冲突前，用来确认具体改动。

注意：`--cached` 看暂存区；不加参数主要看工作区未暂存内容。

#### `git diff --cached`

作用：这条命令的核心作用是：查看已暂存修改。

什么时候用：提交前、恢复前、解决冲突前，用来确认具体改动。

注意：`--cached` 看暂存区；不加参数主要看工作区未暂存内容。

#### `git diff HEAD`

作用：这条命令的核心作用是：查看相对最近提交的全部修改。

什么时候用：提交前、恢复前、解决冲突前，用来确认具体改动。

注意：`--cached` 看暂存区；不加参数主要看工作区未暂存内容。

#### `git add <file>`

作用：这条命令的核心作用是：暂存指定文件。

什么时候用：准备把修改放进下一次提交时使用。

注意：`git add .` 会加入当前目录下大量修改，执行前先看 `git status`。

#### `git add .`

作用：这条命令的核心作用是：暂存当前目录修改。

什么时候用：准备把修改放进下一次提交时使用。

注意：`git add .` 会加入当前目录下大量修改，执行前先看 `git status`。

#### `git add -A`

作用：这条命令的核心作用是：暂存整个仓库新增、修改和删除。

什么时候用：准备把修改放进下一次提交时使用。

注意：`git add .` 会加入当前目录下大量修改，执行前先看 `git status`。

#### `git add -p`

作用：这条命令的核心作用是：交互式选择部分修改。

什么时候用：准备把修改放进下一次提交时使用。

注意：`git add .` 会加入当前目录下大量修改，执行前先看 `git status`。

#### `git commit -m "feat: add login"`

作用：这条命令的核心作用是：创建提交。

什么时候用：一组修改已经确认完成，要保存成本地历史时使用。

注意：`--amend` 会改最近一次提交；已推送到共享分支后谨慎使用。

#### `git commit --amend --no-edit`

作用：这条命令的核心作用是：修改最近提交但保留说明。

什么时候用：一组修改已经确认完成，要保存成本地历史时使用。

注意：`--amend` 会改最近一次提交；已推送到共享分支后谨慎使用。

## 4. 分支

### 常用命令

```bash
git branch                                      # 查看本地分支
git branch -a                                   # 查看本地和远程追踪分支
git branch -r                                   # 只查看远程追踪分支
git branch -vv                                  # 查看分支上游和同步状态
git branch feature/login                        # 创建分支但不切换
git branch -d feature/login                     # 安全删除已合并分支
git branch -D feature/login                     # 强制删除分支
git branch -m old-name new-name                 # 重命名当前分支
git switch main                                 # 切换分支
git switch -c feature/login                     # 创建并切换分支
```

### 逐条解释

#### `git branch`

作用：这条命令的核心作用是：查看本地分支。

什么时候用：查看、创建、重命名或删除本地分支时使用。

注意：`-D` 是强制删除；确认分支内容不要了再用。

#### `git branch -a`

作用：这条命令的核心作用是：查看本地和远程追踪分支。

什么时候用：查看、创建、重命名或删除本地分支时使用。

注意：`-D` 是强制删除；确认分支内容不要了再用。

#### `git branch -r`

作用：这条命令的核心作用是：只查看远程追踪分支。

什么时候用：查看、创建、重命名或删除本地分支时使用。

注意：`-D` 是强制删除；确认分支内容不要了再用。

#### `git branch -vv`

作用：这条命令的核心作用是：查看分支上游和同步状态。

什么时候用：查看、创建、重命名或删除本地分支时使用。

注意：`-D` 是强制删除；确认分支内容不要了再用。

#### `git branch feature/login`

作用：这条命令的核心作用是：创建分支但不切换。

什么时候用：查看、创建、重命名或删除本地分支时使用。

注意：`-D` 是强制删除；确认分支内容不要了再用。

#### `git branch -d feature/login`

作用：这条命令的核心作用是：安全删除已合并分支。

什么时候用：查看、创建、重命名或删除本地分支时使用。

注意：`-D` 是强制删除；确认分支内容不要了再用。

#### `git branch -D feature/login`

作用：这条命令的核心作用是：强制删除分支。

什么时候用：查看、创建、重命名或删除本地分支时使用。

注意：`-D` 是强制删除；确认分支内容不要了再用。

#### `git branch -m old-name new-name`

作用：这条命令的核心作用是：重命名当前分支。

什么时候用：查看、创建、重命名或删除本地分支时使用。

注意：`-D` 是强制删除；确认分支内容不要了再用。

#### `git switch main`

作用：这条命令的核心作用是：切换分支。

什么时候用：切换分支，或创建并切换到新分支时使用。

注意：如果有未提交修改，Git 可能阻止切换，避免覆盖你的工作。

#### `git switch -c feature/login`

作用：这条命令的核心作用是：创建并切换分支。

什么时候用：切换分支，或创建并切换到新分支时使用。

注意：如果有未提交修改，Git 可能阻止切换，避免覆盖你的工作。

## 5. 远程仓库

### 常用命令

```bash
git remote                                      # 查看远程名字
git remote -v                                   # 查看远程的拉取和推送地址
git remote add origin <url>                     # 添加名为 origin 的远程
git remote add upstream <url>                   # 添加另一个远程
git remote get-url --all origin                 # 查看 origin 的全部地址
git remote set-url origin <url>                 # 修改远程地址
git remote rename origin github                 # 修改远程名字
git remote remove upstream                      # 删除远程配置
```

### 逐条解释

#### `git remote`

作用：这条命令的核心作用是：查看远程名字。

什么时候用：查看或修改本地仓库和云端仓库 URL 的关联时使用。

注意：remote 名字只是本地别名；一个 remote 可以有 fetch 地址和多个 push 地址。

#### `git remote -v`

作用：这条命令的核心作用是：查看远程的拉取和推送地址。

什么时候用：查看或修改本地仓库和云端仓库 URL 的关联时使用。

注意：remote 名字只是本地别名；一个 remote 可以有 fetch 地址和多个 push 地址。

#### `git remote add origin <url>`

作用：这条命令的核心作用是：添加名为 origin 的远程。

什么时候用：查看或修改本地仓库和云端仓库 URL 的关联时使用。

注意：remote 名字只是本地别名；一个 remote 可以有 fetch 地址和多个 push 地址。

#### `git remote add upstream <url>`

作用：这条命令的核心作用是：添加另一个远程。

什么时候用：查看或修改本地仓库和云端仓库 URL 的关联时使用。

注意：remote 名字只是本地别名；一个 remote 可以有 fetch 地址和多个 push 地址。

#### `git remote get-url --all origin`

作用：这条命令的核心作用是：查看 origin 的全部地址。

什么时候用：查看或修改本地仓库和云端仓库 URL 的关联时使用。

注意：remote 名字只是本地别名；一个 remote 可以有 fetch 地址和多个 push 地址。

#### `git remote set-url origin <url>`

作用：这条命令的核心作用是：修改远程地址。

什么时候用：查看或修改本地仓库和云端仓库 URL 的关联时使用。

注意：remote 名字只是本地别名；一个 remote 可以有 fetch 地址和多个 push 地址。

#### `git remote rename origin github`

作用：这条命令的核心作用是：修改远程名字。

什么时候用：查看或修改本地仓库和云端仓库 URL 的关联时使用。

注意：remote 名字只是本地别名；一个 remote 可以有 fetch 地址和多个 push 地址。

#### `git remote remove upstream`

作用：这条命令的核心作用是：删除远程配置。

什么时候用：查看或修改本地仓库和云端仓库 URL 的关联时使用。

注意：remote 名字只是本地别名；一个 remote 可以有 fetch 地址和多个 push 地址。

## 6. 获取、合并和推送

### 常用命令

```bash
git fetch                                      # 获取默认远程更新，不合并
git fetch origin                               # 获取 origin 更新
git fetch --all                                # 获取所有远程更新
git fetch --prune                              # 清理已删除的远程追踪分支
git merge origin/main                          # 合并远程 main 到当前分支
git merge --abort                              # 放弃正在进行的合并
git pull                                      # 获取并合并远程更新
git pull --rebase                              # 获取后变基
git pull --ff-only                             # 只允许快进
git push -u origin feature/login               # 首次推送并建立上游
git push                                      # 推送当前分支
git push --delete origin feature/login         # 删除远程分支
git push --force-with-lease                    # 谨慎地强制更新远程
```

### 逐条解释

#### `git fetch`

作用：这条命令的核心作用是：获取默认远程更新，不合并。

什么时候用：想先拿到远程最新信息，但暂时不改本地文件时使用。

注意：fetch 后常看 `origin/main`，再决定 merge、rebase 还是 push。

#### `git fetch origin`

作用：这条命令的核心作用是：获取 origin 更新。

什么时候用：想先拿到远程最新信息，但暂时不改本地文件时使用。

注意：fetch 后常看 `origin/main`，再决定 merge、rebase 还是 push。

#### `git fetch --all`

作用：这条命令的核心作用是：获取所有远程更新。

什么时候用：想先拿到远程最新信息，但暂时不改本地文件时使用。

注意：fetch 后常看 `origin/main`，再决定 merge、rebase 还是 push。

#### `git fetch --prune`

作用：这条命令的核心作用是：清理已删除的远程追踪分支。

什么时候用：想先拿到远程最新信息，但暂时不改本地文件时使用。

注意：fetch 后常看 `origin/main`，再决定 merge、rebase 还是 push。

#### `git merge origin/main`

作用：这条命令的核心作用是：合并远程 main 到当前分支。

什么时候用：想把另一个分支的内容合进当前分支时使用。

注意：有冲突就解决冲突、`git add`，再提交；不想继续可 `git merge --abort`。

#### `git merge --abort`

作用：这条命令的核心作用是：放弃正在进行的合并。

什么时候用：想把另一个分支的内容合进当前分支时使用。

注意：有冲突就解决冲突、`git add`，再提交；不想继续可 `git merge --abort`。

#### `git pull`

作用：这条命令的核心作用是：获取并合并远程更新。

什么时候用：当前分支已经绑定 upstream，想把远程变化拉下来时使用。

注意：它通常等于 fetch 加 merge/rebase；冲突时要手动解决。

#### `git pull --rebase`

作用：这条命令的核心作用是：获取后变基。

什么时候用：当前分支已经绑定 upstream，想把远程变化拉下来时使用。

注意：它通常等于 fetch 加 merge/rebase；冲突时要手动解决。

#### `git pull --ff-only`

作用：这条命令的核心作用是：只允许快进。

什么时候用：当前分支已经绑定 upstream，想把远程变化拉下来时使用。

注意：它通常等于 fetch 加 merge/rebase；冲突时要手动解决。

#### `git push -u origin feature/login`

作用：这条命令的核心作用是：首次推送并建立上游。

什么时候用：本地 commit 想上传到远程仓库时使用。

注意：`--force-with-lease` 只用于你理解为什么要强推的场景。

#### `git push`

作用：这条命令的核心作用是：推送当前分支。

什么时候用：本地 commit 想上传到远程仓库时使用。

注意：`--force-with-lease` 只用于你理解为什么要强推的场景。

#### `git push --delete origin feature/login`

作用：这条命令的核心作用是：删除远程分支。

什么时候用：本地 commit 想上传到远程仓库时使用。

注意：`--force-with-lease` 只用于你理解为什么要强推的场景。

#### `git push --force-with-lease`

作用：这条命令的核心作用是：谨慎地强制更新远程。

什么时候用：本地 commit 想上传到远程仓库时使用。

注意：`--force-with-lease` 只用于你理解为什么要强推的场景。

## 7. 合并、变基和复制提交

### 常用命令

```bash
git merge feature/login                         # 合并功能分支
git merge --no-ff feature/login                 # 强制创建合并提交
git merge --allow-unrelated-histories           # 允许合并无共同历史的仓库
git rebase main                                 # 把当前提交接到 main 后面
git rebase -i HEAD~3                            # 交互式整理最近 3 条提交
git rebase --continue                           # 解决冲突后继续变基
git rebase --abort                              # 放弃变基
git cherry-pick <commit>                        # 复制指定提交到当前分支
git cherry-pick --abort                         # 放弃 cherry-pick
```

### 逐条解释

#### `git merge feature/login`

作用：这条命令的核心作用是：合并功能分支。

什么时候用：想把另一个分支的内容合进当前分支时使用。

注意：有冲突就解决冲突、`git add`，再提交；不想继续可 `git merge --abort`。

#### `git merge --no-ff feature/login`

作用：这条命令的核心作用是：强制创建合并提交。

什么时候用：想把另一个分支的内容合进当前分支时使用。

注意：有冲突就解决冲突、`git add`，再提交；不想继续可 `git merge --abort`。

#### `git merge --allow-unrelated-histories`

作用：这条命令的核心作用是：允许合并无共同历史的仓库。

什么时候用：想把另一个分支的内容合进当前分支时使用。

注意：有冲突就解决冲突、`git add`，再提交；不想继续可 `git merge --abort`。

#### `git rebase main`

作用：这条命令的核心作用是：把当前提交接到 main 后面。

什么时候用：想把当前分支的提交接到另一条最新历史后面时使用。

注意：rebase 会改写提交历史；共享分支上不要随便做。

#### `git rebase -i HEAD~3`

作用：这条命令的核心作用是：交互式整理最近 3 条提交。

什么时候用：想把当前分支的提交接到另一条最新历史后面时使用。

注意：rebase 会改写提交历史；共享分支上不要随便做。

#### `git rebase --continue`

作用：这条命令的核心作用是：解决冲突后继续变基。

什么时候用：想把当前分支的提交接到另一条最新历史后面时使用。

注意：rebase 会改写提交历史；共享分支上不要随便做。

#### `git rebase --abort`

作用：这条命令的核心作用是：放弃变基。

什么时候用：想把当前分支的提交接到另一条最新历史后面时使用。

注意：rebase 会改写提交历史；共享分支上不要随便做。

#### `git cherry-pick <commit>`

作用：这条命令的核心作用是：复制指定提交到当前分支。

什么时候用：只想拿某一个提交，而不是合并整个分支时使用。

注意：发生冲突时解决后继续，或者用 `git cherry-pick --abort` 放弃。

#### `git cherry-pick --abort`

作用：这条命令的核心作用是：放弃 cherry-pick。

什么时候用：只想拿某一个提交，而不是合并整个分支时使用。

注意：发生冲突时解决后继续，或者用 `git cherry-pick --abort` 放弃。

## 8. 撤销和恢复

### 常用命令

```bash
git restore <file>                             # 丢弃工作区文件修改
git restore --staged <file>                    # 取消暂存但保留文件修改
git restore --source HEAD~1 <file>              # 从旧提交恢复文件
git reset HEAD~1                                # 撤回提交，保留修改
git reset --soft HEAD~1                         # 撤回提交，修改仍在暂存区
git reset --hard HEAD~1                         # 连文件修改一起回退
git revert <commit>                             # 用新提交撤销旧提交
git revert --abort                              # 放弃正在进行的 revert
git clean -n                                    # 预览未跟踪文件删除
git clean -fd                                   # 删除未跟踪文件和目录
```

### 逐条解释

#### `git restore <file>`

作用：这条命令的核心作用是：丢弃工作区文件修改。

什么时候用：想丢弃工作区修改，或把文件从暂存区拿出来时使用。

注意：丢弃工作区修改不可轻易恢复，执行前先 `git diff`。

#### `git restore --staged <file>`

作用：这条命令的核心作用是：取消暂存但保留文件修改。

什么时候用：想丢弃工作区修改，或把文件从暂存区拿出来时使用。

注意：丢弃工作区修改不可轻易恢复，执行前先 `git diff`。

#### `git restore --source HEAD~1 <file>`

作用：这条命令的核心作用是：从旧提交恢复文件。

什么时候用：想丢弃工作区修改，或把文件从暂存区拿出来时使用。

注意：丢弃工作区修改不可轻易恢复，执行前先 `git diff`。

#### `git reset HEAD~1`

作用：这条命令的核心作用是：撤回提交，保留修改。

什么时候用：想移动当前分支指针，撤回最近提交时使用。

注意：`--hard` 会丢弃修改，很危险；共享分支上不要随便 reset 已推送历史。

#### `git reset --soft HEAD~1`

作用：这条命令的核心作用是：撤回提交，修改仍在暂存区。

什么时候用：想移动当前分支指针，撤回最近提交时使用。

注意：`--hard` 会丢弃修改，很危险；共享分支上不要随便 reset 已推送历史。

#### `git reset --hard HEAD~1`

作用：这条命令的核心作用是：连文件修改一起回退。

什么时候用：想移动当前分支指针，撤回最近提交时使用。

注意：`--hard` 会丢弃修改，很危险；共享分支上不要随便 reset 已推送历史。

#### `git revert <commit>`

作用：这条命令的核心作用是：用新提交撤销旧提交。

什么时候用：已推送的提交需要撤销时优先使用。

注意：它会新增一个反向提交，不会删除历史。

#### `git revert --abort`

作用：这条命令的核心作用是：放弃正在进行的 revert。

什么时候用：已推送的提交需要撤销时优先使用。

注意：它会新增一个反向提交，不会删除历史。

#### `git clean -n`

作用：这条命令的核心作用是：预览未跟踪文件删除。

什么时候用：想清理未跟踪文件时使用。

注意：先用 `git clean -fdn` 预览，再决定是否真的删除。

#### `git clean -fd`

作用：这条命令的核心作用是：删除未跟踪文件和目录。

什么时候用：想清理未跟踪文件时使用。

注意：先用 `git clean -fdn` 预览，再决定是否真的删除。

## 9. 暂存工作

### 常用命令

```bash
git stash                                      # 临时保存已跟踪文件的修改
git stash push -m "wip: login page"            # 保存修改并添加说明
git stash -u                                   # 同时保存未跟踪文件
git stash list                                 # 查看所有 stash
git stash show -p 'stash@{0}'                  # 查看某条 stash 的具体修改
git stash apply 'stash@{0}'                    # 应用 stash，但保留记录
git stash pop                                  # 应用最近 stash，并删除记录
git stash drop 'stash@{0}'                     # 删除指定 stash
git stash clear                                # 删除全部 stash
```

### 逐条解释

#### `git stash`

作用：把当前工作区里“已经被 Git 跟踪的文件修改”临时收起来，让工作区恢复干净。

什么时候用：代码写到一半，还不想 commit，但需要切分支、pull 最新代码、临时修 bug，或者先做另一个任务。

注意：普通 `git stash` 不会保存新建但未跟踪的文件。执行前可以先 `git status` 看看有没有 `??` 文件。

#### `git stash push -m "wip: login page"`

作用：保存 stash 的同时写一段说明，方便以后知道这条 stash 是什么。

什么时候用：你预计会有多条 stash，或者这条临时修改可能隔一段时间才恢复。比如登录页写到一半，就写 `wip: login page`。

注意：`-m` 后面的说明不是 commit message，不会进入正式提交历史，只是给 stash 列表看的备注。

#### `git stash -u`

作用：保存已跟踪文件的修改，同时也保存未跟踪的新文件。

什么时候用：你新建了文件，但还没有 `git add`，又想把整个工作区都临时收起来。比如新建了 `login.md`，普通 stash 收不走它，就用 `git stash -u`。

注意：`-u` 是 `--include-untracked` 的缩写。被 `.gitignore` 忽略的文件仍然不会保存；那种情况才考虑 `-a`，但新手先别急着用。

#### `git stash list`

作用：查看当前仓库所有 stash 记录。

什么时候用：恢复 stash 前先看一眼，确认你要恢复的是哪一条。`stash@{0}` 是最新一条，`stash@{1}` 是更早一条。

注意：stash 编号会变化。删除或 pop 掉前面的 stash 后，后面的编号会往前移动。

#### `git stash show -p 'stash@{0}'`

作用：查看某条 stash 里面具体改了哪些内容。

什么时候用：你不确定 `stash@{0}` 是不是想要的那条，先用它检查差异，再决定 apply 或 pop。

注意：`-p` 表示显示补丁详情；不加 `-p` 通常只显示文件概要。PowerShell 里建议把 `stash@{0}` 用单引号包起来。

#### `git stash apply 'stash@{0}'`

作用：把指定 stash 的修改恢复到当前工作区，但 stash 记录仍然保留。

什么时候用：你想先试着恢复修改，但还想留一份备份；或者同一条 stash 可能要应用到多个分支。

注意：如果当前文件和 stash 修改了同一块内容，可能产生冲突。解决后需要 `git add` 标记解决。

#### `git stash pop`

作用：应用最近一条 stash，应用成功后删除这条 stash 记录。

什么时候用：你确定最近那条 stash 就是要恢复的内容，而且恢复后不再需要保留 stash 备份。

注意：如果发生冲突，Git 通常不会删除这条 stash。解决冲突后可以再用 `git stash list` 确认它是否还在。

#### `git stash drop 'stash@{0}'`

作用：删除指定 stash。

什么时候用：确认某条 stash 已经没用了，想清理列表时使用。

注意：删除后不像普通 commit 那样容易找回。删之前建议用 `git stash show -p 'stash@{0}'` 看一眼。

#### `git stash clear`

作用：删除当前仓库里的全部 stash。

什么时候用：只有在你确认所有 stash 都是废弃临时修改时才用。

注意：这是批量删除，风险比 `drop` 更大。学习阶段建议少用，真要用之前先 `git stash list`。

## 10. 标签和版本

### 常用命令

```bash
git tag                                      # 查看标签
git tag v1.0.0                               # 创建轻量标签
git tag -a v1.0.0 -m "release v1.0.0"        # 创建带说明的标签
git show v1.0.0                              # 查看标签指向的提交
git push origin v1.0.0                       # 推送一个标签
git push origin --tags                       # 推送全部标签
git tag -d v1.0.0                            # 删除本地标签
git push origin --delete v1.0.0              # 删除远程标签
```

### 逐条解释

#### `git tag`

作用：这条命令的核心作用是：查看标签。

什么时候用：发布版本或给重要提交打标记时使用。

注意：普通 `git push` 不会自动推送标签，需要单独推送。

#### `git tag v1.0.0`

作用：这条命令的核心作用是：创建轻量标签。

什么时候用：发布版本或给重要提交打标记时使用。

注意：普通 `git push` 不会自动推送标签，需要单独推送。

#### `git tag -a v1.0.0 -m "release v1.0.0"`

作用：这条命令的核心作用是：创建带说明的标签。

什么时候用：发布版本或给重要提交打标记时使用。

注意：普通 `git push` 不会自动推送标签，需要单独推送。

#### `git show v1.0.0`

作用：这条命令的核心作用是：查看标签指向的提交。

什么时候用：想看某个提交或标签具体内容时使用。

注意：可以把 `HEAD` 换成提交哈希、分支名或标签名。

#### `git push origin v1.0.0`

作用：这条命令的核心作用是：推送一个标签。

什么时候用：本地 commit 想上传到远程仓库时使用。

注意：`--force-with-lease` 只用于你理解为什么要强推的场景。

#### `git push origin --tags`

作用：这条命令的核心作用是：推送全部标签。

什么时候用：本地 commit 想上传到远程仓库时使用。

注意：`--force-with-lease` 只用于你理解为什么要强推的场景。

#### `git tag -d v1.0.0`

作用：这条命令的核心作用是：删除本地标签。

什么时候用：发布版本或给重要提交打标记时使用。

注意：普通 `git push` 不会自动推送标签，需要单独推送。

#### `git push origin --delete v1.0.0`

作用：这条命令的核心作用是：删除远程标签。

什么时候用：本地 commit 想上传到远程仓库时使用。

注意：`--force-with-lease` 只用于你理解为什么要强推的场景。

## 11. 临时保存、排错和恢复历史

### 常用命令

```bash
git reflog                                    # 查看本地指针移动记录
git branch recover-work HEAD@{3}               # 从历史位置创建恢复分支
git bisect start                               # 开始二分排错
git bisect bad                                 # 标记当前版本有问题
git bisect good <commit>                       # 标记已知正常版本
git bisect reset                               # 结束二分并回到原分支
git fsck --lost-found                          # 检查底层对象
```

### 逐条解释

#### `git reflog`

作用：这条命令的核心作用是：查看本地指针移动记录。

什么时候用：误删、误 reset、误 rebase 后想找回旧位置时使用。

注意：reflog 是本地记录，不等同于远程历史。

#### `git branch recover-work HEAD@{3}`

作用：这条命令的核心作用是：从历史位置创建恢复分支。

什么时候用：查看、创建、重命名或删除本地分支时使用。

注意：`-D` 是强制删除；确认分支内容不要了再用。

#### `git bisect start`

作用：这条命令的核心作用是：开始二分排错。

什么时候用：已知老版本正常、新版本异常，想定位哪个提交引入问题时使用。

注意：每一步测试后标记 good 或 bad，结束后用 `git bisect reset`。

#### `git bisect bad`

作用：这条命令的核心作用是：标记当前版本有问题。

什么时候用：已知老版本正常、新版本异常，想定位哪个提交引入问题时使用。

注意：每一步测试后标记 good 或 bad，结束后用 `git bisect reset`。

#### `git bisect good <commit>`

作用：这条命令的核心作用是：标记已知正常版本。

什么时候用：已知老版本正常、新版本异常，想定位哪个提交引入问题时使用。

注意：每一步测试后标记 good 或 bad，结束后用 `git bisect reset`。

#### `git bisect reset`

作用：这条命令的核心作用是：结束二分并回到原分支。

什么时候用：已知老版本正常、新版本异常，想定位哪个提交引入问题时使用。

注意：每一步测试后标记 good 或 bad，结束后用 `git bisect reset`。

#### `git fsck --lost-found`

作用：这条命令的核心作用是：检查底层对象。

什么时候用：当你需要。执行前如果不确定，先用 git status 看当前状态。

注意：注意目标分支、文件名或提交号要写对；涉及删除、覆盖、强推的命令要先确认。

## 12. 暂存区之外的工程工具

### 常用命令

```bash
git worktree add ../hotfix hotfix             # 在另一个目录检出分支
git worktree list                             # 查看 worktree
git worktree remove ../hotfix                 # 删除 worktree
git archive --format=zip --output=release.zip HEAD # 导出源码包
git sparse-checkout init --cone               # 开启部分检出
git sparse-checkout set src docs              # 只检出指定目录
git sparse-checkout disable                   # 关闭部分检出
```

### 逐条解释

#### `git worktree add ../hotfix hotfix`

作用：这条命令的核心作用是：在另一个目录检出分支。

什么时候用：想在另一个目录同时打开同一仓库的另一个分支时使用。

注意：删除 worktree 前先用 `git worktree list` 确认路径。

#### `git worktree list`

作用：这条命令的核心作用是：查看 worktree。

什么时候用：想在另一个目录同时打开同一仓库的另一个分支时使用。

注意：删除 worktree 前先用 `git worktree list` 确认路径。

#### `git worktree remove ../hotfix`

作用：这条命令的核心作用是：删除 worktree。

什么时候用：想在另一个目录同时打开同一仓库的另一个分支时使用。

注意：删除 worktree 前先用 `git worktree list` 确认路径。

#### `git archive --format=zip --output=release.zip HEAD`

作用：这条命令的核心作用是：导出源码包。

什么时候用：想导出一份不带 `.git` 历史的源码包时使用。

注意：它只是导出文件，不会创建提交或标签。

#### `git sparse-checkout init --cone`

作用：这条命令的核心作用是：开启部分检出。

什么时候用：大型仓库只想检出部分目录时使用。

注意：普通小仓库一般不用，开启后工作区只显示选定目录。

#### `git sparse-checkout set src docs`

作用：这条命令的核心作用是：只检出指定目录。

什么时候用：大型仓库只想检出部分目录时使用。

注意：普通小仓库一般不用，开启后工作区只显示选定目录。

#### `git sparse-checkout disable`

作用：这条命令的核心作用是：关闭部分检出。

什么时候用：大型仓库只想检出部分目录时使用。

注意：普通小仓库一般不用，开启后工作区只显示选定目录。

## 13. 子模块

### 常用命令

```bash
git submodule add <url> path/to/module       # 添加子模块
git submodule update --init --recursive      # 初始化并下载子模块
git submodule update --remote                 # 更新子模块引用
git submodule deinit <path>                   # 取消初始化子模块
```

### 逐条解释

#### `git submodule add <url> path/to/module`

作用：这条命令的核心作用是：添加子模块。

什么时候用：当前仓库需要引用另一个独立 Git 仓库时使用。

注意：子模块会增加 clone、更新、提交复杂度，不要为了普通文件夹关系就使用。

#### `git submodule update --init --recursive`

作用：这条命令的核心作用是：初始化并下载子模块。

什么时候用：当前仓库需要引用另一个独立 Git 仓库时使用。

注意：子模块会增加 clone、更新、提交复杂度，不要为了普通文件夹关系就使用。

#### `git submodule update --remote`

作用：这条命令的核心作用是：更新子模块引用。

什么时候用：当前仓库需要引用另一个独立 Git 仓库时使用。

注意：子模块会增加 clone、更新、提交复杂度，不要为了普通文件夹关系就使用。

#### `git submodule deinit <path>`

作用：这条命令的核心作用是：取消初始化子模块。

什么时候用：当前仓库需要引用另一个独立 Git 仓库时使用。

注意：子模块会增加 clone、更新、提交复杂度，不要为了普通文件夹关系就使用。

## 14. 常见协作流程

### 常用命令

```bash
git switch main                               # 切换主分支
git pull --ff-only                            # 只同步不产生自动合并提交
git switch -c feature/login                   # 创建功能分支
git add -p                                    # 选择性暂存
git commit -m "feat: add login"               # 提交功能
git push -u origin feature/login              # 推送功能分支
git fetch origin                               # 获取主线最新信息
git rebase origin/main                         # 将功能分支接到主线之后
git push --force-with-lease                   # 更新已变基的个人远程分支
```

### 逐条解释

#### `git switch main`

作用：这条命令的核心作用是：切换主分支。

什么时候用：切换分支，或创建并切换到新分支时使用。

注意：如果有未提交修改，Git 可能阻止切换，避免覆盖你的工作。

#### `git pull --ff-only`

作用：这条命令的核心作用是：只同步不产生自动合并提交。

什么时候用：当前分支已经绑定 upstream，想把远程变化拉下来时使用。

注意：它通常等于 fetch 加 merge/rebase；冲突时要手动解决。

#### `git switch -c feature/login`

作用：这条命令的核心作用是：创建功能分支。

什么时候用：切换分支，或创建并切换到新分支时使用。

注意：如果有未提交修改，Git 可能阻止切换，避免覆盖你的工作。

#### `git add -p`

作用：这条命令的核心作用是：选择性暂存。

什么时候用：准备把修改放进下一次提交时使用。

注意：`git add .` 会加入当前目录下大量修改，执行前先看 `git status`。

#### `git commit -m "feat: add login"`

作用：这条命令的核心作用是：提交功能。

什么时候用：一组修改已经确认完成，要保存成本地历史时使用。

注意：`--amend` 会改最近一次提交；已推送到共享分支后谨慎使用。

#### `git push -u origin feature/login`

作用：这条命令的核心作用是：推送功能分支。

什么时候用：本地 commit 想上传到远程仓库时使用。

注意：`--force-with-lease` 只用于你理解为什么要强推的场景。

#### `git fetch origin`

作用：这条命令的核心作用是：获取主线最新信息。

什么时候用：想先拿到远程最新信息，但暂时不改本地文件时使用。

注意：fetch 后常看 `origin/main`，再决定 merge、rebase 还是 push。

#### `git rebase origin/main`

作用：这条命令的核心作用是：将功能分支接到主线之后。

什么时候用：想把当前分支的提交接到另一条最新历史后面时使用。

注意：rebase 会改写提交历史；共享分支上不要随便做。

#### `git push --force-with-lease`

作用：这条命令的核心作用是：更新已变基的个人远程分支。

什么时候用：本地 commit 想上传到远程仓库时使用。

注意：`--force-with-lease` 只用于你理解为什么要强推的场景。

## 15. 安全规则和学习顺序

### 常用检查命令

```bash
git status                                    # 操作前确认当前状态
git diff                                      # 确认工作区修改
git diff --cached                             # 提交前确认暂存内容
git log --oneline --decorate -5                # 推送前确认最近历史
git merge --abort                             # 放弃合并
git rebase --abort                             # 放弃变基
```

### 逐条解释

#### `git status`

作用：这条命令的核心作用是：操作前确认当前状态。

什么时候用：任何 Git 操作前后都可以使用，尤其是不知道当前仓库发生了什么时。

注意：它只查看状态，不会修改文件。

#### `git diff`

作用：这条命令的核心作用是：确认工作区修改。

什么时候用：提交前、恢复前、解决冲突前，用来确认具体改动。

注意：`--cached` 看暂存区；不加参数主要看工作区未暂存内容。

#### `git diff --cached`

作用：这条命令的核心作用是：提交前确认暂存内容。

什么时候用：提交前、恢复前、解决冲突前，用来确认具体改动。

注意：`--cached` 看暂存区；不加参数主要看工作区未暂存内容。

#### `git log --oneline --decorate -5`

作用：这条命令的核心作用是：推送前确认最近历史。

什么时候用：当你需要。执行前如果不确定，先用 git status 看当前状态。

注意：注意目标分支、文件名或提交号要写对；涉及删除、覆盖、强推的命令要先确认。

#### `git merge --abort`

作用：这条命令的核心作用是：放弃合并。

什么时候用：想把另一个分支的内容合进当前分支时使用。

注意：有冲突就解决冲突、`git add`，再提交；不想继续可 `git merge --abort`。

#### `git rebase --abort`

作用：这条命令的核心作用是：放弃变基。

什么时候用：想把当前分支的提交接到另一条最新历史后面时使用。

注意：rebase 会改写提交历史；共享分支上不要随便做。


