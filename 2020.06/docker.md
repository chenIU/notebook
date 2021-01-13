**启动**

> docker run
>
> + -i 交互式
> + -t 终端
> + -d 后台运行



**查看**

docker ps -a



**停止**

docker stop container_id/container_name



**重启**

docker restart container_id/container_name



**删除**

docker rm -f container_id/container_name



**端口**

docker port container_id/container_name



**日志**

docker logs container_id/container_name



**进程**

docker top container_id/container_name



**检查**

docker inspect container_id/container_name



**导出**

docker export container_id/container_name > xxx



**导入**

cat exported_container| docker import - container_name



**删除容器**

docker rmi image_id/image_name



**删除启动过的容器**

docker rm -f  container_id/container_name



**启动容器(交互方式)**

docker run -i -t <image_name/container_id> /bin/bash



**启动容器(后台)**

docker run -d -it image_name

docker run -d -p 16379:6379 --name redis redis:latest

+ p：映射端口
+ --name：给启动的容器起名称



**停止容器**

docker stop container_id/container_name



**查看端口映射**

docker port container_name/id

docker inspect container_name/id



**文件传输**

+ 宿主机文件传到docker容器中：docker cp 本地文件路径 容器ID/名称:/目标路径
+ docker容器文件传到宿主机中：docker cp 容器ID/名称:/文件路径 本地路径  (docker cp ./mysqld.cnf master:/etc/mysql/mysql.conf.d/)



**docker容器中启动redis**

+ 快速启动

```
docker run -itd --name docker-redis -p 6379:6379 redis
```

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



# 总结

**容器内安装软件**

> 容器内安装软件
>
> + apt-get update
> + apt-get install vim





| 命令                           | 解释                     |
| ------------------------------ | ------------------------ |
| docker ps -l                   | 最后一次启动的容器       |
| docker exec -it xxx bash       | 进入某个容器             |
| docker run -d -P image_name/id | 随机映射启动的端口       |
| docker info                    | 查看docker所有的详细信息 |
| docker version                 | 查看docker版本信息       |
| docker rm \`docker ps -a -q\`  | 删除所有docker容器       |
| ip a show docker0              | 查看docker0的网络        |

