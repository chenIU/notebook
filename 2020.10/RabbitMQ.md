## 启动命令

> 启动

```bash
rabbitmq-server -detached
```



> 停止

```bash
rabbitmqctl stop
```



> 状态

```bash
rabbitmqctl status
```





## WEB管理

> 开启web插件

```bash
rabbitmq-plugins enable rabbitmq_management
```

这一步尤其重要，否则外部无法访问。





## 用户管理

> 查看所有用户

```bash
rabbitmqctl list_users
```



> 添加一个用户

```bash
rabbitmqctl add_user chenjy 123456
```



> 配置权限

```
rabbitmqctl set_permissions -p "/" chenjy ".*" ".*" ".*"
```



> 查看用户权限

```
rabbitmqctl list_user_permissions chenjy
```



> 设置tag

```
rabbitmqctl set_user_tags chenjy administrator
```



> 删除用户(安全起见，删除默认用户)

```
rabbitmqctl delete_user guest
```



## 注意事项

+ guest用户只允许本机登录
+ rabbitmq用到两个端口，5672(实际),15672(web管理)
+ 主机名称一定要在/etc/hosts中配置的才行，使用rabbitmq不能随便修改主机名称。



## 工作模式

+ Work Queue：工作队列模式
+ Publish/Subscribe：发布订阅模式
+ Routing：路由模式
+ Topic：通配符模式
+ Header：header模式
+ RPC：远程调用模式