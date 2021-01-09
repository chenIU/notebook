## 利用docker安装mysql

**新建master数据库**

```bash
docker run --name master -p 33061:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:8.0 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```



**新建slave数据库**

```bash
docker run --name slave -p 33062:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:8.0 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```



## 授权用户

```bash
grant replication slave on *.* to 'slave'@'%' identified by '123456'
```



## 开启binlog

### master

**docker中mysql配置文件位置**：`/etc/mysql/mysql.conf.d/mysqld.conf`

```bash
log-bin=/var/lib/mysql/binlog
server-id=1
binlog-do-db=rookie
```



### slave

```bash
server-id=2
```



### 查看主机状态

```bash
show master status;
```



## 从机开启slave

### 登录容器中的mysql

+ docker exec -it slave /bin/bash
+ mysql -uroot -p



### 相关参数

```bash
change master to master_host='47.101.129.111',master_port=33061,master_user='chenjy',master_password='123456',master_log_file='binlog.000001',master_log_pos=2744;
```



### 启动slave

```bash
start slave;
```



### 查看状态

```bash
show slave status\G;
\G：竖向查看结果
```



### 关闭slave

```bash
stop slave;
```

