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



## redis常见问题及解决方法

### 1.缓存雪崩

一般是由于redis服务宕机或者redis中的key同时失效

解决方案：

+ 搭建高可用的redis集群
+ 对不同的数据使用不同的过期时间

### 2.缓存穿透

指使用不存在的key进行高并发访问，导致无法命中，每次请求都要穿透到后端数据库进行查询。

解决方案：

+ 缓存空置
+ 布隆过滤器

### 3.缓存击穿

指缓存中没有但是数据库中有(一般是缓存时间到期)，这时由于并发用户特别多，同时读缓存没有读取到数据，同时读数据库，造成数据库压力瞬间增大。

+ 互斥锁
+ jvm锁
+ 如果是分布式部署则要采用分布式事务锁



## Redis内存问题

### 修改内存大小

**1.通过配置文件配置**

```
//设置Redis最大占用内存为100M
maxmemory 100mb
```

**2.通过命令修改**

Redis支持运行时动态修改内存大小

```bash
//设置Redis最大占用内存大小
127.0.0.1:26379>config set maxmemory 100mb

//获取能使用的最大内存大小
127.0.0.1:26379> config get maxmemory
```



### Redis内存淘汰策略

+ noeviction(默认)：对于写请求不再提供服务，直接返回错误(DEL和部分请求除外)
+ allkeys-lru：对于所有的key使用LRU算法进行淘汰
+ volatile-lru：在设置了过期时间的key中使用LRU算法进行淘汰
+ allkeys-random：从所有的key中随机淘汰数据
+ volatile-random：从设置了过期时间的key中随机淘汰数据
+ volatile-ttl：在设置了过期时间的key中，根据key的过期时间进行淘汰，越早过期的越优先被淘汰

> 当使用volatile-lru、volatile-random、volatile-ttl这三种策略时，如果没有key可以被淘汰，则和noeviction一样返回错误



**设置和获取内存淘汰策略**

获取当前内存淘汰策略

```bash
127.0.0.1:26379> config get maxmemory-policy
```

通过配置文件修改淘汰策略

```
mammemory-policy allkeys-lru
```

通过命令行修改淘汰策略

```bash
127.0.0.1:26379> config set maxmemory-policy allkeys-lru
```



Redis使用的是近似LRU算法，每次随机选出5（默认）个key，从里面淘汰最近最少使用的key。

> maxmemory-samples配置的越大，Redis中LRU淘汰策略越接近严格的LRU算法。









