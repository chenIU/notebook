# run

> ```
> docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
> ```
>
> OPTIONS说明：
>
> + -i 以交互式运行模式，通常与`-t`同时使用 [interactive]
> + -t 为容器分配一个伪输入终端，通常与`-i`同时使用 [tty]
> + -d 后台运行
> + -P 随机映射端口
> + -p 指定端口映射，格式为：`主机(宿主)端口:容器端口` [port]
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
> + --privileged：Give extended privileges to this container



**docker run --rm选项详解**

在Docker容器退出时，默认容器内部的文件系统任然被保留，以方便调试并保留用户数据。

但是，对于foreground容器，由于其只是在开发调试过程中短期运行，用户数据并无保留的必要，因而可以在容器启动时设置`--rm`选项，这样在容器退出时能够自动清理容器内部的文件系统。

显然，`--rm`选项不能和`-d`同时使用，即只能自动清理foreground容器，不能自动清理detached容器。

注意，`--rm`选项也会自动清理容器的匿名data volumes。

所以，执行docker run 命令ddddddddddddddd带`--rm`命令选项，等价于在容器退出后，执行`dodcker rm -v`。



# command

## 查看

```bash
docker ps 		//查看正在运行的容器
docker ps -a    //查看所有启动过的容器
docker ps -l    //查看最新启动的容器
docker ps -n=2  //查看最新创建的n个容器
```



## 停止

```bash
docker stop container_id/container_name
```



## 重启

```bash
docker restart container_id/container_name
```

根据docker官网的解释，docker的重启策略可以分为四种：

| Policy                   | Result                                                       |
| ------------------------ | ------------------------------------------------------------ |
| no                       | 不自动重启容器，默认如此                                     |
| on-failure:[max-retries] | 在退出状态为非0时才会重启（非正常退出）                      |
| always                   | 始终重启容器，当docker守护进程重新启动时，无论容器当时的状态如何，都会重启容器 |
| unless-stopped           | 始终重启容器，但当docker守护进程启动时，如果容器已经停止运行，则不会重新启动它 |



## 删除

```bash
docker rm -f container_id/container_name //-f参数表示删除正在运行的容器
docker rm ${docker ps -a -q} //删除所有容器
```



## 端口

```bash
docker port container_id/container_name
# host:container (主机端口映射容器端口)
```



## 状态

```shell
# 查看某个容器的运行状态（内存/CPU/IO）
docker stats xxx
```



## 日志

```bash
docker logs container_id/container_name
docker logs -f --tail = 3 xxx
```



## 进程

```bash
docker top container_id/container_name
```



## 检查

```bash
docker inspect container_id/container_name
```



## 导出

```bash
docker export container_id/container_name > xxx
```



## 导入

```bash
cat exported_container| docker import - container_name
```



## 构建

```bash
docker build -t [container_name] dir
```



## 数据卷

查看所有数据卷：

```sh
docker volume ls
```



查看数据卷详情：

```sh
docker volume inspect xxx
```



删除数据卷

```sh
docker volume rm; //单个删除
docker volume purge //批量删除
```



## 删除镜像

```bash
docker rmi image_id/image_name
```



## 更改参数

```bash
docker container update --restart=always d72e7e910ab6
```



## 文件传输

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

`docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword`：不进入docker容器内部查看文件内容



# 启动脚本

## nginx

```sh
docker run --name nginx -itd -p 80:80 
-v ${pwd}/mnt/nginx:/usr/share/nginx/html
-v ${pwd}/mnt/conf/nginx.conf:/etc/nginx/nginx.conf
nginx
```



## phymyadmin

```bash
docker run -d --name myadmin -e PMA_HOST=47.101.129.111 -e PMA_PORT=33061 -p 8080:80 phpmyadmin
```



## mysql

```bash
docker run --name mysql -it -d -p 13306:3306 --restart=always -v /c/users/overmind/mnt/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 mysql:latest
```



## mariadb

```bash
docker run --name mariadb -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -v /data/mariadb/data:/var/lib/mysql -d mariadb
```



## consul

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



## redis

### linux

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

### windows

+ 持久化启动

```sh
docker run --name redis -d -it -p 6379:6379 --restart=always -v /c/users/overmind/mnt/redis/data:/data redis redis-server --appendonly yes
```



## portainer

```bash
docker run -d -p 9000:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --name prtainer portainer/portainer
```



## filebrowser

```sh
docker run --name filebrowser -d -v /root/filebrowser/sites/root:/srv -v /root/filebrowser/filebrowserconfig.json:/etc/config.json -v /root/filebrowser/database.db:/etc/database.db -p 18080:80 filebrowser/filebrowser
```

默认用户名和密码：**admin/admin**



## rethinkdb

```sh
docker run --name rethinkdb -p 8080:8080 -p28015:28015 -p29015:29015 -e /data/docker/rethinkdb:/data -d rethinkdb
```



## emqx

```sh
docker run -d --name emqx -p 1883:1883 -p 8083:8083 -p 8883:8883 -p 8084:8084 -p 18083:18083 emqx/emqx
```



## elasticsearch

```sh
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch
```



## couchdb

```sh
docker run --name couchdb -d -p 15984:5984 -e COUCHDB_USER=admin -e COUCHDB_PASSWORD=123456 couchdb
```



## nexus

```sh
mkdir -p /data/nexus & chown -R 200 /data/nexus
docker run --name nexus -d -p 8081:8081 -v /data/nexus:/nexus-data sonatype/nexus3
```



## tomcat

```sh
docker run --name tomcat -d -p 8090:8080 -v ${pwd}/mnt/tomcat/webapps:/usr/local/tomcat/webapps -v ${pwd}/mnt/tomcat/logs:/usr/local/tomcat/logs tomcat
```



## MinIO

```sh
docker run -d --name minio -p 9000:9000 minio/minio server /data
```



## showdoc

```sh
docker run -d --name showdoc --user=root --privileged=true -p 5000:80 -v /showdoc_data/html:/var/www/html/ star7th/showdoc
```



## xxl-job

```sh
docker run -itd -e PARAMS='--spring.datasource.url=jdbc:mysql://[ip]:3306/xxl_job --spring.datasource.username=[username] --spring.datasource.password=[password]' --privileged=true -p 8888:8080 -v /tmp/xxl-job-admin:/data/applogs --name xxl-job-admin xuxueli/xxl-job-admin:2.3.0
```



## jenkins

```sh
docker run -d --name jenkins -p 18080:8080 -p 50000:50000 -v /data/jenkins_home:/var/jenkins_home jenkinszh/jenkins-zh
```



## flowable

```sh
docker run -d --name flowable -p 19001:8080 flowable/all-in-one
# 默认用户名和密码：admin/test
```



## netdata

```shell
docker run -d --name=netdata \
  -p 19999:19999 \
  -v netdataconfig:/etc/netdata \
  -v netdatalib:/var/lib/netdata \
  -v netdatacache:/var/cache/netdata \
  -v /etc/passwd:/host/etc/passwd:ro \
  -v /etc/group:/host/etc/group:ro \
  -v /proc:/host/proc:ro \
  -v /sys:/host/sys:ro \
  -v /etc/os-release:/host/etc/os-release:ro \
  --restart unless-stopped \
  --cap-add SYS_PTRACE \
  --security-opt apparmor=unconfined \
  netdata/netdata
```



## RabbitMQ

```shell
docker run -d --hostname my-rabbit --name RabbitMQ -p 15672:15672 rabbitmq:3-management
```