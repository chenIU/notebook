## vmware设置

1. 设置界面

   ![image-20210820093058906](http://cdn.chenjianyin.com/markdown/jtip-1.png)

   2. NAT设置

      ![image-20210820093151139](http://cdn.chenjianyin.com/markdown/jtip-2.png)

## 网卡设置

1. 设置界面

   ![image-20210820093312267](http://cdn.chenjianyin.com/markdown/jtip-3.png)

2. 具体设置

   ![image-20210820093344937](http://cdn.chenjianyin.com/markdown/jtip-4.png)

3. 重新连接

   ![image-20210820093425031](http://cdn.chenjianyin.com/markdown/jtip-5.png)

## 配置文件

路径：`/etc/sysconfig/network-scripts`

```
PROXY_METHOD=none 
BROWSER_ONLY=no
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
UUID=882b023e-01ac-44bf-b044-df92f3af27c5
DEVICE=ens33

BOOTPROTO=static #设置为静态IP
ONBOOT=yes #开机自动启动
DNS1=192.168.1.2
TYPE=Ethernet #网络类型
IPADDR=192.168.1.102 #IP地址
NETMASK=255.255.255.0 #子掩码
GATEWAY=192.168.1.1 #网关
```

