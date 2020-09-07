**常用参数**



**-b**

`-b`参数用来向服务器发送Cookie

```
curl -b 'foo=bar' https://google.com
```

上述命令会生成一个标头`Cookie：foo=bar`，向服务器发送一个名为`foo`、值为`bar`的Cookie

```
curl -b 'foo1=bar1' -b 'foo2=bar2' https://google.com 
```

上述命令发送两个Cookie



**-c**

`-c`参数将服务器设置的Cookie写入一个文件

```
curl -c cookies.txt http://www.google.com
```

上述命令将服务器的HTTP响应所设置的Cookie写入文本文件`cookies.txt`



**-d**

`-d`参数用于发送POST请求的数据体

```
curl -d 'username=jack&password=123456' -X POST https://google.com/login
```

或者

```
curl -d 'username=jack' -d 'password=123456' -X POST http://google.com/login
```

使用`-d`参数以后，HTTP请求会自动加上标头`Content-Type：application/x-www-form-urlencoded`。并且会自动将请求方法转为POST方法，因此可以省略`-X POST`。

`-d`参数可以读取本地的文本文件数据，向服务器发送。

```
curl -d '@data.txt' https://google.com/login
```

上述命令读取`@data.txt`文件的内容，作为数据体向服务器发送。



**--data-urlencode**

`--data-urlencode`参数等同于`-d`，发送POST请求的数据体，区别在于会自动将发送的数据进行URL编码

```
curl --data-urlencode 'comment=hello world' https://google.com/login
```

上述命令，发送的数据`hello world`之间有一个空格，需要进行URL编码。



**-e**

`-e`参数用来设置HTTP的标头`Referer`，表示请求的来源

```
curl -e 'https://google.com?q=example' https://www.example.com
```

上述命令将`Referer`标头设为`https://googole.com?q=example`。

`-H`参数通过直接设置标头`Referer`，达到同样效果。

```
curl -H 'Referer:https://google.com?q=example' https://www.example.com
```



**-F**

`-F`参数用来向服务器上传二进制文件

```
curl -F 'file=@photo.png' https://google.com/profile
```

上述命令会给HTTP请求加上标头`Content-Type:multipart/form-data`，然后将文件`photo.png`作为`file` 字段上传。

`-F`参数可以指定MIME类型

```
curl -F 'file=@photo.png;type=image/png' https://google.com/profile
```

上述命令会将MIME类型指定为`image/png`，否则curl会把MIME类型设为`application/octet-stream`。

`-F`参数也可以指定文件名

```
curl -F 'file=@photo.png;filename=me.png' https://google.com/profile
```

上述命令中，原始文件名为`photo.png`，但是服务器接收到的文件名为`me.png`。



**-G**

`-G`参数用来构造URL查询字符串

```
curl -G -d 'q=kitties' -d 'count=20' http://google.com/search
```

上述命令会发出一个GET请求，实际请求的URL为`https://google.com/search?q=kitties&count=20`。如果省略`-G`，会发送一个POST请求。

如果数据需要URL编码，可以结合`--data-urlencode`参数。

```
curl -G --data-urlencode 'commnet=hello world' https://google.com
```



**-H**

`-H`参数添加HTTP请求的标头

```
curl -H 'Accept-Language:en-US' https://google.com
```

上述命令添加HTTP标头`Accept-Language:en-US`

```
curl -d '{"username":"jack","password":"123456"}' -H "Content-Type:application/json" https://google.com/login
```

上述命令添加HTTP请求标头`Content-Type:application/json`，然后用`-d`参数发送JSON数据。



**-i**

`-i`参数打印出服务器响应的HTTP标头

```
curl -i https://www.example.com
```

上述命令收到服务器响应后，先输出服务器响应的标头，然后空一行，再输出网页的源码。



**-I**

`-I`参数向服务器发送HEAD请求，然后将服务器返回的HTTP标头打印出来

```
curl -I https://www.example.com
```

上述命令输出服务器对HEAD请求的回应。

`--head`参数等同于`-I`

```
curl --head https://www.example.com
```



**-K**

`-K`参数指定跳过SSL检测

```
curl -k https://www.example.com
```

上述命令不会检查服务器的SSL证书是否正确



**-L**

`-L`参数会让HTTP请求跟随服务器的重定向。curl默认不跟随重定向。

```
curl -L -d 'tweet=hi' https://api.twitter.com/tweet
```



**--limit-rate**

`--limit-rate`用来限制HTTP请求和响应的带宽，模拟慢网速的环境

```
curl --limit-rate 200k https://google.com
```



**-o**

`-o`参数将服务器的响应保存成文件，等同于`wget`

```
curl -o example.html https://www.example.com
```

上述命令将`www.example.com`的响应保存成`example.html`



**-O**

`-O`参数将服务器回应保存成文件，并将URL的最后部分当作文件名

```
curl -O https://www.example.com/foo/bar.html
```

上述命令将服务器的响应保存成文件，文件名为`bar.html`



**-s**

`-s`参数不输出错误和进度信息

```
curl -s https://www.example.com
```

上述命令一旦发生错误，不会显示错误信息。不发生错误，会正常显示运行结果。

如果想让curl不产生任何输出，可以使用如下命令：

```
curl -s -o /dev/null https://www.example.com
```



**-S**

`-S`参数指定只输出错误信息

```
curl -S https://www.example.com
```



**-u**

`-u`参数用来设置服务器认证的用户名和密码

```
curl -u 'jack:123456' https://google.com/login
```

上述命令设置用户名为`jack`，密码为`123456`，然后将其转为HTTP标头`Authorization: Basic`。

curl能够识别URL里面的用户名和密码

```
curl https://jack:123456@google.com/login
```

上述命令能够识别URL里面的用户名和密码，将其转为上个例子里面的HTTP标头。

```
curl -u 'jack' https://googole.com/login
```

上述命令只设置了用户名，执行后，curl会提示用户输入密码。



**-v**

`-v`参数输出通信的整个过程，用户调试。

```
curl -v https://www.example.com
```

`--trace`参数也可用于调试，还会输出原始的二进制数据。

```
curl --trace - https://google.com
```



**-x**

`-x`参数指定HTTP请求的代理

```
curl -x socks5://jack@cats@myproxy.com:8080 https://www.example.com
```

上述命令指定HTTP请求通过`myproxy.com:8080`的socks5代理发出。如果没有指定代理协议，默认为HTTP。

```
curl -x socks5://jack@cats@myproxy.com:8080 https://www.example.com
```

上述命令中，请求代理使用HTTP协议。



**-X**

`-X`参数指定HTTP请求的方法

```
curl -X POST https://www.example.com
```

上述命令对`https://www.example.com`发出POST请求。















