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



`type key`命令可以查看指定key对应value的数据结构类型