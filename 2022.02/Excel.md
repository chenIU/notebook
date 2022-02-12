## 1.初始数据准备

![](http://cdn.chenjianyin.com/markdown/excel-1.png)



## 2.新建名称管理器

![](http://cdn.chenjianyin.com/markdown/excel-2.png)

图中`省`和`县`应该勾选`最左列`，`市`应该勾选`首行`。 具体要看数据怎样排布。



## 3.查看名称管理器

![](http://cdn.chenjianyin.com/markdown/excel-3.png)



## 4.省

![](http://cdn.chenjianyin.com/markdown/excel-4.png)



## 5.市

![](http://cdn.chenjianyin.com/markdown/excel-5.png)

+ 设置`市`的时候一定要县选择`省`，因为后者依赖前者。
+ `INDIRECT`函数的类似指针，指代依赖的地址。
+ `$A2`，表示A列是绝对引用（不会变），2是相对引用（会变），后面要将本列所有列应用到所有行。



## 6.区

![](http://cdn.chenjianyin.com/markdown/excel-6.png)

和`市`类似，在设置`县`时候需要先选择`市`和`省`。



最后，如果想将当前公式引用到所有行，只需按照下图操作即可：

![](http://cdn.chenjianyin.com/markdown/excel-7.png)

将鼠标放在需要设置列的最上方，然后点击`数据验证`，在弹出的窗口中点击`是`。如果报错，直接忽视（因为有的行需要依赖前面的数据，前面的数据为空）。