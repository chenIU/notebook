常见的日志框架和`slf`门面的关系：

|                 | log4j            | log4j2           | logback         |
| --------------- | ---------------- | ---------------- | --------------- |
| 是否实现slf门面 | 否               | 否               | 是              |
| 适配器          | slf4j-log4j12    | log4j-slf4j-impl | logback-classic |
| 桥接            | log4j-over-slf4j | log4j-to-slf4j   | 已实现slf4j     |
| 性能            | 低               | 高               | 中              |



Spring 默认采用`jcl`（门面），`jul`（实现）



Spring Boot 默认采用`logback`



`jul` java.util.logging

`jcl` jakarta.common.logging