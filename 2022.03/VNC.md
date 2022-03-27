**在Ubuntu中安装VNC**



## 安装vnc-server

```shell
sudo apt -y install tigervnc-standalone-server
```



## 设置密码

```shell
vncpasswd
```



## 创建桌面

```shell
vncserver :1

vncserver -kill :1
```



## 配置

配置文件路径：

`~/.vnc/xstartup`

```bash
#!/bin/sh

unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &
x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" & gnome-session &
```



## 启动

```shell
vncserver :1 geometry 1920x1080 -localhost no
```



## 下载客户端

[UltraVNC](https://uvnc.com/downloads/ultravnc.html)

