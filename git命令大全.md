# 1. git 命令大全

<!-- TOC -->

- [1. git 命令大全](#1-git-命令大全)
    - [1.1. 须知概念](#11-须知概念)
    - [1.2. 全局配置](#12-全局配置)
    - [1.3. 帮助命令](#13-帮助命令)
    - [1.4. 查询命令](#14-查询命令)
    - [1.5. 跟踪和提交](#15-跟踪和提交)
    - [1.6. 文件比较](#16-文件比较)
    - [1.7. 文件回退](#17-文件回退)
    - [1.8. 版本回退](#18-版本回退)
    - [1.9. 远程库命令](#19-远程库命令)
    - [1.10. 分支命令](#110-分支命令)
    - [1.11. stash命令](#111-stash命令)
    - [1.12. 标签命令](#112-标签命令)

<!-- /TOC -->
## 1.1. 须知概念
- git是一条时间轴， 分支（master dev）指向提交时间点（commit id），HEAD 指向当前分支。
- git分支切换指向
    - 切换到master分支：![git](1.png)
    - 创建并切换到dev分支：![git](2.png)
    - dev修改提交（commit）:![git](3.png)
    - 切换到master，合并dev：![git](4.png)
- add 将工作区添加到index(stage)中，用于下次提交； commit 将index中提交到 版本库中。
- git结构 ![git](0.jpg)
- pull 拉取远程库  push 推送到远程库。
- stash 保存工作现场(工作区)。


## 1.2. 全局配置
- git config --global credential.helper store
- git config --global color.ui true
- git config --global user.name "Your Name"
- git config --global user.email "email@example.com"
- git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

## 1.3. 帮助命令
- git --help
- git help \<command>

## 1.4. 查询命令

|命令|参数|说明|
|----|----|----|
|git init|无|初始化|
|git status|无|当前git状态|
|git log --pretty=oneline|无|日志信息|
|git log --graph|无|分支合并图|
|git reflog|无|命令历史记录|
|git tag|无|标签信息|
|git show \<tagName>|tagName|标签详细信息|

## 1.5. 跟踪和提交

|命令|参数|说明|
|----|----|----|
|git add \<files>|files|添加到暂存区(index)|
|git commit -m "commit mark"|commit mark|提交到版本库|

## 1.6. 文件比较

|命令|参数|说明|
|----|----|----|
|git diff \<file>|file|工作区 与 暂存区 比较|
|git diff --staged \<file>|file|暂存区 和 版本库 比较|
|git diff HEAD -- \<file>|file|工作区 和 版本库 比较|

## 1.7. 文件回退

|命令|参数|说明|
|----|----|----|
|git reset HEAD \<file>|file|把暂存区file的修改撤销掉（unstage），回到版本库的|
|git checkout -- \<file>|file|让这个文件回到最近一次git commit或git add时的状态，取消工作区修改|

- git reset [--soft (只重置commit)|--mixed(默认，重置index和commit)|--hard(工作区，index,commit 都重置)] 
- git revert [-n(不自动提交)] （反向提交）
## 1.8. 版本回退

|命令|参数|说明|
|----|----|----|
|git reset --hard \<commit id>|commit id|版本库切换， 工作区 暂存区 版本库 全部替换|
|git reset --hard HEAD^|HEAD^ HEAD^^ HEAD-100|版本库切换  工作区 暂存区 版本库 全部替换|

## 1.9. 远程库命令

|命令|参数|说明|
|----|----|----|
|git remote add origin git@server-name:path/repo-name.git|origin url|关联origin远程仓库|
|git push -u origin master|无|第一次推送|
|git push|无|后面推送|
|git clone git@server-name:path/repo-name.git|无|clone 远程库， SSH协议|
|git clone https://github.com/....|无|clone 远程库， HTTP协议|
|git remote rm origin|origin|删除origin远程库连接|
|git remote -v|无|查看远程库信息|
|git branch --set-upstream branch-name origin/branch-name|branch-name|本地分支和远程分支创建链接关系|
|git push --force origin \<branch-name>|branch-name|强制推送|
|git fetch|无|修改 本地远程库记录 的commit id|
|git pull|无|修改 本地版本库  的 commit id|

## 1.10. 分支命令

|命令|参数|说明|
|----|----|----|
|git branch|无|查看分支|
|git branch \<name>|name|创建分支|
|git branch -d \<name>|name|删除分支|
|git branch -D \<name>|name|强制删除分支|
|git push origin --delete \<name>|name|删除远程分支|
|git checkout \<name>|name|切换分支|
|git checkout -b \<name>|name|创建+切换分支|
|git checkout -b \<name> origin/\<name>|name|创建+切换分支+远程对应分支链接关系创建|
|git merge \<name>|name|将name分支合并到当前分支|
|git merge --no-ff -m 'commit mark' \<name>|name|将name分支合并到当前分支,并且将name分支修改提交到当前提交历史|

- 注：解决冲突后， 先 git add \<conflict files>, 再  git commit -m 'conflict fixed'

## 1.11. stash命令

|命令|参数|说明|
|----|----|----|
|git stash|无|暂存工作现场|
|git stash list|无|查看|
|git stash apply|无|恢复，并不删除stash|
|git stash drop|无|删除|
|git stash pop|无|恢复的同时把stash内容也删了|

## 1.12. 标签命令

|命令|参数|说明|
|----|----|----|
