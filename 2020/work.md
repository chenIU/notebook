# 码值



## 数据库

| 环境 |账号  | 密码        | ip |
| ---- | ----- | ----------- | ---- |
| 开发 | ruida | Ruida@2019  | 118.31.42.188 |
| 测试 | ruida | Ruida@2019  | 47.97.223.42 |
| 预发 | ruida | Ruida@2019  | 47.110.233.39 |
| 开发 | root | James627304 | 118.31.42.188 |
| 测试 | root  | James627304 | 47.97.223.42 |
| 预发 | root  | Ruida!2019? | 47.110.233.39 |



## userId

| env       | id    |
| --------- | ----- |
| dev       | 2037  |
| test      | 2275  |
| preonline | 23202 |



## teachingMehod

| id   | name         |
| ---- | ------------ |
| 0    | 双师直播     |
| 1    | 录播课       |
| 2    | 双师线下     |
| 3    | 直播课(线上) |



## findType

| id   | name | 对应teachingMethod |
| ---- | ---- | ------------------ |
| 0    | 双师 | 0和2               |
| 1    | 录播 | 1                  |
| 2    | 线上 | 3                  |



## orderStatus

| key  | value  |
| ---- | ------ |
| 0    | 未支付 |
| 1    | 已支付 |
| 2    | 已关闭 |
| 3    | 待确认 |
| 4    | 退费中 |
| 5    | 已退费 |



## roleType

| id   | name       |
| ---- | ---------- |
| 0    | 超级管理员 |
| 1    | 部门管理员 |
| 2    | 教师       |
| 3    | 学生       |
| 4    | 游客       |
| 5    | 其他       |



## isDelete

| id   | name   |
| ---- | ------ |
| 0    | 未删除 |
| 1    | 已删除 |



## orderType

| key  | value      |
| ---- | ---------- |
| 0    | 单课程订单 |
| 1    | 图书订单   |
| 2    | 组合课订单 |



## menuType

| id   | name |
| ---- | ---- |
| 0    | 目录 |
| 1    | 菜单 |
| 2    | 按钮 |
| 3    | 字段 |



## 班级类型：启迪班、创新班、探究班、精品班



## 课程类型：同步课、测试课、答疑课、正式课、试听课

---



# http请求方法

| 请求方式 | 是否满足幂等性 |
| -------- | -------------- |
| GET      | 是             |
| POST     | 否             |
| PUT      | 是             |
| DELETE   | 是             |
| PATCH    | 否             |



# http请求状态码

| 状态码 | 含义       |
| ------ | ---------- |
| 1xx    | 消息类     |
| 2xx    | 成功类     |
| 3xx    | 重定向     |
| 4xx    | 客户端错误 |
| 5xx    | 服务端错误 |



# 学生端项目系统表

| 英文名称                   | 中文名称                       |
| -------------------------- | ------------------------------ |
| sys_user                   | 用户表                         |
| sys_role                   | 角色表                         |
| t_student                  | 学生表                         |
| t_warn_info                | 提醒信息表(登录后提醒修改密码) |
| t_course_lesson            | 课时信息表                     |
| t_address                  | 收货地址表                     |
| t_sms_code                 | 短信验证码表                   |
| t_course_purchase          | 课程购买表                     |
| t_course_course_lesson_rel | 课程和课次关联表               |
| t_course_lesson            | 课次信息表                     |
| t_class_type               | 班级类型信息                   |
| t_teaching_class           | 教学班级表                     |
| t_weidu_teaching_class_rel | 威渡教学班级关联表             |
| t_broadcast_room           | 直播间表(直播间和校区关联)     |



# 转义符号

| 原符号 | 转译符号 |
| ------ | -------- |
| <      | \&lt;    |
| >      | \&gt;    |
| <=     | \&lt;=   |
| >=     | \&gt;=   |
| &      | \&amp;   |
| '      | \&apos;  |
| "      | \&quot;  |



# 领域模型

| 名词                               | 解释               |
| ---------------------------------- | ------------------ |
| POJO（plain ordinary java object） | 无规则简单java对象 |
| PO（persistent object）            | 持久层对象         |
| BO（business object）              | 业务对象           |
| VO（view object）                  | 表现层对象         |
| DTO（data transfer object）        | 数据传输对象       |
| DAO（data access object）          | 数据访问对象       |

PO和VO都属于POJO

POJO用作表现层－－》VO

POJO传输过程中－－》DTO

POJO持久化之后－－》PO



lombok为我们自动生成了属性的get、set方法，重写了hashcode()、equals()和toString()。



对象的equals()默认是比较对象对象的地址，equals方法内部调用的是"=="。


$$
\sum_{i=1}^n a_i
$$





装箱：基本数据类型到包装类型的过程

拆箱：包装类型到基本数据类型的过程



> 多行注释：
>
> + Ctrl+V ，进入 VISUAL BLOCK模式
> + 移动光标，选择需要注释的行
> + shift+i，输入注释符#，按esc



> 取消多行注释：
>
> + Ctrl+V，进入VISUAL BLOCK模式
> + 移动光标，选择需要取消注释的行
> + 输入x，删除所有的注释符#，同时退出visual block模式



:noh  vim中取消高亮



> 时区
>
> + 查看时区：show variables like '%time_zone%';
> + 当前会话设置时区：set time_zone = '+8:00';
> + 全局设置时区：set global time_zone = '+8:00';
> + 使配置生效：flush privileges;



>cookie,session,token
>
>+ http是无状态的
>+ cookie保存的客户端，是不可跨域的，大小有限制，不能超过4k
>+ session基于cookie，保存在服务端
>+ 移动端对cookie的支持不好，一般用token

jwt的组成部分：header(头部)、payload(载荷)、signature(签名)



**fw0000020 123456 生产环境学生端账号**







