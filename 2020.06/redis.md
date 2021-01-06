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



## 常用API

`redis`一共有五种数据类型，这里指的是value的数据结构，key只能是`string`类型

五种数据结构分别是：

+ string
+ hash
+ list
+ set
+ zset



### string

+ 设置值

  set k1 v1

+ 取值

  get k1

+ 删除值

  del k1

+ 批量设置值

  mset k1 v1 k2 v2

+ 批量取值

  mget k1 k2



### hash

+ 设置值

  hset h1 name jack

+ 取值

  hget h1 name 

+ 多次设值

  hset h1 name jack age 18

+ 一次性取多个值

  hgetall h1

+ 删除

  hdel h1

+ 删除一部分

  hdel h1 age



### list

+ 设置值

  lpush L1 v1 (从左边添加元素)

+ 取值

  lrange L1 0 -1

+ 设置值

  rpush L1 v2 (从右边添加元素)

+ 弹出元素

  lpop L1

  rpop L1



### set

集合中的元素不能重复

+ 添加值

  sadd S1 v1

+ 获取值

  smembers S1



### pub/sub

相当于消息队列

**SUBSCRIBE FOO**

**PUBLISH FOO hello**

支持通配符方式订阅频道



### 进阶



#### 键

`dump` key：序列化key，并返回序列化的值
`move` key db：将当前数据库的key移动到指定db中
`randomky`：从当前数据中随机返回一个key
`enamenx` key newkey：仅当newkey不存在时，将key改名为newkey
`type` key命令可以查看指定key对应value的数据结构类型



#### 字符串

`strlen` key：返回 key 对应的value的长度

`incr` key：将key所存储的数值增加1

`incrby` key increment：将key所存储的数值增加指定的数值

`decr` key：将key所存储的数值减1

`decrby` key decrement：将key所存储的数值减去指定的数值

`append` key value：当key存在且类型为string时，将value追加到原值之后

`setnx` key value：只有在key不存在时，设置key的值



#### 哈希

`hkeys` key：获取指定哈希类型的key中字段的内容

`hlen` key：获取指定哈希类型的key字段的数量

`hvals` key：获取指定哈希类型的key中的所有值

`hsetnx` key field value：只有在字段field不存在时，数值哈希表的值

`hexists` key field：查看哈希类型的key中，指定的字段是否存在



#### 列表

`lindex` key index：通过索引查找值

`llen` key：查看集合中元素的个数

`lset` key index value：修改值

`lrem` key count value：移除元素

+ count = 0 ：移除所有和value相等的值
+ count > 0：从表头开始向表位搜索，移除与value相等的元素，数量为count
+ count < 0：从表尾开始向表头搜索，移除与value相等的元素，数量为count的绝对值



#### 集合

`scard` key：获取结合中元素的个数

`sdiff` key1 [key2]：返回第一个集合和其他集合的差集

`sintern` key1 [key2]：返回给定所有集合的交集

`sinterstore` destination key1 [key2]：返回指定所有集合的交集，并存储在destination中

`sismember` key member：判断member元素是否是集合key的成员

`srem` key member1 [member2]：移除集合中一个或多个元素

`smove` source destination member：将member元素中source集合移动到destination集合

`sunion` key1 [key2]：返回指定集合的交集

`sunionstore` destination key1 [key2]：返回指定集合的交集，并存储在destination中



