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