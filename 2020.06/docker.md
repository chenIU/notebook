**启动**

> ```
> docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
> ```
>
> OPTIONS说明：
>
> + -i 以交互式运行模式，通常与`-t`同时使用
> + -t 为容器分配一个伪输入终端，通常与`-i`同时使用
> + -d 后台运行
> + -P 随机映射端口
> + -p 指定端口映射，格式为：`主机(宿主)端口:容器端口`
> + --name 为容器指定一个名称
> + --dns 指定容器使用的DNS服务器，默认和宿主一致
> + -h 指定容器的hostname
> + -e 设置环境变量
> + --env-file [] 从指定文件读入环境变量
> + -m 指定容器使用最大内存值
> + --net 指定容器的网络连接类型，支持`bridge/host/none/container`四种类型
> + --link=[] 添加链接到另一容器
> + --expose=[] 开放一个或者一组端口
> + --volume/-v：绑定一个卷



**docker run --rm选项详解**

在Docker容器退出时，默认容器内部的文件系统任然被保留，以方便调试并保留用户数据。

但是，对于foreground容器，由于其只是在开发调试过程中短期运行，用户数据并无保留的必要，因而可以在容器启动时设置`--rm`选项，这样在容器退出时能够自动清理容器内部的文件系统。

显然，`--rm`选项不能和`-d`同时使用，即只能自动清理foreground容器，不能自动清理detached容器。

注意，`--rm`选项也会自动清理容器的匿名data volumes。

所以，执行docker run 命令ddddddddddddddd带`--rm`命令选项，等价于在容器退出后，执行`dodcker rm -v`。



**查看**

```bash
docker ps -a
```



**停止**

```bash
docker stop container_id/container_name
```



**重启**

```bash
docker restart container_id/container_name
```



**删除**

```bash
docker rm -f container_id/container_name
```



**端口**

```bash
docker port container_id/container_name
```



**日志**

```bash
docker logs container_id/container_name
```



**进程**

```bash
docker top container_id/container_name
```



**检查**

```bash
docker inspect container_id/container_name
```



**导出**

```bash
docker export container_id/container_name > xxx
```



**导入**

```bash
cat exported_container| docker import - container_name
```



**构建**

```bash
docker build -t [container_name] dir
```



**删除容器**

```bash
docker rmi image_id/image_name
```



**删除启动过的容器**

```bash
docker rm -f  container_id/container_name
```



**更改容器启动参数**

```bash
docker container update --restart=always d72e7e910ab6
```



**启动容器(交互方式)**

```bash
docker run -i -t <image_name/container_id> /bin/bash
```



**启动容器(后台)**

```bash
docker run -d -it image_name
```

```bash
docker run -d -p 16379:6379 --name redis redis:latest
```

+ p：映射端口
+ --name：给启动的容器起名称



**停止容器**

```sh
docker stop container_id/container_name
```



**查看端口映射**

```sh
docker port container_name/id
```

```sh
docker inspect container_name/id
```



**文件传输**

+ 宿主机文件传到docker容器中：

  ```bash
  docker cp 本地文件路径 容器ID/名称:/目标路径
  ```

  实例：

  ```sh
  docker cp /docker/httpd/htdocs/index.html 22e:/usr/local/apache2/htdocs/index.html
  ```

  

+ docker容器文件传到宿主机中：

  ```bash
  docker cp 容器ID/名称:/文件路径 本地路径  (docker cp ./mysqld.cnf master:/etc/mysql/mysql.conf.d/)
  ```
  
  实例：
  
  ```sh
  docker cp 22e43c9d5b9a:/usr/local/apache2/htdocs/index.html  /docker/httpd/htdocs/index.html
  ```
  
  

# 总结

**容器内安装软件**

> 容器内安装软件
>
> + apt-get update
> + apt-get install vim



**Docker服务的启动**

+ 启动：systemctl start docker/service docker start
+ 停止：systemctl stop docker/service docker stop
+ 重启：systemctl restart docker/service docker retart



| 命令                           | 解释                     |
| ------------------------------ | ------------------------ |
| docker ps -l                   | 最后一次启动的容器       |
| docker exec -it xxx bash       | 进入某个容器             |
| docker run -d -P image_name/id | 随机映射启动的端口       |
| docker info                    | 查看docker所有的详细信息 |
| docker version                 | 查看docker版本信息       |
| docker rm \`docker ps -a -q\`  | 删除所有docker容器       |
| ip a show docker0              | 查看docker0的网络        |



# 启动脚本

启动phymyadmin

```bash
docker run -d --name myadmin -e PMA_HOST=47.101.129.111 -e PMA_PORT=33061 -p 8080:80 phpmyadmin
```



启动mysql

```bash
docker run --name mysql -p 3306:3306 --restart=always -e MYSQL_ROOT_PASSWORD=123456 -d mysql:latest
```



启动mariadb

```bash
docker run --name mariadb -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -v /data/mariadb/data:/var/lib/mysql -d mariadb
```



启动consul

```bash
docker run --name consul -d -p 8500:8500 -p 8300:8300 -p 8301:8301 -p 8302:8302 -p 8600:8600 consul agent -server -bootstrap-expect=1 -ui -bind=0.0.0.0 -client=0.0.0.0
```

参数如下：

> -net = host docker参数，使得docker容器越过了netnamespace的隔离，免去手动指定端口映射的步骤
>
> -server consul支持以server或client的模式运行，server是服务发现模块的核心，client主要用于转发请求
>
> -advertise 将本机私有IP传递到consul
>
> -bootstrap-expect 指定consul将等待几个节点连通，形成一个完整的集群
>
> -retry-join 指定要加入的consul节点地址，失败会重试，可多次指定不同的地址
>
> -client consul绑定在哪个client地址上，这个地址提供HTTP、DNS、RPC等服务，默认是127.0.0.1
>
> -bind 改地址用来在结群内部的通讯，集群内的所有节点到该地址都必须是可达的，默认是0.0.0.0
>
> -allow_state 设置为true，表明可以从consul集群的任一server节点获取DNS信息，false则表明每次请求都会经过consul server leader
>
> --name Docker容器的名称
>
> -client 0.0.0.0表明任何地址都可以访问
>
> -ui 提供图形化界面



启动redis

+ 快速启动

```bash
docker run -itd --name docker-redis -p 6379:6379 redis
```

`--restart=always`：docker服务重启，容器自动启动

+ 配置文件启动

```bash
docker run -p 16379:6379 --name redis -v /usr/local/docker/redis.conf:/etc/redis/redis.conf -v /usr/local/docker/data:/data -d redis redis-server /etc/redis/redis.conf --appendonly yes
```

+ -p：端口映射
+ --name：指定容器名称
+ -v：挂载目录
+ -d：后台启动
+ redis-server：以配置文件启动redis
+ --appendonly yes：开启redis持久化

`-v  /usr/local/docker/data:/data`：指定数据文件映射



启动portainer

```bash
docker run -d -p 9000:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --name prtainer portainer/portainer
```



启动filebrowser

```sh
docker run --name filebrowser -d -v /root/filebrowser/sites/root:/srv -v /root/filebrowser/filebrowserconfig.json:/etc/config.json -v /root/filebrowser/database.db:/etc/database.db -p 18080:80 filebrowser/filebrowser
```



启动rethinkdb

```sh
docker run --name rethinkdb -p 8080:8080 -p28015:28015 -p29015:29015 -e /data/docker/rethinkdb:/data -d rethinkdb
```