## 常用命令

```shell
mongo localhost:27017 #连接mongo数据库
help #查看帮助命令
use admin #切换/创建数据库
db.auth("username", "password") #认证
show dbs # 查看数据库
db.createCollection("xxx") #创建集合
db.dropDatebase() #删除当前使用数据库
db.getName() #查看当前数据库名称
db.version() #查看版本
db.addUser("username", "password", true/false) #添加用户，设置密码，是否只读
show users #显示当前所有用户
db.removeUser() #删除用户
db.(xxx).find() #查询集合数据
```

