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



