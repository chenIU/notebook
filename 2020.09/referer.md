**Referer**



**Referrer Policy的值**

**1.no-referrer**

不发送`Referer`字段



**2.no-referrer-when-downgrade**

如果从HTTPS网址链接到HTTP网址，不发送`Referer`字段，其他情况（包括HTTP网址链接到HTTP网址）。这是浏览器的默认行为。



**3.same-origin**

链接到同源地址（协议+域名+端口 都相同）时发送，否则不发送。注意，`https://foo.com`链接到`http://foo.com`也属于跨域。



**4.origin**

`Referer`字段一律只发送源信息，不管是否跨域。



**5.strict-origin**

如果从HTTPS网址链接到HTTP网址，不发送`Referer`字段，其他情况只发送源信息。



**6.origin-when-cross-origin**

同源时，发送完整的`Referer`字段，跨域时发送源信息。



**7.strict-origin-when-cross-origin**

同源时，发送完整的`Referer`字段；跨域时，如果从HTTPS网址链接到HTTP网址，不发送`Referer`字段，否则发送源信息。



**8.unsafe-url**

`Referer`字段包含源信息、路径和查询字符串，不包含锚点、用户名和密码。



**Referrer Policy**的用法

**1.HTTP头信息**

```
Referrer-Policy:origin
```

**2.\<meta\>标签**

```html
<meta name="referrer" content="origin">
```

**3.referrerpolicy属性**

`<a>`、`<area>`、`<img>`、`<iframe>`和`<link>`标签都可以设置referrerpolicy属性

```html
<a href="..." referrerpolicy="origin" target="_blank">xxx</a>
```





