## 1.环境说明

+ CentOS Linux release 8.2.2004 (Core)
+ Redis 6.2.6

```
127.0.0.1 6379
127.0.0.1 6380
127.0.0.1 6381
```

```
redis6379.conf
redis6380.conf
redis6381.conf
```



## 2.修改配置文件

```shell
port 6379
pidfile /var/run/redis_6379.pid
logfile "6379.log"
dbfilename dump6379.rdb
appendfilename "appendonly6379.aof"
```



## 3.查看信息

**mster** 节点：

```shell
127.0.0.1:6379> info replication
# Replication
role:master
connected_slaves:2
slave0:ip=127.0.0.1,port=6380,state=online,offset=112,lag=0
slave1:ip=127.0.0.1,port=6381,state=online,offset=112,lag=0
master_failover_state:no-failover
master_replid:5770d2cb4a4ab6ebe017045a5fa4c8cf26d41b01
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:112
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:112
```



**slave-01** 节点：

```shell
127.0.0.1:6380> info replication
# Replication
role:slave
master_host:127.0.0.1
master_port:6379
master_link_status:up
master_last_io_seconds_ago:4
master_sync_in_progress:0
slave_read_repl_offset:140
slave_repl_offset:140
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:5770d2cb4a4ab6ebe017045a5fa4c8cf26d41b01
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:140
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:140
```



**slave-02** 节点：

```
127.0.0.1:6381> info replication
# Replication
role:slave
master_host:127.0.0.1
master_port:6379
master_link_status:up
master_last_io_seconds_ago:2
master_sync_in_progress:0
slave_read_repl_offset:168
slave_repl_offset:168
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:5770d2cb4a4ab6ebe017045a5fa4c8cf26d41b01
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:168
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:85
repl_backlog_histlen:84
```

