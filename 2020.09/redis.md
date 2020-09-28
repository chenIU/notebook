`redis`一共有五种数据类型，这里指的是value的数据结构，key只能是`string`类型

五种数据结构分别是：

+ string
+ hash
+ list
+ set
+ zset



# string

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



# hash

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



# list

+ 设置值

  lpush L1 v1 (从左边添加元素)

+ 取值

  lrange L1 0 -1

+ 设置值

  rpush L1 v2 (从右边添加元素)

+ 弹出元素

  lpop L1

  rpop L1



# set

集合中的元素不能重复

+ 添加值

  sadd S1 v1

+ 获取值

  smembers S1



# PUB/SUB

相当于消息队列

**SUBSCRIBE FOO**

**PUBLISH FOO hello**

支持通配符方式订阅频道



# 进阶



## 键

`dump` key：序列化key，并返回序列化的值
`move` key db：将当前数据库的key移动到指定db中
`randomky`：从当前数据中随机返回一个key
`enamenx` key newkey：仅当newkey不存在时，将key改名为newkey
`type` key命令可以查看指定key对应value的数据结构类型



## 字符串

`strlen` key：返回 key 对应的value的长度

`incr` key：将key所存储的数值增加1

`incrby` key increment：将key所存储的数值增加指定的数值

`decr` key：将key所存储的数值减1

`decrby` key decrement：将key所存储的数值减去指定的数值

`append` key value：当key存在且类型为string时，将value追加到原值之后

`setnx` key value：只有在key不存在时，设置key的值



## 哈希

`hkeys` key：获取指定哈希类型的key中字段的内容

`hlen` key：获取指定哈希类型的key字段的数量

`hvals` key：获取指定哈希类型的key中的所有值

`hsetnx` key field value：只有在字段field不存在时，数值哈希表的值

`hexists` key field：查看哈希类型的key中，指定的字段是否存在



## 列表

`lindex` key index：通过索引查找值

`llen` key：查看集合中元素的个数

`lset` key index value：修改值

`lrem` key count value：移除元素

+ count = 0 ：移除所有和value相等的值
+ count > 0：从表头开始向表位搜索，移除与value相等的元素，数量为count
+ count < 0：从表尾开始向表头搜索，移除与value相等的元素，数量为count的绝对值



## 集合

`scard` key：获取结合中元素的个数

`sdiff` key1 [key2]：返回第一个集合和其他集合的差集

`sintern` key1 [key2]：返回给定所有集合的交集

`sinterstore` destination key1 [key2]：返回指定所有集合的交集，并存储在destination中

`sismember` key member：判断member元素是否是集合key的成员

`srem` key member1 [member2]：移除集合中一个或多个元素

`smove` source destination member：将member元素中source集合移动到destination集合

`sunion` key1 [key2]：返回指定集合的交集

`sunionstore` destination key1 [key2]：返回指定集合的交集，并存储在destination中