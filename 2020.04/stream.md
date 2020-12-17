# stream

https://www.cnblogs.com/jimoer/p/10995574.html



## 0.stream常用方法

### 求和

**BigDecima**

```java
BigDecimal totalAmount = userList.stream.map(User::getAmount).reduce(BigDecimal.ZERO,BigDecimal::add);
```

**int doule long**

```java
double sum = userList.stream.mapToDouble(User::getHeight).sum();
```

`mapToDouble`，`mapToInt`，`mapToLong`

**空指针**

```java
double sum = userList.stream.filter(user -> StringUtils.isEmpty(user.getHeight)).mapToDouble(User::getHeight).sum();
```

解决思路：用filter过滤



## 1.创建stream

1、Arrays.stream()

2、Stream.of()

3、Stream.generate()

4、Stream.iterate()

5、Collections.stream()

6、StreamSupport.stream()



## 2.流的转换

### filter

```java
List<Integer> list = integerList.stream().filter(i->i>50).collect(Collectors.toList());
```

### map

```java
List<String> afterString = integerList.stream().map(i->String.valueOf(i)).collect(Collectors.toList());
```

### flatMap

```java
List<Stream<Integer>> list = testMap.values().stream().map(number->number.stream()).collect(Collectors.toList());
```

### limit

limit(n)方法会返回一个包含n个元素的新的流（若总长小于n则返回原始流）。

```java
List<Integer> afterLimit = rawList.stream().limit(n).collect(Collectors.toList());
```

### skip

skip(n)方法正好相反，它会丢弃掉前面的n个元素。

```java
List<Integer> afterSkip = rawList.stream().skip(n).collect(Collectors.toList());
```

### distinct

根据原始流中的元素返回一个具有相同顺序、去除了重复元素的流。

```java
List<Integer> distinctList = rawList.stream().distinct().collect(Collectors.toList());
```

### sorted

是需要遍历整个流的，并在产生任何元素之前对它进行排序。

```java
List<Integer> sortedList = rawList.stream().sorted(Integer::compareTo).collect(Collectors.toList());
```



## 3.聚合操作

### max

```java
Integer maxItem = rawList.stream().max(Integer::compareTo).get();
```

### min

```java
Integer minItem = rawList.stream().min(Integer::compareTo).get();
```

### findFirst

返回非空集合中的第一个值，它通常与filter方法结合起来使用。

```java
Integer firstItem = rawList.stream().filter(i->i>100).findFirst().get();
```

### findAny

可以在集合中只要找到任何一个所匹配的元素，就返回，此方法在对流并行执行时十分有效（任何片段中发现第一个匹配元素都会结束计算，串行流中和findFirst返回一样)。

```java
Integer anyItem = rawList.stream().filter(i->i>100).findAny().get();
```

### anyMatch

可以判定集合中是否还有匹配的元素。返回结果是一个boolean类型值。

```java
boolean flag = rawList.stream().anyMatch(i->i>100);
```

### allMatch

所有元素都匹配时返回true

```java
boolean flag = rawList.parallelStream().allMatch(i->i>100);
```

### noneMatch

没有元素匹配时返回true

```java
boolean flag = rawList.parallelStream().noneMatch(i->i>100);
```



## 4.收集结果

### 收集到集合

```java
//收集到list
List<Integer> list = rawList.stream().collect(Collectors.toList());

//收集到set
Set<Integer> list = rawList.stream().collect(Collectors.toSet());

//指定类型
TreeSet<Integer> treeSet = rawList.stream().collect(Collectors.toCollection(TreeSet::new))
```



### 拼接

将字流中的字符串连接并收集起来

```java
String result = rawList.stream().collect(Collectors.joining());
```

在将流中的字符串连接并收集起来时，想在元素中介添加分隔符，传递个joining方法即可。

```java
String result = rawList.stream().collect(Collectors.joining(","));
```

当流中的元素不是字符串时，需要先将流转成字符串流再进行拼接。

```java
String result = rawList.stream().map(String::valueOf).collect(Collectors.joining(","));
```

### 收集聚合

```java
int sum = rawList.stream().collect(Collectors.sumingInt(Integer::intValue);

Double ave = rawList.stream().collect(Collectors.averagingInt(Integer::intValue));

Integer max = rawList.stream().collect(Collectors.maxBy(Integer::compare)).get();       
                                   
Integer min = rawList.stream().collect(Collectors.minBy(Integer::compare)).get();                           
```

### 将结果收集到Map

```java
Map<Double,Double> map = roomList.stream().collect(Collectors.toMap(Room::getHeight,Room::getWidth));
```

### 分组

```java
Map<Double,List<Room>> groupMap = roomList.stream().collect(Collectors.groupingBy(Room::getWidth));
```

### 分片

```java
Map<Boolean,List<Room>> partitionMap = roomList.stream().collect(Collectors.partitioningBy(room->Room::getHeight==3));
```

## 5.扩展功能

### counting

返回收集元素的总个数

```java
Map<Double,Long> countMap = roomList.stream().collect(Collectors.groupingBy(Room:getHeight,Collectors.counting()));
```

### summing

```java
Map<Double,Double> sumMap = roomList.stream().collect(Collectors.groupingBy(Room::getWidth,Collectors.sumingDouble(Room:getHeight)));
```

### maxBy

### minBy

### mapping

### 多级分组

```java
Map<Double,Map<Double,List<Room>>> multiMap = roomList.stream().collect(Collectors.groupingBy(Room:getHeight,Collectors.groupingBy(Room:getWidth));
```

### 并行流

```java
Stream.of(roomList).parallel();
```