**MIME**：媒体类型(Multipurpose Internet Mail Extensions)



# 语法

`type/subtype`

| 类型          | 描述                                              | 典型示例                                                     |
| ------------- | ------------------------------------------------- | ------------------------------------------------------------ |
| `text`        | 表明文件是普通文本，理论是人类可读                | `text/plain`,`text/html`,`text/css`,`text/javascript`        |
| `image`       | 表明是某种图像，不包括视频，但动态图也是image类型 | `image/gif`,`image/png`,`image/jpeg`,`image/bmp`             |
| `audio`       | 表明是某种音频文件                                | `audio/ogg`,`audio/mpeg`,`audio/wav`                         |
| `video`       | 表明是某事视频文件                                | `video/ogg`,`video/webm`                                     |
| `application` | 表明是某种二进制数据                              | `application/xml`,`application/json`,`application/octet-stream` |



`application/x-www-form-urlencoded`：是表单默认的提交格式

`multipart/form-data`：表单中进行文件上传时，需要使用该格式