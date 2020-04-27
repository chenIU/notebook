# date_format
**时间转字符串**

```sql
select date_format(now(),'%Y-%m-%d %H:%i:%s')
```

**字符串格式转换**
```sql
select date_format('2020-04-27','%Y-%m-%d')
```

# str_to_date
**字符串转时间**

```sql
select str_to_date('2020-04-27 09:00:00','%Y-%m-%d %H:%i:%s')
```

# interval
**获取当前时间之前某天**

```sql
select now() - interval xxx day
```

**获取当前实际之前某小时**


```sql
select now() - interval xxx hour
```

# date_add
**当前时间加一个时间间隔**

```sql
select date_add(now(),interval xxx TIME.UNIT)
```

# date_sub
**当前时间减去一个时间间隔**

```sql
select date_sub(now(),interval xxx TIME.UNIT)
```

# timediff
**两个时间做差**

```sql
select timediff('2020-04-27 09:00:00','2020-04-27 08:00:00')
```









