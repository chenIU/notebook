# 常用命令
| 命令                                                   | 说明                                           |
| ------------------------------------------------------ | ---------------------------------------------- |
| git push origin :branch_name                           | 删除远程分支                                   |
| git branch -r -d origin/branch_name                    | 删除远程分支                                   |
| git branch -d branch_name                              | 删除本地分支                                   |
| git branch -D branch_name                              | 强制删除本地分支                               |
| git checkout --track origin/branch_name                | 在本地建立一个远程分支的跟踪分支               |
| git checkout -b branch_name origin                     | 复制远程的分支                                 |
| git push --set-upstream origin branch_name             | 将本地的新分支推送到远程                       |
| git rebase 主干分支  特性分支                          | 将特性分支中的内容变基到主干分支               |
| git rebase --continue                                  | 继续变基操作                                   |
| git rebase --skip                                      | 跳过变基操作                                   |
| git rebase --abort                                     | 放弃变基操作                                   |
| git rabase --onto master server client                 | 找出client和server的不同变基到master           |
| git show SHA-1的值                                     | 查看具体某次提交的详细信息                     |
| git log --abbrev-commit --pretty=oneline               | 美化git提交日志                                |
| git show branch_name                                   | 查看某个分支最后一次提交信息                   |
| git reflog                                             | 引用日志里的简称                               |
| git show HEAD^        等价于HEAD~                      | HEAD的父提交                                   |
| git stash                                              | 暂存当前修改                                   |
| git stash save                                         | 增加stash工作区日志内容                        |
| git stash show                                         | 查看最近保存到暂存区中的内容                   |
| git stash show -p                                      | 查看修改了什么文件，里面修改了什么内容         |
| git stash list                                         | 查看所有的暂存                                 |
| git stash pop                                          | 将最后一次stash工作区提取出来，并删除栈中记录  |
| git stash apply                                        | 应用最近的一次暂存，但不会删除栈中记录         |
| git stash apply stash{index}                           | 应用某次的暂存                                 |
| git stash drop stash_name                              | 移除某个暂存                                   |
| git stash clear                                        | 清空所有缓存的stash                            |
| git commit --amend                                     | 修改提交记录                                   |
| git reset --hard origin/master                         | 还原本地到初始状态                             |
| git help command                                       | 查看某个命令的帮助文档                         |
| git config --global alias.co checkout                  | 为git checkout命令指定别名，其他类似           |
| git log -1 HEAD                                        | 查看最后一次提交的历史                         |
| git reset HEAD file_name                               | 对某个文件取消暂存                             |
| git pull origin master                                 | 拉取远程内容                                   |
| git push -u origin master                              | 第一次推送，且远程仓库是空                     |
| git remote add origin git仓库地址                      | 将本地和远程git仓库关联                        |
| git remote show origin                                 | 查看远程信息                                   |
| git tag                                                | 查看所有的标签                                 |
| git tag tag_name                                       | 创建标签                                       |
| git tag -d tag_name                                    | 删除标签                                       |
| git push origin tag_name                               | 推送某一个标签                                 |
| git push origin --tags                                 | 一次性推送所有标签                             |
| git fetch + git merge =git pull                        | 后者可能会出现冲突                             |
| git fetch origin                                       | 拉取默认分支的内容                             |
| git fetch origin branch1:branch2                       | 在本地创建分支并拉取                           |
| git config user.name                                   | 查看某项配置                                   |
| git rest HEAD                                          | 暂存区的目录树会被重写                         |
| git clone xxx repo_name                                | clone的时候指定新的仓库名称                    |
| **git diff**                                           | 查看尚未缓存的改动                             |
| git diff --cached                                      | 查看已缓存的改动                               |
| git diff HEAD                                          | 查看已缓存和尚未缓存的改动                     |
| git diff --state                                       | 显示摘要而非整个diff                           |
| git commit -am "xxx"                                   | 跳过git add而直接commit                        |
| git reset HEAD                                         | 取消已缓存的内容                               |
| git rm --cached  file_name                             | 从暂存区移除，在工作目录中保存                 |
| git checkout -b branch_name                            | 创建并切换分支                                 |
| git log --oneline                                      | 简明查看提交日志                               |
| git log --reverse --oneline                            | 逆向查看日志                                   |
| git remote                                             | 当前仓库配置了哪些远程仓库                     |
| git remote -v                                          | 远程仓库的具体信息                             |
| git remote rm  别名                                    | 删除远程仓库                                   |
| git push origin master                                 | 推送本地分支到远端                             |
| git checkout -- <file_name>                            | 用master中的内容替换掉工作目录中的修改         |
| git fetch origin                                       | 拉取远端最新代码                               |
| git reset --hard origin/master                         | 将本地分支指向拉取下来的最新master             |
| git config format.pretty oneline                       | 查看提交历史时只显示一行                       |
| git reset --hard HEAD^                                 | 回退到上一次版本                               |
| git reset --hard HEAD~3                                | 回退到三次提交之前                             |
| git reset --hard HEAD commit_id                        | 回退到指定的提交时刻                           |
| git push origin HEAD --force                           | 强制将本地的代码还原为远端                     |
| git rm --cached file_name                              | 让git不再追踪某个文件/回退git add的文件        |
| git remote add origin repo_addr                        | 让本地仓库和远端仓库关联                       |
| git push --set-upstream origin master                  | 第一次上传本地仓库代码                         |
| git config credential.helper store                     | 保存git账户和密码                              |
| git config --global alias.last 'log -1 HEAD'           | 查看最后一次提交                               |
| git reset --mixed HEAD^                                | commit和index回退到上个版本，保留源码变更      |
| git reset --soft HEAD^                                 | commit回退，保留源码和index变更                |
| git reset--hard HEAD^                                  | commit、index、源码都会回退到上个版本          |
| git revert <commit_id>                                 | 可以将本地和远程代码同时回退，之后执行git push |
| git config --global user.name                          | 查看user.name属性值                            |
| git config --global user.name "chenjy"                 | 为user.name重新赋值                            |
| git diff --stat master origin/master                   | 比较本地和远程master分支文件的差别             |
| git config --global alias.glog "log --oneline --graph" | 设置别名                                       |
| git config --list\|grep alias                          | 查看别名                                       |
| git config --global --unset alias.br                   | 取消别名                                       |
| git log --oneline --graph                              | 图形化形式查看提交日志                         |
| git log --pretty=oneline --abbrev-commit               | 简略形式查看提交日志                           |
| git push --delete origin branch_name                   | 删除远程分支                                   |



# 名词解释

## 1、HEAD

是一个指向本地工作分支的指针，可以将HEAD想象为当前分支的别名。

![HEAD图示](D:\snipaste\Snipaste_2020-04-24_08-38-05.png)

## 2、Merge into Current

合并指定分支到当前分支，可以理解为current省略了this。

![image-20200424101613347](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200424101613347.png)

当前分支test，此操作过后，dev分支合并到test分支。



# 组合操作

## 1、关联仓库

git add .

git commit -m "xxx"

git remote add origin url

git push -u origin master

## 2、merge回滚

git checkout branch_name：切换到需要处理的分支上

git reflog：查看提交历史记录

git reset --hard commit_id：回滚到merge之前的版本号

## 3、回退远程代码

git reflog| grep branch_name：查看需要回退版本的commit_id

git reset --hard commit_id：回退代码

git push origin HEAD --force：强制提交到远程

## 4、推送分支

git checkout -b branch_name：本地新建分支

git push --set-upstream origin branch_name：推送本地分支到远程

git fetch：拉取新建的分支

git branch -d branch_name：删除本地分支

git push origin :branch_name：删除远程分支

## 5、cherry-pick

git cherry-pick commit_id：合并其他分支指定的commit_id

git cherry-pick --continue：解决冲突之后执行此命令，继续之前的合并

git cherry-pick --skip：跳过本地合并

git cherry-pick --abort：放弃本次cherry-pick

## 6、回退提交

### 6.1 本地回退

git reset --hard commit_id(可以使用git log -online查看)

### 6.2 远程回退

git push origin HEAD --force



# 注意事项

* 在当前分支上不能删除本分支
* 在某个分支没有合并之前必须使用强制删除分支命令才能删除分支
* stash命令的作用是将修改的内容暂时保存到暂存区，而将工作区中的修改暂时抹除
* git维护的三颗"树"，工作目录、暂存区(index)、HEAD
* HEAD指向最后一次提交的结果
* 解决完冲突之后要执行git add <file_name> 将它们标记为合并成功
* git status无法识别新建文件夹时，可以在文件夹中添加文件再执行git status命令
* git仅跟踪文件的变动，不跟踪目录
* 本地分支的指针HEAD可以小写



# github高级搜索

| 指令                            | 解释                                         |
| ------------------------------- | -------------------------------------------- |
| in:name spring cloud            | 名称中包含spring cloud的仓库                 |
| in:description spring cloud     | 描述中包含spring cloud的仓库                 |
| in:readme spring cloud          | readme文件中包含spring cloud的仓库           |
| stars:>3000 spring cloud        | star大于3000的仓库                           |
| forks:10..20 spring cloud       | fork在10到20之间的仓库                       |
| size:>5000                      | 大小大于5000K的仓库                          |
| pushed:>2020-06-18 spring cloud | 最后一次更新大于2020-06-18的spring cloud仓库 |
| license:apache-2.0 spring cloud | LICENCE是apache-2.0的spring cloud仓库        |
| language:java spring cloud      | 语言是java的spring cloud仓库                 |
| user:cheniu spring cloud        | 作者是cheniu的spring cloud仓库               |





