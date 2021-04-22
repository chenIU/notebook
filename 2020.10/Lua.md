### 1.基本用法

**1.1 EVAL script numbers key [key ...] arg [arg...]**

numbers是key的个数,后面接着写key1,key2...,val1,val2...,举例

```bash
127.0.0.1:6379> eval "return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}" 2 key1 key2 val1 val2
1) "key1"
2) "key2"
3) "val1"
4) "val2"
```

**1.2 SCRIPT LOAD script**

把脚本加载到脚本缓存中，返回SHA1校验和。但不会立马执行，举例

```bash
127.0.0.1:6379> SCRIPT LOAD "return 'hello world'"
"5332031c6b470dc5a0dd9b4bf2030dea6d65de91"
```

**1.3 EVALSHA sha1 numbers keys [key...] arg [arg...]**

根据缓存码执行脚本内容，举例

```bash
127.0.0.1:6379> SCRIPT LOAD "return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}" 
"a42059b356c875f0717db19a51f6aaca9ae659ea"
127.0.0.1:6379> EVALSHA "a42059b356c875f0717db19a51f6aaca9ae659ea" 2 key1 key2 val1 val2
1) "key1"
2) "key2"
3) "val1"
4) "val2"
```

**1.4 SCRIPT EXISTS script [script...]**

通过sha1校验和判断脚本是否在缓存中

```bash
127.0.0.1:6379> SCRIPT EXISTS a42059b356c875f0717db19a51f6aaca9ae659ea
```

**1.5 SCRIPT FLUSH**

清空缓存

```bash
127.0.0.1:6379> SCRIPT LOAD "return 'hello jihite'"
"3a43944275256411df941bdb76737e71412946fd"
127.0.0.1:6379> SCRIPT EXISTS "3a43944275256411df941bdb76737e71412946fd"
1) (integer) 1
127.0.0.1:6379> SCRIPT FLUSH
OK
127.0.0.1:6379> SCRIPT EXISTS "3a43944275256411df941bdb76737e71412946fd"
1) (integer) 0
```

**1.7 SCRIPT KILL**

杀死正在执行的脚本



### 2.实战

直接在redis-cli中写脚本非常不方便，通常情况下是将lua脚本写在一个文件中，然后执行这个lua脚本。示例

```lua
if redis.call("EXISTS",KEYS[1])==1 then
    return redis.call("INCRBY",KEYS[1],ARGV[1])
else return nil
end

```

> 存储位置：/root/lua/incr.lua

> 执行

```bash
redis-cli --eval -p 16379 -a 123456 /root/lua/incr.lua age , 1
```

>注意事项

KEY和ARGV之间(age , 1)一定要有空格，否则会导致执行失败。



`cat delete.lua | redis-cli -p 16379 -a 123456 script load --pipe：将lua脚本缓存到redis中`



**释放锁脚本**

```lua
if redis.call('get',KEYS[1]) == ARGV[1] then return redis.call('del',KEYS[1]) else return 0 end)
```

