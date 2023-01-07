# Git笔记

## 常用命令

git 和 Linux 是同一个爹 命令一样

git config --global user.name 用户名

git config --global user.email 邮箱

git init 初始化本地库  进入项目目录 如 /Git-Space/  再初始化

git status 查看本地库状态

git add 文件名 添加到暂存区

git commit -m “日志信息” 文件名 提交到本地库

git reflog 查看历史记录

git log 查看详细日志

git reset --hard 版本号 版本穿梭

git rm --cached 文件名 从暂存区删除文件

## 分支

git branch 分支名 创建分支

git branch -v 查看分支 可以查看当前git-demo的全部分支

git checkout 分支名 切换分支

git merge 分支名 把指定的分支合并到当前分支上

​	合并分支时，如果发生冲突，<<<<<<<<<<

​												   ==========

​													>>>>>>>>>> 表示冲突的内容，需要手动合并，然后直接 git merge -m "日志信息"

## 远程仓库操作

git remote -v 查看当前所有远程地址别名

git remote add 别名 远程地址 起别名

git push 别名 分支 推送本地分支上的内容到远程仓库

git clone 远程地址 将远程地址的内容克隆到本地

git pull 远程库地址别名 远程分支别名 将远程库对应分支最新内容拉下来后与当前分支直接合并

git push 别名 分支 推送本地分支到远程仓库

