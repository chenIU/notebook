# Elastic Search 常用可视化管理工具

## elasticsearch-head

+ 项目地址：https://github.com/mobz/elasticsearch-head
+ docker安装方式：

```bash
docker pull mobz/elasticsearch-head:5-alpine

```

+ 访问地址：http://localhost:9100

+ 使用效果：

  ![image-20201109152344632](http://cdn.chenjianyin.com/markdown/esv-1.png)



## ElasticHD

+ 项目地址：https://github.com/360EntSecGroup-Skylar/ElasticHD

+ 直接安装方式：

  ```bash
  首先下载zip压缩包：https://github.com/360EntSecGroup-Skylar/ElasticHD/releases/
  修改权限：chmod -R 777 ElasticHD
  运行: ./ElasticHD -p 127.0.0.1:9800
  ```

+ docker安装方式：

  ```bash
  docker run -p 9200:9200 -d --name elasticsearch elasticsearch
  docker run -p 9800:9800 -d --link elasticsearch:demo containerize/elastichd
  ```

+ 访问地址：http://localhost:9800

+ 使用效果：

![image-20201109154618501](http://cdn.chenjianyin.com/markdown/esv-2.png)



## Dejavu

+ 项目地址：https://github.com/appbaseio/dejavu/

+ docker安装方式：

  ```bash
  docker pull appbaseio/dejavu
  docker run -p 1358:1358 -d appbaseio/dejavu
  ```

+ 访问地址：http://localhost:1358

+ 使用效果

![image-20201109155210473](http://cdn.chenjianyin.com/markdown/esv-3.png)