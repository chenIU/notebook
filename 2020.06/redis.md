redis.conf常用配置文件：
| 配置               | 解释                                                         |
| ------------------ | ------------------------------------------------------------ |
| bind 127.0.0.1     | 只接收来自于该IP地址的请求，如果不进行设置，那么将处理所有请求。 |
| protected-mode yes | 开启该参数后，redis只会本地进行访问， 拒绝外部访问。         |
| port 6379          | redis监听的端口号                                            |
| daemonize yes      | yes：后台运行；no：不是后台运行                              |
| databases 16       | 数据库的数量，默认使用的数据库是0。                          |
| appendonly yes     | 开启aof持久化                                                |
| requirepass xxx    | 设置密码                                                     |

