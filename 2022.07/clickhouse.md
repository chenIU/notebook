## 1.创建相关配置目录

```shell
mkdir -P /data/clickhouse/conf
mkdir -P /data/clickhouse/data
mkdir -P /data/clickhouse/log
```



## 2.拉取镜像

```shell
# 下载最新版本clickhouse
docker pull yandex/clickhouse-server
# 下载指定版本clickhouse
docker pull yandex/clickhouse-server:20.3.5.21
```



## 3. 创建临时容器，用以生成配置文件

```shell
docker run -d --name clickhouse-server --ulimit nofile=262144:262144 \
-p 8123:8123 -p 9000:9000 -p 9009:9009 \
-v /data/clickhouse/data/:/var/lib/clickhouse \
-v /data/clickhouse/conf/:/etc/clickhouse-server/ \
-v  /data/clickhouse/log:/var/log/clickhouse-server \
yandex/clickhouse-server
```



## 4.将配置文件复制到宿主机对应目录下

```shell
docker cp clickhouse-server:/etc/clickhouse-server/config.xml /data/clickhouse/conf/config.xml
docker cp clickhouse-server:/etc/clickhouse-server/users.xml /data/clickhouse/conf/users.xml
```



## 5.修改用户名、密码

```xml
<users>
	<default>
		<password>********</password>
	</default>
</users>
```



## 6.关闭临时容器

```shell
docker stop clickhouse-server
```



## 7.启动容器

```shell
docker run -d --name=clickhouse-server \
-e TZ="Asia/Shanghai" \
-p 8123:8123 \
-p 9009:9009 \
-p 9090:9000 \
--ulimit nofile=262144:262144 \
-v /data/clickhouse/data:/var/lib/clickhouse:rw \
-v /data/clickhouse/conf/config.xml:/etc/clickhouse-server/config.xml \
-v /data/clickhouse/conf/users.xml:/etc/clickhouse-server/users.xml \
-v /data/clickhouse/log:/var/log/clickhouse-server:rw \
yandex/clickhouse-server
```



[Dockerfile](https://hub.docker.com/r/yandex/clickhouse-server/dockerfile)