# 常用方法

+ Arrays.asList(T... a)：将数组转成集合
+ list.toArray()：将集合转成数组



**运行时数据区**

堆、方法区、栈、本地方法栈、程序计数器



rt.jar RunTime Java运行时环境



jdk1.5之后不需要配Classpath环境变量



Set contains()的时间复杂度是O(1)，List contains()的时间复杂度是O(n)



# BigDecimal

## 1.创建

1.BigDecimal b1 = new BigDecimal(String value);

2.BigDecimal b2 = BigDecimal.valueOf(Double value);

## 2.舍入

| roundingMode | 值        | 含义                                                         |
| ------------ | --------- | ------------------------------------------------------------ |
| 0            | UP        | 远离0的方向舍入                                              |
| 1            | DOWN      | 向0方向舍入                                                  |
| 2            | CEILING   | 向正无限大方向舍入                                           |
| 3            | FLOOR     | 向负无限大方向舍入                                           |
| 4            | HALF_UP   | 向最接近的数字方向舍入，如果与两个相邻数字<br />的距离相等，则向上舍入 |
| 5            | HALF_DOWN | 向最接近的数字方向舍入，如果与两个相邻数字<br />的距离相等，则向下舍入 |
| 6            | HALF_EVEN | 向最接近数字方向舍入，如果与两个相邻数字的<br />距离相等，则向相邻的偶数舍入 |

## 3.比较

```java
BigDecimal a = new BigDecimal("0.00");
BigDecimal b = new BigDecimal("0.0");

System.out.println(a.equals(b)); //-->false
System.out.println(a.compareTo(b)); //-->true

//原因：BigDecimal的equals方法先比较scale，如果精度不同，则返回false。compareTo方法比较的是数值。
```

## 4.总结

+ 在需要精确的小数计算时再使用BigDecimal，BigDecimal的性能比double和float差，在处理庞大，复杂的运算时尤为明显。故一般精度的计算没必要使用BigDecimal。
+ 尽量使用参数类型为String的构造函数。
+ BigDecimal都是不可变的（immutable）的， 在进行每一次四则运算时，都会产生一个新的对象 ，所以在做加减乘除运算时要记得要保存操作后的值。

## 5.注意事项

```java
//这里为了提醒自己避免重复错误

//原先的代码是这样的，想着输出会是9.00,可是结果却是0.00
BigDecimal day_fee = new BigDecimal("0.00");
day_fee.add( new BigDecimal("9.00"));
System.out.print("day_fee:" + day_fee);

//正确的代码应该是这样的，输出的是9.00,BigDecimal使用方法自身不会改变，没想到居然被糊弄了
BigDecimal day_fee = new BigDecimal("0.00");
day_fee = day_fee.add( new BigDecimal("9.00"));
System.out.print("day_fee:" + day_fee);

//BigDecimal其他的方法也是具有类似情况

//附：发现了BigDecimal一个自身转负数的方法
day_fee = day_fee.negate();
```



# 双亲委派机制



## 什么是类加载器

类加载器是jre的一部分，负责动态将类加载到JVM



## 类加载器分类

+ Bootstrap classloader：加载jre/lib/rt.jar
+ Extension classloader：加载jre/lib/ext/*.jar
+ application classloader：加载classpath上指定的类库



## 双亲委派机制

双亲委派机制是指当一个类加载器收到一个类加载请求时，该类加载器首先会把请求委派给父类加载器。每个类加载器都是如此，只有在父类加载器在自己的搜索范围内找不到指定类时，子类加载器才会尝试自己去加载。



## 双亲委派工作流程

1.当Application ClassLoader 收到一个类加载请求时，他首先不会自己去尝试加载这个类，而是将这个请求委派给父类加载器Extension ClassLoader去完成。 

2.当Extension ClassLoader收到一个类加载请求时，他首先也不会自己去尝试加载这个类，而是将请求委派给父类加载器Bootstrap ClassLoader去完成。

3.如果Bootstrap ClassLoader加载失败(在<JAVA_HOME>\lib中未找到所需类)，就会让Extension ClassLoader尝试加载。 

4.如果Extension ClassLoader也加载失败，就会使用Application ClassLoader加载。 

5.如果Application ClassLoader也加载失败，就会使用自定义加载器去尝试加载。

6.如果均加载失败，就会抛出ClassNotFoundException异常。



## 设计初衷

防止替换系统级别的类



# 正则

## 元字符

| 元字符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| .      | 匹配任意单个字符除了换行符                                   |
| []     | 字符种类。匹配方括号中的任意字符                             |
| [^ ]   | 否定的字符种类。匹配除了方括号里的任意字符                   |
| *      | 匹配>=0个重复在*之前的字符                                   |
| +      | 匹配>=1个重复在+之前的字符                                   |
| ?      | 标记?出现的字符可选                                          |
| {n,m}  | 匹配num个大括号之前的字符或字符集(n <= num <=m)              |
| (xyz)  | 字符集，匹配与xyz完全相等的字符串                            |
| \|     | 或运算符，匹配符号前或后的字符                               |
| \      | 转义字符，用于匹配一些保留的字符，`[] {} () . * + ? ^ $ \ |` |
| ^      | 从开始行开始匹配                                             |
| $      | 从结束行开始匹配                                             |

## 简写字符集

| 简写 | 描述                                         |
| ---- | -------------------------------------------- |
| .    | 除换行符之外所有的字符                       |
| \w   | 匹配所有的数字和字母，等同于：`[A-Za-z0-9_]` |
| \W   | 匹配所有的非字母数字，即符号，等同于：`[\w]` |
| \d   | 匹配数字，等同于：`[0-9]`                    |
| \D   | 匹配非数字，等同于：`[^\d]`                  |
| \n   | 匹配一个换行符                               |
| \r   | 匹配一个回车符                               |
| \t   | 匹配一个制表符                               |
| \f   | 匹配一个换页符                               |



# 类型转换

int转string

```java
//第一种方式
String s = i+"";

//第二种方式
String s = Integer.toString(i);

//第三种方式
String s = String.valueOf(i);
```

string转int

```java
//第一种方式
int i = Integer.parseInt(s);

//第二种方式
int i = Integer.valueOf(s);
```



# 知识点

**Mapper和MapperScan的异同点：**

相同点：都是使mapper被spring管理

不同点：Mapper需要在每个mapper上都使用，比较麻烦。MapperScan只用声明一次即可扫描指定包下面的所有mapper。



**MapperScan可以注解多个包：**

@MapperScan({"com.ruida.demo","com.ruida.mapper"})



**mapper文件没有在spring boot主程序可以扫描的包下面：**

@MapperScan({"com.ruida.\*.mapper","org.ruida.\*.mapper"})



**HandlerInterceptorHandler**

1.preHandle在业务处理器处理请求之前被调用。预处理，可以进行编码、安全控制等处理； 

2.postHandle在业务处理器处理请求执行完成后，生成视图之前执行。后处理（调用了Service并返回ModelAndView，但未进行页面渲染），有机会修改ModelAndView； 

3.afterCompletion在DispatcherServlet完全处理完请求后被调用，可用于清理资源等。返回处理（已经渲染了页面），可以根据ex是否为null判断是否发生了异常，进行日志记录；



**ApplicationContextAware**



**spring环境中获取request**

HttpServletRequest request = 	((ServletRequestAttributes)RequestContextHolder.getRequestAttributes()).getRequest();



**SimpleDateFormat**

```java
 SimpleDateFormat sdf = new SimpleDateFormat("YYYY-MM-dd");
 Calendar c = Calendar.getInstance();
 c.set(2019,Calendar.DECEMBER,31);
 Date date = c.getTime();
 System.out.println(sdf.format(date));//输出2020-12-31
```

YYYY是ISO-8601标准，2019-12-31按周来算属于2020，所有会出现此问题。建议使用yyyy-MM-dd。

```java
 SimpleDateFormat sdf = new SimpleDateFormat("YYYY-MM-DD");
 Calendar c = Calendar.getInstance();
 c.set(2019,Calendar.DECEMBER,31);
 Date date = c.getTime();
 System.out.println(sdf.format(date));//输出2020-12-365
```

DD表示的是当前日期在本年中的哪一天，而dd表示当前日期在本月的哪一天。

> 总结：yyyy和YYYY含义不一样；dd和DD的含义也不一样。



>spring事务的传播属性
>
>+ **propagation-required**: 支持当前事务,如果有就加入当前事务中;如果当前方法没有事务,就新建一个事务;
>+ **propagation-supports**: 支持当前事务,如果有就加入当前事务中;如果当前方法没有事务,就以非事务的方式执行;
>+ **propagation-mandatory**: 支持当前事务,如果有就加入当前事务中;如果当前没有事务,就抛出异常;
>+ **propagation-requires_new**: 新建事务,如果当前存在事务,就把当前事务挂起;如果当前方法没有事务,就新建事务;
>+ **propagation-not-supported**: 以非事务方式执行,如果当前方法存在事务就挂起当前事务;如果当前方法不存在事务,就以非事务方式执行;
>+ **propagation-never**: 以非事务方式执行,如果当前方法存在事务就抛出异常;如果当前方法不存在事务,就以非事务方式执行;
>+ **propagation-nested**: 如果当前方法有事务,则在嵌套事务内执行;如果当前方法没有事务,则与required操作类似;

前六个策略类似于EJB CMT，第七个（PROPAGATION_NESTED）是Spring所提供的一个特殊变量。

> 注意事项：
>
> 前置说明：save方法调用delete方法
>
> 1)**REQUIRED**
>
>  当两个方法的传播机制都是REQUIRED时，如果一旦发生回滚，两个方法都会回滚
>
> 2)**REQUIRES_NEW**
>
> 当delete方法传播机制为REQUIRES_NEW，会开启一个新的事务，并单独提交方法，所以save方法的回滚并不影响delete方法事务提交
>
> 3)**NESTED**
>
> 当save方法为REQUIRED，delete方法为NESTED时，delete方法开启一个嵌套事务；
>
> 当save方法回滚时，delete方法也会回滚；反之，如果delete方法回滚，则并不影响save方法的提交。



TransactionDefinition：spring中关于事务转播和隔离的定义类



Integer.valueOf()：返回的值是包装类型

Integer.parseInt()：返回的基本数据类型



**类的成员变量不需要初始化，局部变量需要初始化。**



> Tree
>
> + BST 二叉搜索树 最坏的情况下时间复杂度是O(n)
>
> + AVL 自平衡二叉树 要求是左右节点的深度相差最大为1，读和写在最坏情况下都是O(logN)
>
> + Black-Red Tree 红黑树，要求：
>
>   1)根节点必须是黑节点
>
>   2)叶子节点是黑节点
>
>   3)红节点的子节点必须是黑节点
>
>   4)新入的几点是红节点
>
>   5)从相同节点上出发的路径上黑节点必须相同
>
>   红黑树的读写复杂度也是O(logN)



过滤器、拦截器、控制器的执行顺序：

filter.init()-->filter.doFilter()之前的程序-->interceptor.preHandle()-->controller-->interceptor.postHandle()-->interceptor.alterCompletion()-->filter.doFilter()之后的程序-->filter.destroy()



int 类型的1/2是0而非0.5



`Arrays.toList()：数组转集合`

`list.toArray():集合转数组`



### scope的分类

+ **compile**：默认值，它表示被依赖项目需要参与当前项目的编译和后续的测试以及运行周期，是一个比较强的依赖，打包的时候通常需要包含进去。

+ **test**：被依赖项目仅仅参与测试相关的工作，包括测试代码的编译和执行，不会被打包。 例如junit

+ **runtime**：被依赖项目无需参与项目的编译，但是后期的测试和运行周期需要其参与其中。与compile相比，跳过了编译阶段。 例如JDBC驱动

+ **provided**：打包的时候可以不用打包进去，别的设施会提供。事实上该依赖理论可以参与编译、测试、运行等周期。相当于compile，但是打包阶段做了exclude操作。

+ **system**：从参与度来说，和provided相同，不过被依赖项不会从maven仓库下载，而是从本地文件系统拿。需要添加systemPath属性来定义路径。

  

```java
@AllArgsConstructor //lombok所有参数构造方法
@NoArgsConstructor  //lombok无参构造方法
```



### Content-Type

+ application/json：消息主体是序列化之后的JSON字符串
+ application/x-www-form-urlencoded：数据被编码为键值对，这是标准的编码格式
+ multipart/form-data：需要再表单中进行文件上传时，需要使用该格式
+ text/plain：数据以纯文本形式(text/json/xml/html)进行编码，其中不好含任何控件和格式字符



`stripTrailingZeros()`：BigDecimal去掉小数点后无用的0



### stream求和

```java
long s1 = list.stream().map(Bean:getNum1).reduce(Long::sum).get();
double s2 = list.stream().map(Bean:getNum2).reduce(Double::sum).get();
```



**对集合分组**

```java
Map<String, List<Order>> treeMap = orders.stream()
                .collect(Collectors.groupingBy(Order::getName,TreeMap::new,Collectors.toList()));
```



### multipart文件上传文件过大

#### 1、yaml

```yaml
spring:
  servlet:
  	multipart:
  		#Spring Boot 2.0以上的版本MB需要大写；2.0一下的版本可以写为Mb
  		max-file-size: 10MB #单个文件最大值
  		max-request-size: 100MB #总上传最大值
  		enable: true
```



#### 2、配置bean

```java
@Configuration
public class MultipartFileConfig {
    @Bean
    public MultipartConfigElement multipartConfigElement() {
        MultipartConfigFactory factory = new MultipartConfigFactory();
        //  单个数据最大值 7Mb, 原方法 setMaxFileSize(long maxFileSize) 已经过期,建议使用 setMaxFileSize(DataSize maxFileSize)
        factory.setMaxFileSize(DataSize.ofBytes(1024 * 1024 * 10L));
        /// 总上传数据最大值 14M, 同将 setMaxRequestSize(long maxRequestSize) 方法替换为 setMaxRequestSize(DataSize 			    maxRequestSize)
        factory.setMaxRequestSize(DataSize.ofBytes(1024 * 1024 * 100L));
        // DataSize 方法属性配置建议自行查看源码
        return factory.createMultipartConfig();
    }
}
```



### 数据库加密

1、引入依赖

```xml
<dependency>
			<groupId>com.github.ulisesbocchio</groupId>
			<artifactId>jasypt-spring-boot-starter</artifactId>
			<version>1.18</version>
		</dependency>
```

2、生成密码

`java -cp jasypt-x.x.x.jar  org.jasypt.intf.cli.JasyptPBEStringEncryptionCLI input="xxx" password=e9fbdb2d3b21 algorithm=PBEWithMD5AndDES`

3、配置密码

```yaml
jasypt:
  encryptor:
    password: xxx # 盐
    
spring:
  datasource:
  	username: ENC(xxx) # 加密后的用户名
  	password: ENC(xxx) # 加密后的密码
=======
### 在xml中需要转义的字符

| 原字符 | 转义后   |
| ------ | -------- |
| `&`    | `&amp;`  |
| `<`    | `&lt;`   |
| `>`    | `&gt;`   |
| `"`    | `&quot;` |
| `'`    | `&apos;` |



### char数组和string相互转换

​```java
String str = "hello";
char[] c = str.toCharArray(); // string转char数组
String s = String.valueOf(c); // char数组转string
```



### 字符串是否都为字母

```java
public static boolean isLetter(String str){
    Pattern p = Pattern.compile("^[A-Za-z]+$");
    Matcher m = p.matcher(str);
    return m.matches();
}
>>>>>>> cb90392ec9c40afac2f5f7564b8919fbb2015245
```



### SpringBootConfiguration

#### 1、作用

+ 用来把启动类注入到容易中
+ 定义容器扫描的范围
+ 加载classpath中的一些bean

#### 2、属性

+ scanBasePackages：显示指定要扫描的包的范围
+ scanBasePackageClasses：显示指定要扫描的类
+ exclude：显示指定要排除的类
+ excludeName：显示指定要排除的类的名字



### @Configuration注解总结

+ @configuartion等价于<Beans></Beans>
+ @Bean等价于<Bean></Bean>
+ ComponentScan等价于<context:component-scan base-package="com.xxx"/>



### this

java中this指代的当前对象



```java
Character.isDigit(c)：判断字符是否为数字类型
```



生成指定范围的随机数

```java
private static int randomInt(int min,int max){
    return new Random.nextInt(max)%(max-min+1) + min;
}
```



### 异常

+ 获取异常的种类

  ```java
  e.getClass.getSimpleName();
  ```

+ 获取异常具体信息

  ```java
  e.getMessage();
  ```

  

### 注解

+ 定义注解时，`@Target`可有可无。若有，则注解只能用在它所指定的地方；若没有，注解可以用在任何地方。
+ 定义注解时，`@RentionPolicy`可有可无。默认是`RentionPolicy.CLASS。`
+ 对于返回值是数组类型的抽象方法，在声明值的时候需要用`{}`。如果只有一个值，`{}`可以省略。
+ 如果注解中只有一个抽象方法，且名称为`value()`，则在声明值时，抽象方法的名称可以省略。



### 修饰符

|               | 类内部 | 本包 | 子类 | 外部包 |
| ------------- | ------ | ---- | ---- | ------ |
| **public**    | ✔      | ✔    | ✔    | ✔      |
| **protected** | ✔      | ✔    | ✔    | ❌      |
| **default**   | ✔      | ✔    | ❌    | ❌      |
| **private**   | ✔      | ❌    | ❌    | ❌      |



**Method Reference**



**java数据类型**

![20140531091306906](http://cdn.chenjianyin.com/markdown/java_data_type.jpg)



## Validator

**JSR提供的校验注解** 		`jSR(Java Specification Requests) Java规范请求`

| 注解                      | 解释                                                   |
| ------------------------- | ------------------------------------------------------ |
| @Null                     | 作用的元素必须是null                                   |
| @NotNull                  | 作用的元素必须不是null                                 |
| @AssertTrue               | 作用的元素必须是true                                   |
| @AssertFalse              | 作用的元素必须是false                                  |
| @Min(value)               | 作用的元素必须是一个数字，其值必须大于等于指定的值     |
| @Max(value)               | 作用的元素必须是一个数字，其值必须小于等于指定的值     |
| @DecimalMin(value)        | 作用的元素必须是一个数字，其值必须大于等于指定的值     |
| @DecimalMax(value)        | 作用的元素必须是一个数字，其值必须小于等于指定的值     |
| @Size(max = ,min =)       | 作用的元素大小必须在指定的范围内                       |
| @Digit(integer,fraction)  | 作用的元素大小必须是一个数字，其值必须在可接受的范围内 |
| @Past                     | 作用的元素必须是一个过去的日期                         |
| @Future                   | 作用的元素必须是一个将来的日期                         |
| @Pattern(regex = ,flag =) | 作用的元素必须符合指定的正则表达式                     |



**Hibernate Validator提供的校验注解**

| 注解                            | 解释                                  |
| ------------------------------- | ------------------------------------- |
| @NotBlank(message = )           | 验证字符串非null，且trim后的长度大于0 |
| @Email                          | 作用的元素必须是电子邮箱地址          |
| @Length(min = ,max = )          | 被注解的字符串长度必须在指定的范围内  |
| @NotEmpty                       | 被注解的字符串必须非空                |
| @Range(min = ,max = ,message =) | 被注解的元素必须在合适的范围内        |



## redis存储对象的三种方式

+ 序列化操作
+ 使用fastjson将对象转为json字符串后存储
+ 使用hash数据类型



**Spring Cache是Java世界中所有缓存的门面**



## Spring Boot中的日志

+ 门面（Apache commons-logging、SLF4j）
+ 具体实现(java.util.logging、log4j、logback)



`Spring 实例化bean默认是非懒加载形式`



@Lazy = true 懒加载，false 非懒加载。默认值是true



## 线程主要方法

![image-20201126171115029](http://cdn.chenjianyin.com/markdown/thread.png)

+ sleep()：让线程休眠，交出CPU，让CPU执行其他任务。但是需要注意的是sleep不会释放锁
+ yield()：让出CPU权限，和sleep()类似。不同的是，yield不能控制交出CPU的具体时间，另外yield只能让处于相同优先级的线程获得CPU时间片的机会，而且不会让线程进入阻塞状态，而是重新进入就绪状态。
+ wait()：让线程处于waiting状态，会释放锁，是object的方法。
+ join()：实际上利用了wait()，只不过不需要notify/notifyAll唤醒，且不受此影响。它结束的条件是：
  + 等待时间到
  + 线程执行完毕（通过isAlive()）判断
+ interrupt()：此方法会将线程的终端标志位置为true
  + 如果线程处于阻塞状态，那么线程会定时检查中断标志位，如果终端标志位是true，则会在阻塞方法调用处抛出InterruputedException。并且在抛出异常之后立刻将线程终端标志位清除，重新设置为false。抛出异常是为了让线程从中断状态中醒来，并且在线程结束前让程序员有足够的时间处理终端请求。
  + 如果线程正在运行，争用synchronized，lock等，那么是不可中断的，它们会忽略。
+ suspend()/resume()：挂起线程，知道resume，才会苏醒。但是suspend线程和resume线程可能因为争锁问题发生死锁，所以在JDK1.7之后不推荐使用。

**注意**：park/wait/join方法都会进去wait状态，但是wait/join方法进入的其他线程调用interrupt()，会排除异常，park则不会。



**split**需要转义的字符：`|.+*^?[\\{()$`



**回车和换行**

`CR`：回车 （Carriage Return）

`LF`：换行  （Line Feed）

+ `\r`：回车，使光标移动到行首
+ `\n`：换行，使光标移动到下一行
+ `Enter`是两者的结合

**不同操作系统换行的区别:**

+ Windows：CRLF
+ Unix：LR
+ Mac：CR



`\t`：制表符



## 拦截器和过滤器的区别

+ 拦截器基于Java的反射实现，过滤器基于函数回调；
+ 拦截器不依赖于servlet容器，过滤器依赖于servlet容器
+ 拦截器只能对action请求起作用，过滤器可以对几乎所有的请求起作用
+ 拦截器可以访问action上下文、值栈中的对象，而过滤器不能
+ 在action的生命周期中，拦截器可以多次被调用，而过滤器只能再容器初始化时被调用一次
+ 拦截器可以获取IoC容器中的各个bean，而过滤器不能
+ 过滤器是Serlvet规范规定的，之恶能用用户Web程序中。拦截器既可以适用于Web程序，也可用于Application、Swing程序
+ 过滤器只能在Servlet容器前后起作用，而拦截器能够深入到方法前后、异常抛出前后。所以在Spring框架程序中，优先使用拦截器



## 各种数据对象之前的区别

+ PO（persistant object）：持久层对象，对应数据库中的表
+ DTO（data transfer object）：数据传输对象，一是可以减少数据的传输，二是可以隐藏后端表结构
+ POJO（plain ordinary java object）：简单无规则的Java对象，属性加上get、set方法
+ VO（value object）：值对象，对于一个web页面将整个页面的属性封装成一个对象，然后用一个VO对象在控制层和视图层进行传输交换



## JVM 内存分配

```bash
export JAVA_OPTS="$JAVA_OPTS -Xms5000m -Xmx6000m -XX:PermSize=1024m -XX:MaxPermSize=2048m
```

+ -Xms：最小内存分配
+ -Xmx：最大内存分配
+ -XX:PermSize：JVM启动时初始大小
+ -XX:MaxPermSize：JVM启动后可分配的最大空间



**spring boot项目带参数启动**

```bash
java -jar -Dspring.config.location=./application.yml --spring.profiles.active=test --server.prot=8080 
```

+ spring.config.location：指定配置文件的位置
+ spring.profiles.active：指定要使用的配置文件
+ server.port：指定端口（**=两边不能有空格**）



**错误日志打印**

```java
// 一个参数的类型string
log.error(String msg);
// 两个参数的重载方法可以转入异常对象本身，打印堆栈信息
log.error(String msg, Throwable t);
```



## Spring Boot logging

```yaml
logging:
	file: # 日志文件，绝对路径或相对路径
	path: # 保存日志文件目录
	config: # 日志配置文件，Spring Boot 默认使用classpath路径下的日志配置文件，如：logback.xml
	level:
		org.springframework.web: DEBUG # 日志级别
```



## Spring Boot 配置文件优先级

1. 项目根目录的config目录中配置文件
2. 项目根目录下配置文件
3. classpath路径下config目录中的配置文件
4. classpath路径下配置文件



## @Value

```java
@Value("${outsystem.url:}")
private String url;
```

使用`@Value`注解获取配置项时，最好使用`:`指定缺省值，这样在不配置的时候也不会报错。



## 文件路径

```java
@PropertySource(value = {"classpath:config/mysql.properties"})
```



## final

1. 修饰类，则这个类不能被继承
2. 修饰方法，则这个方法不能被重写
3. 修饰变量，如果是普通数据类型，则初始化之后不能被修改；如果是应用类型变量，则在对其初始化之后便不能再让其指向另一个对象



## @Primary

一个类有多个实现类时，使用此注解标注优先加载某个类



## 函数式接口

| 接口名称        | 主要方法          |
| --------------- | ----------------- |
| Consumer\<T\>   | void accept(T t)  |
| Supplier\<T\>   | T get()           |
| Function\<T,R\> | R apply(T t)      |
| Predicate\<T\>  | boolean test(T t) |



`this`关键字会导致spring注解失效，`@Transactional`、`@Async`失效都包含这种情况。
