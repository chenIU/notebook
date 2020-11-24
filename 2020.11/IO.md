## 1 初识Java IO

流(stream)，是一个抽象的概念，是指一连串的数据(字节或字符)，以先进先出的方式发送信息的通道。

一般来说流的特征主要有以下几个方面：

+ 先进先出：最先写入输出流的数据最先被输入流读取到。
+ 顺序读取：可以一个接一个地往流中写入一串字节，读取时也将按写入顺序读取一串字节，不能随机访问中间数据。(RandomAccessFile除外)
+ 只读或只写：每个流只能是输入流或输出流的一种，不能同事具备两个功能。

### 1.1 IO流分类

按分类方式的不同主要有以下三种：

+ 按数据流的方向：输入流、输出流
+ 按处理数据单位：字节流、字符流
+ 按功能：节点流、处理流

![image-20201124092024143](http://cdn.chenjianyin.com/markdown/IO1.png)

**1、输入流和输出流**

输入和输出是相对应用程序而言，读文件是输入流，写文件是输出流。



**2、字节流和字符流**

字节流和字符流的用法几乎完全一样，区别在于字节流和字符流所操作的数据单元不同。字节流操作的数据单元是8位的字节，字符流操作的数据单元是16位的字符。

**区别**

+ 字节流一般用来处理图像、视频、音频、PPT、Word等类型的文件。字符流一般用于处理纯文本类型的文件，如TXT文件，但不能处理图像视频等非文本文件。一句话概括：字节流可以处理一切文件，而字符流只能处理纯文本文件。
+ 字节流本身没有缓冲区，缓冲字节流相对于字节流， 效率提升非常高。而字符流本身就有缓冲区，缓冲字符流相对于字符流效率提升就不是很大。



**3、节点流和处理流**

**节点流**：直接操作数据读写的类，比如`FileInputStream`

**处理流**：对一个已存在的流的链接和封装，通过对数据进行处理为程序提供强大、灵活的读写功能，比如`BufferedInputSteam`

处理流和节点流应用了Java的装饰者模式



完整的IO分类图如下：

![img](http://cdn.chenjianyin.com/markdown/IO2.png)

### 1.2 案例实操

**1、FileInputStream、FileOutputStream(字节流)**

> 字节流的方式效率较低，不建议使用

```java
public class Test1 {
    public static void main(String[] args) throws IOException {
        String str = "松下问童子，言师采药去。只在此山中，云深不知处。";
        OutputStream out = new FileOutputStream(new File("E:/test.txt"));
        out.write(str.getBytes());

        InputStream in = new FileInputStream(new File("E:/test.txt"));
        StringBuffer sb = new StringBuffer();
        byte[] buffer = new byte[1024];
        int len;
        while((len = in.read(buffer)) != -1){
            sb.append(new String(buffer,0,len));
        }
        out.close();
        in.close();
        System.out.println(sb.toString());
    }
}
```

**2、BufferedInputStream、BufferedOutputStream(缓冲字节流)**

> 缓冲字节流是为高效率而设计的，真正的读写操作还是靠FileInputStream和FileOutputStream

```java
public class Test2 {
    public static void main(String[] args) throws IOException {
        String str = "松下问童子，言师采药去。只在此山中，云深不知处。";
        OutputStream out = new BufferedOutputStream(new FileOutputStream(new File("E:/test.txt")));
        out.write(str.getBytes());
        out.flush();

        InputStream in = new BufferedInputStream(new FileInputStream(new File("E:/test.txt")));
        StringBuffer sb = new StringBuffer();
        byte[] buffer = new byte[1024];
        int len;
        while ((len = in.read(buffer)) != -1) {
            sb.append(new String(buffer, 0, len));
        }
        out.close();
        in.close();
        System.out.println(sb.toString());
    }
}
```

**注意**：out.flush()，强制将内存中的数据刷新到硬盘上

**3、InputStreamReader、OutputStreamWriter(字符流)**

> 字符流适用于文本文件的读写，`OutputStreamWriter`类其实也是借助`FileOutputStream`类实现的，故其构造方法是`FileOupputStream`对象

```java
public class Test3 {
    public static void main(String[] args) throws IOException {
        String str = "松下问童子，言师采药去。只在此山中，云深不知处。";
        OutputStreamWriter osr = new OutputStreamWriter(new FileOutputStream(new File("E:/test.txt")));

        osr.write(str);
        osr.close();

        InputStreamReader isr = new InputStreamReader(new FileInputStream(new File("E:/test.txt")));
        char[] chars = new char[1024];
        StringBuilder sb = new StringBuilder();
        int len;
        while((len = isr.read(chars)) != -1){
            sb.append(chars,0,len);
        }
        isr.close();
        System.out.println(sb.toString());
    }
}
```

**4、FileWriter、FileReader(字符流便捷类)**

> Java提供了FileWriter、FileReader简化字符流的读写，new FileWriter等同于new OutputStreamWriter(new FileOutputStream(file,true))

```java
public class Test4 {
    public static void main(String[] args) throws IOException {
        String str = "松下问童子，言师采药去。只在此山中，云深不知处。";
        FileWriter fw = new FileWriter("E:/test.txt");
        fw.write(str);
        fw.close();

        FileReader fr = new FileReader("E:/test.txt");
        char[] chars = new char[1024];
        StringBuilder sb = new StringBuilder();
        int len;
        while ((len = fr.read(chars)) != -1){
            sb.append(chars,0,len);
        }
        fr.close();
        System.out.println(sb.toString());
    }
}
```

**5、BufferedReader、BufferedWriter(字符缓冲流)**

```java
public class Test5 {
    public static void main(String[] args) throws IOException {
        String str = "松下问童子，言师采药去。只在此山中，云深不知处。";
        BufferedWriter bw = new BufferedWriter(new FileWriter("E:/test.txt"));
        bw.write(str);
        bw.close();

        BufferedReader br = new BufferedReader(new FileReader("E:/test.txt"));
        StringBuilder sb = new StringBuilder();
        String line;
        while ((line = br.readLine()) != null){
            sb.append(line);
        }
        br.close();
        System.out.println(sb.toString());
    }
}
```



## 2 IO 流对象



### 2.1 File类

`File`类是用来操作文件的类，但它不能操作文件中的数据

**File类常用方法**

| 方法              | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| createNewFile     | 当且仅当不存在具有此抽象路径名指定名称的文件时，不可分地创建一个新的空文件 |
| delete()          | 删除此抽象路径名表示的文件或目录                             |
| exists()          | 测试此抽象名表示的文件或目录是否存在                         |
| getAbsoluteFile() | 返回此抽象路径名的绝对路径名形式                             |
| getAbsolutePath() | 返回此抽象路径名的绝对路径名字符串                           |
| length()          | 返回由此抽象路径名表示的文件的长度                           |
| mkdir()           | 创建此抽象路径名指定的目录                                   |



### 2.2 字节流

`InputStream`与`OutputStream`是两个抽象类，是字节流的基类，说有具体的字节流实现类都分别继承这两个类。



`InputStream`类继承图：

![image-20201124111159842](http://cdn.chenjianyin.com/markdown/IO3.png)

+ FileInputStream：文件输入流，一个非常重要的字节输入流，用于对文件进行读取操作。
+ PipedInputStream：管道字节输入流，能实现多线程间的管道通信
+ ByteArraryInputStream：字节数组输入流，从字节数组(byte[])中进行以字节为单位的读取，也就是将资源文件都以字节的形式存入到该类中的字节数组中去。
+ FilterInputStream：装饰者类，具体的装饰者继承该类，这些类都是处理类，作用是对节点流进行封装，实现一些特殊功能。
+ DataInputStream：数据输入流，它是用来装饰其他输入流，作用是"允许应用程序以与机器无关的方式从底层输入流中读取基本Java数据类型"
+ BufferedInputStream：缓冲流，对节点流进行装饰，内部会有一个缓冲区，用来存放字节，每次都是将缓冲区存满之后发送，而不是一个字节或两个字节发送，效率得以提高。
+ ObjectInputSteam：对象输入流，用来提供对基本数据或对象的持久存储。通俗点说就是能直接传输对象，通常应用在反序列化中。它也是一种处理流，构造器入参是一个InputStream实例对象。



`OutputStream`类继承图：

![image-20201124104010835](http://cdn.chenjianyin.com/markdown/IO4.png)

OutputStream类继承与InputStream类似。



### 2.3 字符流

> 与字节流类似，字符流也有两个抽象基类，分别是Reader和Writer。其他的字符流实现类分别必须继承这两个类



以Reader为例，它的主要实现子类如下图：

![image-20201124104413073](http://cdn.chenjianyin.com/markdown/IO5.png)

+ InputStreamReader：从字节流到字符流的桥梁(InputStreamReader构造器入参是FileInputStream实例对象)，它将读取的字节使用指定的字符集编码解码为字符。
+ BufferedReader：从字符输入流中读取文本，设置一个缓冲区来提高效率。BufferedReader是对InputStreamReader的封装，前者的构造器入参是后者的一个实例对象。
+ FileReader：用于读取字符文件的便捷类，new FileReader(File file)等同于new InputStreamReader(new FileInputStream(file,true),"UTF-8")，但FileReader不能指定字符编码和默认字节缓冲区大小。
+ PipeReader：管道字符流，可以实现多线程间的管道通信
+ CharArrayReader：从Char数组中读取数据的介质流
+ StringReader：从String 中读取数据的介质流



Writer和Reader结构类似，方向相反，不再赘述。



## 3 IO流方法

### 3.1 字节流方法

字节输入流`InputStream`主要方法：

+ read()：从字节流中读取一个数据字节
+ read(byte[] b)：从输入流中将最多b.length个字节的数据读入到一个byte数组中
+ read(byte[] b,int off,int len)：从输入流中将最多len个字节的熟读入到一个byte数组中
+ close()：关闭此输入流并释放与流关联的系统资源



字节输出流`OutputStream`主要方法：

+ write(int b)：将指定字节写道到此输出流
+ write(byte[] b)：将b.length个字节从指定数组写入到此输出流中
+ write(byte[] b,int off,int len)：将指定数组从偏移量off开始的len个字节写入到此输出流中
+ close()：关闭此输出流并释放与该流关联的系统资源



### 3.2 字符流方法

字符输入流`Reader`主要方法：

+ read()：读取单个字符
+ read(char[] cbuf)：将字符读入数组
+ read(char[] cbuf,int off,int len)：将字符读入数组的某一部分
+ read(CharBuffer target)：试图将字符读入指定的字符缓冲区
+ flush()：刷新该流的缓冲
+ close()：关闭此流，但要先刷新它。



字符输出流`Writer`主要方法：

+ write(int c)：写入单个字符
+ write(char[] cbuf)：写入字符数组
+ write(cahr[] cbuf,int off,int len)：写入字符数组的某一部分
+ write(String str)：写入字符串
+ write(String str,int off,int len)：写入字符串的某一部分
+ flush()：刷新该流的缓冲
+ close()：关闭此流，但要先刷新它



## 4 附加内容

字节(Byte)是计量单位，表示数据量多少，一字节等于八位

字符(Character)是计算机中使用的字母、数字和符号，比如'A'、'$'

一般在英文状态下一个字母或字符占用一个字节，一个汉字占用两个字节

其他编码情况：

+ ASCII：一个英文(不分大小写)占用一个字节，一个中文汉字占用两个字节
+ Unicode：一个英文占用一个字节，一个中文占用两个字节
+ UTF-8：一个英文占用一个字节，一个中文占用三个字节
+ UTF-16：一个英文字母或一个汉字字符都占用两个字节(Unicode扩大区的一些汉字存储需要4个字节)
+ UTF-32：世界上任何字符都占用4个字节