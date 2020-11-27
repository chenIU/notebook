hostnamectl  set-hostname ‘xxx’：设置主机名称并永久生效



rpm -ivh xxx：安装某个软件

rpm -qa：查看安装过的软件

rpm -e xxx：卸载某个软件



> **nginx开机自启:**
>
> + 编辑文件
>
>   vim /etc/init.d/nginx 
>
>   脚本参考：https://www.nginx.com/resources/wiki/start/topics/examples/redhatnginxinit/
>
> + 设置权限
>
>   chmod a+x /etc/init.d/nginx
>
>   ```
>   /etc/init.d/nginx start
>   /etc/init.d/nginx stop
>   ```
>
> + 添加到chkconfig管理
>
>   chkconfig --add /etc/init.d/nginx
>
>   ```
>   service nginx start
>   service nginx stop
>   ```
>
> + 开机自启动
>
>   chkconfig nginx on



**systemctl**

| 命令                     | 解释                    |
| ------------------------ | ----------------------- |
| systemctl status mysqld  | 查看mysql服务的状态     |
| systemctl start mysqld   | 启动mysql服务           |
| systemctl stop mysqld    | 停止mysql服务           |
| systemctl restart mysqld | 重启mysql服务           |
| systemctl enable mysqld  | 将mysql设置为开机自启动 |
| systemctl disable mysqld | 取消mysql开机自启动     |

```
systemctl list-unit-files：列出所有的开机启动项
```



**yum**

| 命令                       | 解释                     |
| -------------------------- | ------------------------ |
| yum check-update           | 检查所有可更新软件       |
| yum update                 | 一次性更新所有可更新软件 |
| yum install <package_name> | 安装软件                 |
| yum remove <package_name>  | 卸载软件                 |
| yum search \<keyword>      | 按照关键字查找           |

```
yum clean all
yum makecache
当更换yum源时，需要执行上面两条命令，更新yum缓存。
```

centos下yum源配置文件路径：/etc/yum.repos.d



ln -s source target：创建软链接



**runlevel**

| id   | 解释                                                        |
| ---- | ----------------------------------------------------------- |
| 0    | 系统停机状态，系统默认运行级别不能设置为0，否则不能正常启动 |
| 1    | 单用户工作状态，root权限，用于系统维护，禁止远程登录        |
| 2    | 多用户状态，没有NFS                                         |
| 3    | 完全的多用户状态（有NFS），登录进入控制台命令行模式         |
| 4    | 系统未设置，保留                                            |
| 5    | X11控制台，登录后进入图形GUI模式                            |
| 6    | 系统正常关闭并重启，默认级别不能设置为6，否则不能正常启动   |

+ init 0：关机
+ init 6：重启



**NFS**：网络文件系统 network file system