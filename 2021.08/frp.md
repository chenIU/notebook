## 下载

[releases](https://github.com/fatedier/frp/releases)



## 配置



### 服务端配置

```shell
bind_port = 19007
vhost_http_port = 19006
privilege_token= chenjianyin

dashboard_port = 7500
dashboard_user = admin
dashboard_pwd = 123456
```

**启动**：

`nohup ./frps -c frps.ini &`



### 客户端配置

```shell
[common]
server_addr = 47.101.129.111
server_port = 19007

[web]
type = http
local_port = 8080
custom_domains = chenjianyin.com
```

**启动**：

`./frpc -c frpc.ini`