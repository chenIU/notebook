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