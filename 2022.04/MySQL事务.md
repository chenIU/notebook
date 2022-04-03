**隔离级别**

|                      | 脏读 | 不可重复读 | 幻读 |
| -------------------- | ---- | ---------- | ---- |
| Read Uncommitted(RU) | ✔    | ✔          | ✔    |
| Read Committed(RC)   | ❌    | ✔          | ✔    |
| Repeatable Read(RR)  | ❌    | ❌          | ✔    |
| Serializable         | ❌    | ❌          | ❌    |



`脏读`：事务A对资源X进行写，当A发生异常回滚时，事务B读到数据可能为脏数据，此时事务B有脏读问题。



`不可重复读`：同一个事务中，对于同一条数据，多次 读取到的内容不一致



`幻读`：同一个事务中，多次读取的条数不一致



[Link](https://www.bilibili.com/video/BV1ya411t7H4)