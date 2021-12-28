## 安装

```
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
iwr -useb get.scoop.sh | iex
```



## 常用命令

```bash
scoop help #查看帮助
scoop help <某个命令> #查看具体某个scoop命令的帮助

scoop install <app> #安装软件
scoop uninstall <app> #卸载软件

scoop list #列出已安装的软件
scoop search <app> #查询某个软件
scoop status #检查哪些软件需要更新

scoop update #更新scoop自身
scoop update * #更新所有需要更新的软件
scoop update <app1> <app2> #更新某些特定的软件

scoop bucket known #列出所有已知的bucket(软件源)
scoop bucket add <bucketName> #添加某个bucket

scoop cache rm <app> #移除某个软件的缓存
```



## 更新软件

```bash
#更新软件
scoop update <app>

#禁止更新
scoop hold <app>

#允许更新
scoop unhold <app>
```



## 清除缓存与旧版本

```bash
#查看所有已下载的缓存信息
scoop cache show

#清除指定程序的下载缓存
scoop cache rm <app>

#清除所有缓存
scoop cache rm *

#删除某软件的旧版本
scoop cleanup <app>

#删除全局安装的某软件的旧版本
scoop clean <app> -g

#删除过期的下载缓存
scoop clean <app> -k
```



## 别名

```bash
#可用的操作
scoop alias add|list|rm [<args>]

#添加别名,格式:
scoop alias add <name> <command> <description>

#添加别名,示例:
scoop alias add st 'scoop status' '检查更新'

#检查已添加的别名
scoop alias list -v

#另一个示例
scoop alias add rm 'scoop uninstall $args[0]' '卸载app'
```



## 版本切换

```
scoop reset [app]@[version]

#示例
scoop reset idea-ultimate-eap@201.6668.13

scoop reset idea-ultimate-eap@201.6073.9

#切换到最新版本
scoop reset idea-ultimate-eap
```



## 软件源

scoop可安装的软件信息存储在bucket中，也可以称为软件源。scoop默认的bucket为`main`;官方维护的另一个bucket为`extras`，需要我们手动添加。

```bash
#bucket的用法
scoop bucket add|list|known|rm [<args>]
```

添加extras：

```
scoop bucket add extras
```

添加第三方bucket：

```
scoop bucket add dorado https://github.com/h404bi/dorado
```

常见软件源：`extras`、`nirsoft`、`dorado`、`Ash258`、`nerd-fonts`、`java`、`version`



## aria2断点续传

```
aria2c.exe --input-file='D:\Scoop\Applications\cache\vscode-portable.txt'

--input-file在错误提示中会出现

scoop update <app>
```



## 切换版本

```bash
#需要先安装此仓库
scoop bucket add versions

#安装最新python(python3)
scoop install python

#安装python2
scoop install python27 python

#由python3切换到python2
scoop reset python27

#由python2切换到python3
scoop reset python
```



## 其他命令

```
#显示某个app的信息
scoop info <app>

#在浏览器中打开某个app的主页
scoop home <app>

#检查当前环境存在的问题
scoop checkup
```

