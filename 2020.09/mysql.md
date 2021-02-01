## mysql常用命令

| 命令               | 说明                   |
| ------------------ | ---------------------- |
| show databases;    | 查看所有数据库         |
| show tables;       | 查看某个数据库下所有表 |
| select database(); | 查看当前使用的数据库   |
| select user();     | 查看当前登录用户       |
| select version();  | 查看当前数据库版本     |

**explain**

![image-20200907103633232](http://cdn.chenjianyin.com/markdown/image-20200907103633232.png)

解释：

table：显示这一列的数据是关于哪张表的

type：这是重要的列，显示连接使用了何种类型，从好到差依次是:const、eq_reg、ref、range、index和all

possible_keys：显示可能应用在这张表中的索引。如果为空则表示没有可能的索引

key：实际使用的索引。如果为null，则没有使用索引。很少的情况下，mysql会优化不足的索引。这种情况下，可以在select语句中使用use index(index_name)来强制使用某个索引或者使用ignore index(index_name)来强制mysql忽略索引。

key_len：索引的长度。在不损失精度的情况下，越短越好

ref：显示索引的哪一列被使用了，如果可能的话，是一个常数

rows：请求数据的行数，越小越好

extra：关于mysql如何解析查询的额外信息。最坏的情况是using temporary和using filesort，这种情况下不会使用索引，结果查询会很慢



**授权**

`5.7`

```bash
grant all privilege on your_db.table_name(*) to 'user'@'localhost(%)' identified by 'your_password';
flush privileges;
```

`8.0`

```bash
use mysql;
ALTER USER 'roo'@'localhost' IDENTIFIED WITH mysql_native_password BY 'xxx';
flush privileges;
```



**事务隔离级别**

`5.7`

```bash
当前会话：select @@tx_isolation
```

```
全局：select @@global.tx_isolation
```

`8.0`

```
当前会话：select @@transaction_isolation
```

```
全局：select @@global.transaction_isolation
```



## 数据库索引为什么用B+树而不是hash表

+ hash表只能匹配是否相等，不能实现范围查找
+ 当按照索引进行order by的时候，hash值没办法实现排序
+ hash表无法支持部分索引
+ 当数据量很大时候，hash冲突的概率也会很大



## 时间



**date_forma**
时间转字符串

```sql
select date_format(now(),'%Y-%m-%d %H:%i:%s')
```

字符串格式转换

```sql
select date_format('2020-04-27','%Y-%m-%d')
```



**str_to_date**
字符串转时间

```sql
select str_to_date('2020-04-27 09:00:00','%Y-%m-%d %H:%i:%s')
```



**interval**
获取当前时间之前某天

```sql
select now() - interval xxx day
```

获取当前实际之前某小时


```sql
select now() - interval xxx hour
```



**date_add**
当前时间加一个时间间隔

```sql
select date_add(now(),interval xxx TIME.UNIT)
```



**date_sub**
当前时间减去一个时间间隔

```sql
select date_sub(now(),interval xxx TIME.UNIT)
```



**timediff**
两个时间做差

```sql
select timediff('2020-04-27 09:00:00','2020-04-27 08:00:00')
```



## mysqldiff

```bash
mysqldiff

--server1=root:123456@47.101.129.111:33061 //测试库mysql

--server2=root:123456@47.101.129.111:33062 //正式库mysql

--difftype=sql                             //差异展现形式，用sql语句，方便执行，也可用context在控制台显示

db1:db2                                    //选取要比较的数据库，或者表db1.table1:db2.table2

--force                                    //强行比较，即使发现不一致，也继续比较知道全部比较完成，不会在第一个不一致处停下来

--skip-table-options                       //忽略对engine、charset、自增id之类表选项的比较

--show-reverse                             //两个服务器的变化都要显示

--change-for=server1                       //以server2为参照，寻找server1的变化

\> /root/mysqldata/diff/1.sql              //输出文件位置
```



## 配置文件

yum方式安装的mysql配置文件的默认位置：`/etc/my.cnf`

+ port=33061 修改mysql服务的端口
+ skip-grant-tables 跳过密码验证



## 索引失效

+ like以%开头，索引失效；当like前缀没有%，后缀有%，索引有效。
+ or语句前后没有同时使用索引，当or查询左右字段只有一个是索引时，改索引失效，只有当or左右字段都为索引时，索引才会生效。
+ 数据类型出现隐式类型转换。如varchar不带单引号会自动转换为int，产生全表扫描，使索引失效。
+ 在索引字段上使用not、<>、!=。不等于操作永远不会使用索引，因此对它的操作会产生全表扫描。优化方法：key <> 0 改为 key > 0 or key < 0 。
+ 对索引字段使用计算操作、函数操作。
+ 组合索引时，不是使用第一列索引，索引失效。
+ 如果mysql觉得全表扫描更快时（数据少）。