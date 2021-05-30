mybatis中可以使用>=，但是不能使用<=。	后者使用"\&lt;="代替

<if test="username != null">

</if>

此处的null不可以使用NULL

@Param是mybatis的注解，一般在2=<参数数<=5时使用最佳

使用<![CDATA[ ] ]标记的语句中包含的特殊字符不会被xml解析器解析

mybatis数值类型默认转换为Long类型，这点需要特别注意，否则可能出现类型转换异常

mp中and和andNew的区别是后者可以给筛选条件加上括号



> @Param
>
> + 使用@Param注解修饰的参数，xml文件中可以使用#或者$；没有使用@Param注解的参数，在xml文件中只能使用#。
> + 不使用@Param注解时，参数只能有一个，并且是JavaBean。在SQL语句中可以引用JavaBean的属性，并且只能引用JavaBean的属性。

**强制**：mapper方法参数有多个时，必须使用`@param`；如果只有一个参数，可以不使用。



**`#`传参**

`一般用户传递带表名的SQL`

`注意`：

```xml
statementType="STATEMENT"
```

`作用`：非预编译



**mybatis开启驼峰命名**


```xml-dtd
<setting name="mapUnderscoreToCamelCase" value="true" />
```



**mapper注入到spring容器**
```xml-dtd
<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
	<property name="basePackage" value="cloud.zjtlcb.cloudplat.**.*.mapper"/>
	<property name="sqlSessionFactoryBeanName" value="sqlSeesionFactory"/>
</bean>
```



# 动态sql

+ if
+ choose(when,otherwise)
+ trim(where,set)
+ foreach

如果要在注解接口中使用动态sql，需要使用`script`标签。

## set

```xml
<update id="updateStudent" parameterType="Object">
    UPDATE STUDENT
    <set>
        <if test="name!=null and name!='' ">
            NAME = #{name},
        </if>
        <if test="hobby!=null and hobby!='' ">
            MAJOR = #{major},
        </if>
        <if test="hobby!=null and hobby!='' ">
            HOBBY = #{hobby}
        </if>
    </set>
    WHERE ID = #{id}
</update>
```

使用 set+if 标签修改后，如果某项为 null 则不进行更新，而是保持数据库原值。



## trim

trim标记是一个格式化的标记，主要用于拼接sql语句(前缀或者后缀的添加或者忽略)

主要属性：

+ prefix：在trim标签内sql语句加上浅醉
+ suffix：在trim标签内sql语句加上后缀
+ prefixOverrides：指定去除多余的前缀内容，如：prefixOverrides=“AND | OR”，去除trim标签内sql语句多余的前缀"and"或者"or"。
+ suffixOverrides：指定去除多余的后缀内容。

1、update

```xml
<update id="updateByPrimaryKey" parameterType="Object">
	update student set 
	<trim  suffixOverrides=",">
		<if test="name != null">
		    NAME=#{name},
		</if>
		<if test="hobby != null">
		    HOBBY=#{hobby},
		</if>
	</trim> 
	where id=#{id}
</update>
```

2、select

```xml
<select id="selectByNameOrHobby" resultMap="BaseResultMap">
	select * from student 
	<trim prefix="WHERE" prefixOverrides="AND | OR">
		<if test="name != null and name.length()>0"> 
			AND name=#{name}
		</if>
		<if test="hobby != null and hobby.length()>0">
			AND hobby=#{hobby}
		</if>
	</trim>
</select>
```

3、insert

```xml
<insert id="insert" parameterType="Object">
    insert into student 
	<trim prefix="(" suffix=")" suffixOverrides=",">
		<if test="name != null">
			NAME,
		</if>
		<if test="hobby != null  ">
			HOBBY,
		</if>
	</trim>
	<trim prefix="values(" suffix=")" suffixOverrides=",">
		<if test="name != null  ">
			#{name},
		</if>
		<if test="hobby != null  ">
			#{hobby},
		</if>
	</trim>
</insert>				
```



## choose

**查询男性用户，如果输入姓名则按照姓名查找，如果输入年龄则按照年龄查找，否则查找名称为jack的用户**

```xml
<select id="queryUserList" resultType="com.ruida.model.User">
    select * from t_user where sex = 1
    <choose>
        <!--
		1.一旦有条件成立的when,则后续的when不再执行
		2.当所有的when都不成立,才会执行otherwise
		-->
        <when test="name!=null and name.trim()!=''">
            and name like '%#{name}%'
        </when>
        <when test="age!=null">
            and age = #{age}
        </when>
        <otherwise>
            and name='jack'
        </otherwise>
    </choose>
</select>
```



## where

```xml
<select id="queryUserList" resultType="com.ruida.model.User">
    select * from t_user
    <where>
        <!--多一个and会自动去除，如果缺少and或者多出多个and则会报错-->
        <if test="name!=null and name.trim()!=''">
            and name like '%#{name}%'
        </if>
        <if test="age!=null">
            and age = #{age}
        </if>
    </where>
</select>
```

`where 1=1`这种查询在数据量很大的时候会严重影响效率，推荐使用`<where></where>`格式。




**SqlSessionFactory**

```java
String resource = "org/mybatis/example/mybatis-config.xml";
InputStream in = Resources.getResourceAsStream(resource);
SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(in);
```

**SqlSession**

```java
try(SqlSession session = SqlSessionFactory.openSession()){
    Blog blog = (Blog)session.selectOne("org.mybatis.BlogMapper.selectBlog",1);
}
```

或者

```java
try(SqlSession session = SqlSessionFactory.openSession()){
    BlogMapper mapper = session.getMapper(BlogMapper.class);
    Blog blog = mapper.selectBlog(1);
}
```

后者代码更加清晰，而且类型更加安全。

**scope**

+ SqlSessionFactoryBuilder一次创建，后续不再需要，因此最佳作用域是方法作用域(局部方法变量)
+ SqlSessionFactory只能有一份，最佳作用域是应用作用域，可以使用单例模式或者静态单例模式
+ SqlSession每个线程都有一份，最佳作用域是请求方法作用域



# foreach



## 1 属性介绍

collection：必须和mapper.java中@param标签指定的元素名一样，参数类型可以是List、Map、Array

item：表示在迭代过程中每一个元素的别名，可以随便起，但是必须和#{}里面一样

index：表示在迭代过程中每次迭代的位置(下标)

open：前缀，sql语句中集合都必须用小括号括起来

close：后缀

separator：分隔符，表示在迭代时元素以什么分割



## 2 一个参数



### 2.1 List

mapper.java

List<User> selectByIdSet(List idList);

如果参数的类型是List，则在使用时，collection的属性值必须指定为list，和参数名称无关

<select id="selectByIdSet" resultMap="BaseResultMap">
    select 
    <include refid="Base_Column_list"/>
    from t_user
    where id in
    <foreach collection="list" item="id" index="index" open="(" close=")" separator=",">
        #{id}
    </foreach>
</select>





### 2.2 Array

mapper.java

List<User> selectByIdSet(String[] idList);

如果参数类型时Array，则在使用时，collection的属性值必须指定为array，和参数名称无关

<select id="selectByIdSet" resultMap="BaseResultMap">
    select 
    <include refid="Base_Column_list"/>
    from t_user
    where id in
    <foreach collection="array" item="id" index="index" open="(" close=")" separator=",">
        #{id}
    </foreach>
</select>


## 3 多个参数

### 3.1 @param("xxx")方式

List<User> selectByIdSet(@Param("name")String name,@Param("ids")String[] idList)

<select id="selectById" resultMap="BaseResultMap">
    select
    <include refid="Base_Column_list"/>
    from t_user
    where name = #{name}
    and id in
    <foreach collection="ids" item="id" index="index" open="(" close=")" separator=",">
        #{id}
    </foreach>
</select>


### 3.2 map方式

`map`传参，取值时使用`map`的`key`

Map<String,Object> param = new HashMap<>();

param.put("name",name);

param.put("ids",ids);

mapper.selectByIdSet(param);

<select id="selectById" resultMap="BaseResultMap">
    select
    <include refid="Base_Column_list"/>
    from t_user
    where name = #{name}
    and id in
    <foreach collection="ids" item="id" index="index" open="(" close=")" separator=",">
        #{id}
    </foreach>
</select>


# 延迟加载

**延迟加载的意义在于，虽然是关联查询，但并不是及时将关联数据查询出来，而是在需要的时候进行查询**

开启延迟加载：

```xml
<setting name="lazyLoadingEnabled" value="true"/>
<setting name="aggressiveLazyLoading" value="false"/>
```

lazyLoadingEnabled：true使用延迟加载；false禁用延迟加载。 默认是true

aggressiveLazyLoading：true启用时，当访问对象中的一个懒对象属性时，会加载这个对象的所有懒对象属性。false，当延迟加载时，按需加载对象属性(即访问对象的一个懒对象属性时，不会加载对象中的其他懒对象属性)，默认是true。



# 高级查询

**案例说明：**

此案例的关系是订单、订单详情、用户和商品的关系。其中：

一个订单只能属于一个人

一个订单可以包含多个订单详情

一个订单详情对应一个商品信息



**它们的关系是：**

订单和人是一对一关系

订单和订单详情是一对多关系

订单和商品是多对多关系



**java类：**
```java
public class Order{
    private Integer id;
    private Long userId;
    private String orderNumber;
    private Date created;
    private Date updated;
    private User user;
    private List<OrderDetail> orderDetailList;
}

public class OrderDeatil{
    private Integer id;
    private Integer orderId;
    private Integer itemId;
    private Double totalPrice;
    private Integer status;
}

public class Item {
    private Integer id;
    private String itemName;
    private Float itemPrice;
    private String itemDetail;
}
```



1.一对一

使用resultType不能自动完成结果集映射，需要使用resultMap手动映射。

```xml-dtd
<resultMap id="orderUserResultMap" type="com.ruida.model.Order" autoMapping="true">
    <id column="id" property="id"/>
    <!--association：完成子对象的映射-->
    <!--property：子对象在父对象中的属性名称-->
    <!--javaType：子对象的java类型-->
    <!--autoMapping：完成子对象的自动映射，若开启驼峰，则按照驼峰匹配-->
    <association property="user" javaType="com.ruida.model.User" autoMapping="true">
        <id column="user_id" property="id"/>
    </association>
</resultMap>

<select id="queryOrderInfo" resultMap="orderUserResultMap">
    select * from t_order o
    left join t_user u
	on o.user_id = u.id
	where o.order_number = #{number}
</select>
```

2.一对多

```xml-dtd
<resultMap id="orderUserDetailMap" type="com.ruida.model.Order" autoMapping="true">
    <id column="id" property="id"/>
    <!--collection:定义子对象集合映射-->
    <association property="user" javaType="com.ruida.model.User" autoMapping="true">
        <id column="user_id" property="id"/>
    </association>
    <collection property="orderDetailList" javaType="java.util.List" ofType="com.ruida.model.OrderDetail" autoMapping="true">
        <id column="id" property="order_id"/>
    </collection>
</resultMap>

<select id="queryOrderUserDetailInfo" resultMap="orderUserDetailMap">
    select * from t_order o
    left join t_user u on o.user_id = u.id
    left join t_order_detail od on o.id = od.order_id
    where o.order_number = #{number}
</select>
```

3.多对多

```xml-dtd
<resultMap id="OrderUserDetailItemResultMap" type="com.ruida.model.Order" autoMapping="true">
    <id column="id" property="id"/>
    <association property="user" javaType="com.ruida.model.User" autoMapping="true">
        <id column="user_id" property="id"/>
    </association>
    <collection property="orderDetail" javaType="java.util.List" ofType="com.ruida.model.OrderDetail" autoMapping="true">
        <id column="detail_id" property="id"/>
        <association property="item" javaType="com.ruida.model.Item" autoMapping="true">
            <id column="item_id" property="id"/>
        </association>
    </collection>
</resultMap>

<select id="queryOrderUserDetailItemInfo" resultMap="OrderUserDetailItemResultMap">
    select *,od.id as detail_id
    from t_order o
    left join t_user u on o.user_id = u.id
    left join t_order_detail on o.id = od.order_id
    left join t_item i on od.item_id = i.id
    where o.order_number = #{number}
</select>
```



# 缓存

## 一级缓存

### 1.什么是一级缓存

一级缓存实际上是一个依赖于SqlSession的缓存对象，通过一个k-v结构的来缓存数据。

### 2.一级缓存的生命周期

> PerpetualCache的生命周期是和SqlSession相关的，即只有在同一个SqlSession中，一级缓存才会用到。
>
> + 如果SqlSession调用了close()方法，会释放掉一级缓存PerpetualCache对象，一级缓存将不可用；
> + 如果SqlSession调用了clearCache()，会清空PerpetualCache对象中的数据，但是该对象仍可使用；
> + SqlSession中执行了任何一个update操作(update()、delete()、insert()) ，都会清空PerpetualCache对象的数据，但是该对象可以继续使用。

### 3.如何使用一级缓存

使用@Transactional可以使用一级缓存

## 二级缓存

### 1.什么是二级缓存

二级缓存是mapper级别的缓存，多个SqlSession去操作同一个Mapper的sql语句，多个SqlSession可以共用二级缓存，二级缓存是跨SqlSession的。二级缓存底层还是 HashMap 结构。

### 2.二级缓存的生命周期

+ 映射语句文件中所有的select语句将会被缓存
+ 映射语句文件中所有的update、delete和insert会刷新缓存
+ 缓存默认使用LRU(最近最少使用)算法回收缓存
+ 缓存被视为是可读可写的，意味着对象检索不是共享的，而且可以安全的被调用者修改，不干扰其他调用者或者线程所做的潜在修改。

### 3.开启二级缓存

```xml
<setting name="cacheEnabled" value="true"/>
```

开启二级缓存还必须使pojo对象实现Serializable接口，否则会抛异常。



# SQL

**group_concat**

```sql
t_user:
1	jack	57	1
2	mike	24	3
3	john	18	3
4	tom		25	3

select dept_id,group_concat(name) from t_user group by dept_id;
1	jack
3	mike,john,tom
```

**concat_ws**

添加分隔符的作用

```sql
SELECT CONCAT_WS("-", "江西省", "赣州市", "于都县");
江西省-赣州市-于都县

SELECT CONCAT_WS("-", "江西省", NULL, "于都县");
江西省-于都县

SELECT CONCAT_WS("-", NULL, "赣州市", "于都县");
赣州市-于都县

SELECT CONCAT_WS(NULL, "江西省", "赣州市", "于都县");
NULL
```

**concat**

连接的作用

```sql
SELECT CONCAT("-", "江西省", "赣州市", "于都县");
-江西省赣州市于都县
```



> mybatis-generator小技巧
>
> + 建表时，字段名称建议用"_"分隔多个单词，比如:AWB_NO、REC_ID…，这样生成的entity，属性名称就会变成漂亮的驼峰命名。
> + oracle中，数值形的字段，如果指定精度，比如Number(16,2)，默认生成entity属性是BigDecimal型 ，如果不指定精度，比如:Number(8)，指默认生成的是Long型。
> + oracle中的nvarchar/nvarchar2，mybatis-generator会识别成Object型，建议不要用nvarchar2，改用varchar2。



# 插件

## 一个接口

`Interceptor`



## 四大对象

+ `Executor`
+ `ParameterHandler`
+ `ResultSetHandler`
+ `StatmentHandler`