`如何快速启动一个http服务`



### 1 借助编程语言

```python
python3 -m http.server
```



```php
php -S localhost:8080
```



```
ruby -run -e httpd . -p 8080
```



或者稍微麻烦一点，一些编程语言的库也可以做到

```
#安装http-server
npm i -g http-server
#运行
http-server -p 8080
```





### 2 使用二进制包

```
#下载二进制文件
wget -O server  https://github.com/sunwu51/Tool/releases/download/2/server_linux_amd64

#增加可执行权限
chmod +x server

#运行
./server -port 8080 --assets .
```

