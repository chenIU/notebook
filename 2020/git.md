# 常用命令

| 命令                                                   | 说明                                           |
| ------------------------------------------------------ | ---------------------------------------------- |
| git checkout --track origin/branch_name                | 在本地建立一个远程分支的跟踪分支               |
| git rebase 主干分支  特性分支                          | 将特性分支中的内容变基到主干分支               |
| git rebase --continue                                  | 继续变基操作                                   |
| git rebase --skip                                      | 跳过变基操作                                   |
| git rebase --abort                                     | 放弃变基操作                                   |
| git rabase --onto master server client                 | 找出client和server的不同变基到master           |
| git show SHA-1的值                                     | 查看具体某次提交的详细信息                     |
| git log --abbrev-commit --pretty=oneline               | 美化git提交日志                                |
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
| git fetch + git merge =git pull                        | 后者可能会出现冲突                             |
| git fetch origin                                       | 拉取默认分支的内容                             |
| git config user.name                                   | 查看某项配置                                   |
| git rest HEAD                                          | 暂存区的目录树会被重写                         |
| git clone xxx repo_name                                | clone的时候指定新的仓库名称                    |
| git diff                                               | 查看尚未缓存的改动                             |
| git diff --cached                                      | 查看已缓存的改动                               |
| git diff HEAD                                          | 查看已缓存和尚未缓存的改动                     |
| git diff --state                                       | 显示摘要而非整个diff                           |
| git commit -am "xxx"                                   | 跳过git add而直接commit                        |
| git reset HEAD                                         | 取消已缓存的内容                               |
| git rm --cached  file_name                             | 从暂存区移除，在工作目录中保存                 |
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
| git reset --hard HEAD^                                 | commit、index、源码都会回退到上个版本          |
| git revert <commit_id>                                 | 可以将本地和远程代码同时回退，之后执行git push |
| git config --global user.name                          | 查看user.name属性值                            |
| git config --global user.name "chenjy"                 | 为user.name重新赋值                            |
| git diff --stat master origin/master                   | 比较本地和远程master分支文件的差别             |
| git config --global alias.glog "log --oneline --graph" | 设置别名                                       |
| git config --list\|grep alias                          | 查看别名                                       |
| git config --global --unset alias.br                   | 取消别名                                       |
| git log --oneline --graph                              | 图形化形式查看提交日志                         |
| git log --pretty=oneline                               | 美化git提交日志                                |
| git log --pretty=oneline --abbrev-commit               | 简略形式查看提交日志                           |
| git checkout -- filename                               | 放弃某个文件的修改                             |
| git clean -n                                           | 是一次clean演习，只会提醒，不会真的clean       |
| git clean -f (-df/-xf)                                 | 删除当前目录下所有没有被track过的文件          |
| git commit --amend -m "xxx"                            | 替换上一次的提交信息                           |
| git bisect start start end                             | 二分法查找代码错误                             |
| gitk                                                   | 图形化展示git提交历史                          |
| git init [project_name]                                | 初始化一个git仓库                              |
| git config -e [--global]                               | 编辑git配置文件(本仓库/全局)                   |
| git rm --cached [file]                                 | 停止追踪某个文件，依赖保留在暂存区             |
| git commit -am "xxx"                                   | add和commit合并成一步                          |
| git log branch                                         | 查看某个分支的提交日志                         |
| git config -e                                          | 打开当前仓库的git配置文件                      |
| git push -u origin -all                                | 推送所有分支                                   |
| git config --global push.default simple                | simple模式推送（只推送当前分支）               |
| git config --global push.default matching              | matching模式推送（推送所有关联分支）           |
| git blame <file\>                                      | 指定文件在什么时候修改过                       |
| git reflog                                             | 查看当前分支最近几次提交                       |
| git fetch <remote\>                                    | 下载远程仓库的所有变动                         |
| git push <remote\> --all                               | 推送所有分支到远程仓库                         |
| git show HEAD                                          | 显示HEAD的提交日志                             |



# branch

| 命令                                                     | 说明                                         |
| -------------------------------------------------------- | -------------------------------------------- |
| git branch                                               | 列出所有的本地分支                           |
| git branch -r                                            | 列出所有的远程分支                           |
| git branch -a                                            | 列出所有的分支                               |
| git branch <branch_name>                                 | 新建分支，但依然停留在当前分支               |
| git branch `-b` <branch_name>                            | 新建分支，并切换到该分支                     |
| git branch -b <local_branch> <remote_branch>             | 检出远程分支                                 |
| git branch <branch_name> <commit_id>                     | 新建一个分支，并指向某次commit               |
| git branch --track <local_branch> <remote_branch>        | 新建一个分支，并与执行的远程分支建立追踪关系 |
| git checkout <branch_name>                               | 切换到执行分支，并更新工作区                 |
| `git checkout -`                                         | 切换到上一个分支                             |
| git fetch origin <branch_name>:<branch_name>             | 本地创建分支并拉取                           |
| git branch --set-upstream <local_branch> <remote_branch> | 将本地分支和远程分支建立追踪关系             |
| git merge <branch_name>                                  | 合并分支到当前分支                           |
| git cherry-pick <commit\>                                | 选择一个commit，合并到当前分支               |
| git push origin <origin_name>                            | 将本地分支推送到远程                         |
| git branch -d <branch_name>                              | 删除分支                                     |
| git branch -D <branch_name>                              | 强制删除分支                                 |
| git push origin --delete <branch_name>                   | 删除远程分支                                 |
| git push origin :<branch_name>                           | 删除远程分支                                 |
| git branch -dr <remote_branch>                           | 删除远程分支                                 |
| git show <branch_name>                                   | 查看某个分支最后一次提交信息                 |
| git checkout --orphan <branch_name\>                     | 新建一个独立的分支(不包括之前的提交信息)     |
| git symbolic-ref HEAD refs/heads/gh-pages                | gh-pages多页面                               |



# tag

| 命令                                     | 说明                         |
| ---------------------------------------- | ---------------------------- |
| git tag                                  | 查看所有标签                 |
| git tag <tag_name>                       | 创建轻量标签                 |
| git tag -a <tag_name> -m "\<comment\>"   | 创建附注标签                 |
| git show <tag_name>                      | 查看标签信息                 |
| git tag -a <tag_name> 9fceb02(commit_id) | 后期在之前的某次提交处打标签 |
| git push origin <tag_name>               | 推送本地标签到远程           |
| git push origin --tags                   | 推送本地所有标签到远程       |
| git tag -d <tag_name>                    | 删除本地标签                 |
| git push origin :/refs/tags/<tag_name>   | 删除远程标签（方式一）       |
| git push origin --delete <tag_name>      | 删除远程标签（方式二）       |
| git checkout <tag_name>                  | 检出标签                     |
| git checkout -b <branch_name> <tag_name> | 在某个标签处检出一个新分支   |

**检出标签**

如果想查看某个标签所指向的文件，可以使用`git checkout`命令。这样会使仓库处于分离头指针`detached HEAD`的状态，这个状态有些不好的副作用：

在"分离头指针"状态下，如果做了某些更改然后提交它们，标签不会发生变化，但新提交将不属于任何分支，并且无法访问，除非通过确切的提交哈希。因此，如果需要进行更改，比如要修复旧版本中的错误，那么通常需要新建一个分支：

```bash
git checkout -b version2 v2.0.0
```

如果在这之后又进行了一次提交，`version2`就会因为这个分支继续向前移动，此时它就会和`v2.0.0`标签稍微有些不同。



# remote

| 命令                               | 说明                   |
| ---------------------------------- | ---------------------- |
| git remote                         | 查看远程仓库名称       |
| git remote -v                      | 查看远程仓库的连接信息 |
| git remote rm origin               | 删除远程仓库           |
| git remote rename origin old       | 重命名远程仓库名称     |
| git remote add <shortname\> <url\> | 添加一个远程仓库       |
| git remote origin set-url <url\>   | 修改远程仓库的连接信息 |
| git remote add origin <url\>       | 添加远程仓库           |
| git remote show <remote\>          | 显示某个远程仓库的信息 |



# 查看信息

| 命令                                | 说明                                 |
| ----------------------------------- | ------------------------------------ |
| git diff                            | 显示工作区暂存区的差异               |
| git diff HEAD                       | 显示工作区和当前commit的差异         |
| git shortlog -sn                    | 显示提交过的用户，按照提交次数排序   |
| git blame [file]                    | 显示指定文件被什么人什么时间修改过   |
| git log -p [file]                   | 显示和指定文件有关的提交             |
| git log --follow [file]             | 查看某个文件的修改历史，包括文件改名 |
| git whatchanged [file]              | 查看某个文件的修改历史，包括文件改名 |
| git log -S [keyword]                | 按关键字搜索提交信息                 |
| git diff --shortstat "@{0 day ago}" | 显示今天提交代码量                   |



# 归档(archive)

| 命令                                                         | 说明                                       |
| ------------------------------------------------------------ | ------------------------------------------ |
| git archive -l                                               | 查看archive支持的目录                      |
| git archive --format tar.gz --output "./output.tar.gz" master | 打包并执行格式                             |
| git archive --output "./output.tar.gz" master                | 也可以不指定格式，可以根据输出文件自己判断 |
| git archive --format tar.gz --output "./output.tar.gz" test  | 打包某个分支                               |
| git archive --format tar.gz --output "./output.tar.gz" 5ca16ac0d603603 | 打包某次提交                               |
| git archive --format tar.gz --output "./output.tar.gz" master mydir mydir2 | 打包某些目录                               |



# 名词解释

## 1.HEAD

是一个指向本地工作分支的指针，可以将HEAD想象为当前分支的别名。

![HEAD](http://cdn.chenjianyin.com/markdown/HEAD.png)

## 2.Merge into Current

合并指定分支到当前分支，可以理解为current省略了this。

![image-20200424101613347](http://cdn.chenjianyin.com/markdown/image-20200424101613347.png)

当前分支test，此操作过后，dev分支合并到test分支。

## 3.git pull/fetch

git pull = git fetch + git merge



# 组合操作

## 1.关联仓库

git add .

git commit -m "xxx"

git remote add origin url

git push -u origin master

## 2.merge回滚

git checkout branch_name：切换到需要处理的分支上

git reflog：查看提交历史记录

git reset --hard commit_id：回滚到merge之前的版本号

## 3.回退远程代码

git reflog| grep branch_name：查看需要回退版本的commit_id

git reset --hard commit_id：回退代码

git push origin HEAD --force：强制提交到远程

## 4.推送分支

git checkout -b branch_name：本地新建分支

git push --set-upstream origin branch_name：推送本地分支到远程

git fetch：拉取新建的分支

git branch -d branch_name：删除本地分支

git push origin :branch_name：删除远程分支

## 5.cherry-pick

git cherry-pick commit_id：合并其他分支指定的commit_id

git cherry-pick --continue：解决冲突之后执行此命令，继续之前的合并

git cherry-pick --skip：跳过本地合并

git cherry-pick --abort：放弃本次cherry-pick

## 6.回退提交

### 6.1 本地回退

git reset --hard commit_id(可以使用git log -online查看)

### 6.2 远程回退

git push origin HEAD --force

## 7.强制覆盖本地代码

git fetch -all

git reset --hard origin/master



## 8.删除中间的某次提交

+ 找到需要删除提交的上一次提交的commit_id
+ git rebase -i commit_id
+ 进入vi模式，将需要删除提交记录前面的单词(pick)改为(drop或者d)，保存退出
+ git push origin head --force



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
* 使用github的提交统计功能时，需要保证用户名或邮箱至少有一个相等



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



# 检查与撤销修改

## 检查修改

### 已修改，未暂存

```
git diff
```

### 已暂存，未提交

```
git diff --cached
```

git diff只检查工作区和暂存区之间的差异，如果想查看暂存区和本地仓库之间的差异，需要加上--cached参数

### 已提交，未推送

```
git diff origin/master
```

origin/master代表远程仓库，git diff加上此参数之后可以查看本地仓库和远程仓库之间的差异



## 撤销修改

### 已修改，未暂存

```
git checkout .
```

或者

```
git reset --hard
```

```
git add . 和 git checkout . 是一对反义词，做完修改之后，如果想往前走一步进入暂存区，就执行git add .，如果想往后走一步，撤销刚才的更改，就执行git checkout .
```

### 已暂存，未提交

```
git reset 
git checkout .
```

或者

```
git reset --hard
```

git reset只是将修改回退到git add .之前的状态。也就是说文件本身还处于已修改未暂存的状态，如果要退回到未修改的状态，还需要执行git checkout .

### 已提交，未推送

如果既执行了git add .，又执行了git commit -m "comment"，这时候代码已经进入到本地仓库，可以执行以下命令撤销修改：

```
git reset --hard origin/master
```

origin/master代表远程仓库，既然本地仓库的代码已经被污染，就从远程仓库拉取最新无污染的代码覆盖本地仓库

### 已推送

如果已经推送了此次修改，可以先恢复本地仓库的代码，再强制推送到远程仓库即可，如下：

```
git reset --hard HEAD^
git push -f
```



# 设置

## git log 美化

git config --global alias.plog "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr)%Creset' --abbrev-commit --date=relative"



# 后悔药

git reflog



## 工作总结

> 场景：在master上修改了代码并提交推送，想把这部分代码合到dev或者test分支上

```bash
git log：查看这次提交的commit_id
git checkout dev：从master分支切换到dev分支
git cherry-pick commit_id：将刚才那一部分代码复制到dev分支上来
```



> 本地仓库和远程仓库关联

```bash
git remote add origin git@github.com:chenIU/rabbitmq.git
git push -u origin master
```



> git rebase 

+ git rebase -i HEAD~3

+ 第一个pick不能改成squash

  git rebase主要的作用是将多次提交合并为一次，或者将非线性提交改为线性提交。

**示例:**

第一种方式：

```bash
$ git checkout master
$ git rebase feature
```

这种方式是将master上所有的修改变基到feature分支上

第二种方式：

```bash
$git checkout feature
$git rebase master
$git checkout master
$git merge feature
```

这种方式是将feature上所做的提交合并到master分支上，一般不在公共分支上使用`rebase`命令。



# 标签

我们常常再代码封板时，使用git创建一个tag，这样一个不可修改的历史代码版本就像被我们封存起来一样，不论是运维发布拉取，或者以后的代码版本管理，都是十分方便的。



**git tag的功能**

git下打标签其实有两种情况：

+ 轻量级：它其实是一个独立的分支,或者说是一个不可变的分支.指向特定提交对象的引用。
+ 带附注：实际上是存储在仓库中的一个独立对象，它有自身的校验和信息，包含着标签的名字，标签说明，标签本身也允许使用 GNU Privacy Guard (GPG) 来签署或验证,电子邮件地址和日期，一般我们都建议使用含附注型的标签，以便保留相关信息

推荐使用第二种标签形式



**创建tag**

```bash
git tag -a V1.0.0 -m 'release 1.0.0'
```

上面的命令成功创建了一个本地版本V1.0.0，并且添加了附注信息'release 1.0.0'



**查看tag**

```bash
git tag
```

要显示复注信息，需要使用 show  指令查看

```bash
git show V1.0.0
```



**推送tag**

上面的标签仅仅提交到了本地git仓库，可以使用以下命令同步到远程仓库

```bash
git push origin --tags
```



**回退tag**

如果刚刚同步上去，发现了一个验中的bug，需要重新打版，可以使用如下命令

```bash
git tag -d V1.0.0
```

到这一步只是删除本地的 tag，远程仓库的 tag 还存在。这时可以推送空的同名版本tag到线上，达到删除线上tag的目的

```bash
git push origin :refs/tags/V1.0.0
```



**获取远程版本**

```bash
git fetch origin tag V1.0.0
```

这样就可以精准的拉取指定时刻的某一个版本，便于运维部署和迭代开发



**git push -u origin master**

如果当前分支与多个主机存在追踪关系，则可以使用`-u`参数指定一个默认主机，这样就可以在后面不加任何参数使用`git push`



## 发布项目到gh-pages分支

1.进入build文件夹

```bash
cd build
```

2.git初始化

```bash
git init
```

3.创建gh-pages分支

```bash
git checkout --orphan gh-pages
```

4.将文件添加到暂存区

```bash
git add .
```

5.添加提交信息

```bash
git commit -m "init"
```

6.设置远程仓库地址

```bash
git remote add origin git@github.com:chenIU/spring-boot-master.git
```

7.推送项目到gh-pages分支

```bash
git push origin gh-pages
```



# 撤销操作

撤销操作主要有以下几种：

```sh
git commit --amend：撤销上一次操作、并将暂存区文件重新提交
git checkout -- <file>：拉取暂存区文件，并将其替换成工作区文件
git reset HEAD -- <file>：拉取最近一次提交到版本库的代码到暂存区

--常用撤销操作
git reset HEAD ：将当前暂存区中所有内容还原
git checkout . ：将当前工作区中所有内容还原
```



`git pull --rebase origin dev`：拉取远程分支内容并跟随远程变基

