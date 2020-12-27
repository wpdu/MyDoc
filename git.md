# Git 命令

## 初始化仓库
1. git init     含本地worktree
    - 修改 git/config (避免主仓worktree影响push)
        [receive]
        denyCurrentBrash = ignore

2. git --bare init  不包含本地worktree
    - 也可以通过 git config --bool core.bare true 切换成不含worktree

## 配置
- git config --list 查看全局配置
- 修改全局：
    - git config --global user.name "duyanjie"
    - git config --global user.email "***@163.com"
- 修改当前项目：
    - git config user.name ""
    - git config user.email ""

## 跟踪文件
- git add .             跟踪，暂存
- git add filename
- git stage .           添加暂存，红变绿
- git reset HEAD        撤销跟踪, 绿变红
- git reset HEAD filename
- git checkout -- *         撤销未跟踪文件修改
- git checkout -- filename  
- git rm -r -n --cached file/dir    列出想要取消跟踪的文件
- git rm -r --cached file/dir       撤销跟踪，然后再添加ignore，防止继续跟踪

