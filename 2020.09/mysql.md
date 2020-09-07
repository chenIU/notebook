**explain**

![image-20200907103633232](http://cdn.chenjianyin.com/markdown/image-20200907103633232.png)

解释：

table：显示这一列的数据是关于哪张表的

type：这是重要的列，显示连接使用了何种类型，从好到差依次是:const、eq_reg、ref、range、index和all

possible_keys：显示可能应用在这张表中的索引。如果为空则表示没有可能的索引

key：实际使用的索引。如果为null，则没有使用索引。很少的情况下，mysql会优化不足的索引。这种情况下，可以在select语句中使用use index(index_name)来强制使用某个索引或者使用ignore index(index_name)来强制mysql忽略索引。

key_len：索引的长度。在不损失精度的情况下，越短越好

ref：显示索引的哪一列被使用了，如果可能的话，是一个常数

rows：请求数据的行数，越小越好

extra：关于mysql如何解析查询的额外信息。最坏的情况是using temporary和using filesort，这种情况下不会使用索引，结果查询会很慢