常见的日志框架和`slf`门面的关系：

|                 | log4j            | log4j2           | logback         |
| --------------- | ---------------- | ---------------- | --------------- |
| 是否实现slf门面 | 否               | 否               | 是              |
| 适配器          | slf4j-log4j12    | log4j-slf4j-impl | logback-classic |
| 桥接            | log4j-over-slf4j | log4j-to-slf4j   | 已实现slf4j     |
| 性能            | 低               | 高               | 中              |

> 适配器就是由具体的日志实现方式来实现 `slf`门面模式
>
> 桥接器是对某套API（`slf4j`）的伪实现，这种实现并不是直接完成API所声明的功能，而是去调用有类似功能的别的API



Spring 默认采用`jcl`（门面），`jul`（实现）



Spring Boot 默认采用`logback`



`jul` java.util.logging

`jcl` jakarta.common.logging



**日志级别**

`debug` < `info` < `warn` < `error` < `fatal`



**log4j2核心依赖**

```xml
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-api</artifactId>
    <version>${log4j.version}</version>
</dependency>
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-core</artifactId>
    <version>${log4j.version}</version>
</dependency>
```

> `log4j-api` 提供接口，`log4j-core` 是实现包



**调用**

1. log4j

   ```java
   private final Logger logger = Logger.getLogger();
   ```

2. log4j2

   ```java
   private static Logger logger = LogManager.getLogger();
   ```

3. logback

   ```java
   private final static Logger logger = LoggerFactory.getLogger();
   ```

   