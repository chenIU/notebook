## 下载

```bash
wget https://github.com/aristocratos/btop/releases/download/v1.0.9/btop-1.0.9-linux-x86_64.tbz
```



## 解压

```bash
yum install bzip2 -y
mkdir btop
mv btop-1.0.9-linux-x86_64.tbz btop
cd btop
bunzip2 btop-1.0.9-linux-x86_64.tbz
tar xf btop-1.0.9-linux-x86_64.tar
```



## 安装

```bash
make install PREFIX=/opt/btop
```



## 启动

```bash
#默认
/opt/btop/bin/btop --utf-force

#TTY默认，看上去比较鲜艳一些
/opt/btop/bin/btop --utf-force -t
```



## 功能

```
比较有用的是右下角这一块，，会显示出进程的线程数，使用的内存，CPU等直观的数据

MemB列显示内存使用具体多少，Cpu%例显示cpu使用率多少，轻松定位CPU高，内存高的进程

同时还支持过滤进程,在进程较多时比较有用，先按f 然后再输入想找的进程名(模糊查询)
```



## 帮助

```
打开界面后，按h就可以打开帮助页面，详细的功能指南, 再次按h退出帮助

如果要退出整个界面，按q
```

