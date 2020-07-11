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



# 总结

**容器内安装软件**

> 容器内安装软件
>
> + apt-get update
> + apt-get install vim





| 命令                           | 解释                     |
| ------------------------------ | ------------------------ |
| docker ps -l                   | 最后一次创建的容器       |
| docker exec -it xxx bash       | 进入某个容器             |
| docker run -d -P image_name/id | 随机映射启动的端口       |
| docker info                    | 查看docker所有的详细信息 |
| docker version                 | 查看docker版本信息       |

