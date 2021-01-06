## github
### vscode_sync
- access token: 969a439d08bc1146b5de1b9aa07dbf2aceac0a0b
- 6a922f390c9275f4ce5aa73736c08ebd
- alt shift u   上传
- alt shift d   下载

# Git 命令

## 初始化仓库
1. `git init`     含本地worktree
    - 修改 git/config (避免主仓worktree影响push)
        [receive]
        denyCurrentBrash = ignore
    - 他人推送后，主仓需要 `git reset --hard HEAD` 才能看到更新

2. `git --bare init`  不包含本地worktree
    - 也可以通过 `git config --bool core.bare true` 切换成不含worktree

3. `git clone <url> -b dev`     拉取仓库并切换到分支dev

## remote
* git remote -v                     查看远程地址
- git remote set-url origin [url]   修改远程仓库地址
- git remote add group [url]        添加远程仓地址，并添加别名group
- git fetch group                   拉取group仓
- git push group master             推送master代码到group仓
- git remote show group             查看仓信息
- git remote rename group origin    重命名
- git remote remove group           删除远程仓库group

## 配置
- git config --list 查看全局配置
- 修改全局：
    - git config --global user.name "duyanjie"
    - git config --global user.email "***@163.com"
- 修改当前项目：
    - git config user.name ""
    - git config user.email ""

## 跟踪文件
- git add .                 跟踪，暂存
- git add filename
- git stage .               添加暂存，红变绿
- git reset HEAD            撤销跟踪, 绿变红
- git reset HEAD filename
- git reset --soft HEAD     回滚到某次提交，保留本地修改，不撤销add
- get reset --mixed HEAD    回滚到某次提交，保留本地修改，撤销add
- git reset --hard HEAD     回滚到某次提交，删除本地修改，撤销add
- git checkout -- *         撤销未跟踪文件修改
- git checkout -- filename  撤销已修改未跟踪文件
- git clean -f              清理未跟踪文件
- git clean -fd            清理未跟踪文件和文件夹
- git clean -nfd            查看会清理那些文件
- git rm -r -n --cached file/dir    列出想要取消跟踪的文件
- git rm -r --cached file/dir       撤销跟踪，然后再添加ignore，防止继续跟踪

## 暂存
- git stash                     暂存
- git stash list                显示暂存列表
- git stash pop                 应用并且删除
- git stash apply stash@{0}     应用
- git stash show stask@{0}      显示
- git stash drop                删除
- git stash clear               清除所有暂存

## 分支，合并
- git checkout dev
- git merge dev         dev分支合并到当前分支
- git checkout -b dev               创建本地dev分支，并切换到dev分支
- git push origin dev:dev           将dev分支推送到远程
- git push origin --delete dev      删除远程dev分支
- git checkout -b dev origin/dev    拉取远程分支dev到本地
- git branch [-a/-r/-b]             查看所有分支 [全部/远程/本地]

- git branch --set-upstream-to=origin/dev   设置默认push/pull 为dev分支
- git branch --unset-upstream master

## Patch
- git format-patch HEAD&
- git format-patch -1 <commit id>           某次提交的变更
- git format-patch <from commit id>
- git format-patch <from commit id>..<to commit id>

- git apply --stat *.patch      查看patch内容
- git apply --check *.patch     测试patch能否打上，无内容说明正常
- git apply *.patch             打patch，只修改，不提交
- git am *.patch                打patch，并直接提交commit
- git am --abord                终止，返回原始状态

## Log
- git log --pretty=oneline
- git log --author=duyanjie
- git log --pretty=format:"%H %am %cd %s" --graph

## 恢复stash clear 的占村代码
1. git fsck --lost-found        列出记录
2. 查看类似 dangling commit [id]
3. git show [id]    查看提交内容
4. git merge [id]   还原被清理的暂存