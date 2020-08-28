**proxy_pass(带/和不带/的区别)**

1、location后没有/，proxy_pass后没有/

location /bbs {

​	proxy_pass http://127.0.1.0:8080;

}

最后网站转发到http://127.0.0.1:8080/bbs/index.html



2、location后没有/，proxy_pass后有/

location /bbs {

​	proxy_pass http://127.0.1.0:8080/;

}

最后网站转发到http://127.0.0.1:8080/index.html



3、location后有/，proxy_pass后没有/

location /bbs/ {

​	proxy_pass http://127.0.1.0:8080;

}

最后网站转发到http://127.0.0.1:8080/bbs/index.html



4、location后有/，proxy_pass后有/

location /bbs/ {

​	proxy_pass http://127.0.1.0:8080/;

}

最后网站转发到http://127.0.0.1:8080/index.html



**总结**

```
从这四种我们可以的看出，当nginx里面匹配时可以把端口后的参数分为path1+path2(其中我在上方标注的location属于path1，proxy_pass属于path2)当proxy_pass  
里面是ip:port+/时nginx最后匹配的网址是 proxy_pass的内容加上path2
里面是ip:port时nginx最后匹配的网址是 proxy_pass的内容加上path1+path2
```



`在nginx中配置proxy_pass代理转发时，如果在proxy_pass后面的url加/，表示绝对根路径；如果没有/，表示相对路径，把匹配的路径部分也给代理走。`



`server_name的作用：`

+ _：匹配所有域名
+ ""：匹配没有传递Host头部的情况



`nginx访问日志目录：/var/log/nginx/access_log`



`Host`

+ 不设置：Host是代理之后的ip+port
+ proxy_set_header Host $host：原ip，不加端口
+ proxy_set_header Host $host:$proxy_port：原ip+转发之后的代理端口
+ proxy_set_header Host $http_host：原ip+原端口



`常用内置变量：`

```
$host：客户端主机名
$http_host：客户端主机名+端口
$proxy_port：服务器代理端口
$server_addr：服务器地址
$server_name：服务器名
$server_port：服务器端口
$remote_addr：客户端ip
$remote_port：客户端端口
$request_method：请求方法
$request：客户端请求地址
$request_length：请求长度（包括请求地址+请求头和请求主体）
$schema：请求中的协议（通常是http或者https）
$server_protocol：服务器的http版本（通常是"HTTP/1.0"或者"HTTP/1.1"）
$args：请求中的参数值
$query_string：同$args
$uri：请求地址，不包含参数，参数位于$args
$content-type：Content-Type" 请求头字段
$content-length："Content-Length" 请求头字段
```



`常用设置：`

```
proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
```

