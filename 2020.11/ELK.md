# 利用ELK搭建docker容器化应用日志中心



## 镜像准备

+ ElasticSearch镜像
+ Logstash镜像
+ Kibana镜像
+ Nginx镜像（作为容器化应用来生产日志）



## 开启linux系统的rsyslog服务

修改rsyslog配置文件

```bash
vim /etc/rsyslog.conf
```



开启下面三个参数

```bash
$ModLoad imtcp
$InputTCPServerRun 514

*.* @@localhost:4560
```

让rsyslog加载imtcp模块并监听514端口，然后将rsyslog中收集的数据转发到本地4560端口。



重启rsyslog服务

```bash
systemctl restart rsyslog
```



查看rsyslog启动状态

```bash
netstat -tnl
```



## 部署ElasticSearch服务

```bash
docker run -d  -p 9200:9200 -p 9300:9300 -v ~/elasticsearch/data:/usr/share/elasticsearch/data -e ES_JAVA_OPTS="-Xms256m -Xmx256m" -e "discovery.type=single-node" --name elasticsearch elasticsearch:7.9.3
```



**错误1**：

内存不足

**解决方法**：

```bash
-e ES_JAVA_OPTS="-Xms512m -Xmx512m"
```



**错误2**：

权限不足

```bash
nested: AccessDeniedException[/usr/share/elasticsearch/data/nodes]
```

**解决法**：

```bash
chmod 777 ~/elasticsearch/data
```



**错误3**：

```bash
the default discovery settings are unsuitable for production use; at least one of [discovery.seed_hosts, discovery.seed_providers, cluster.initial_master_nodes] must be configured
```

**解决方法**：

```bash
-e "discovery.type=single-node"
```



## 部署Logstash服务

添加/usr/local/elk/logstash/logstash.conf，配置如下：

```bash
input {
  syslog {
    type => "rsyslog"
    port => 4560
  }
}

output {
  elasticsearch {
    hosts => [ "localhost:9200" ]
  }
}
```

配置中，让Logstash从本地的rsyslog服务中读取应用日志数据，然后转发到ElasticSearch数据库中。

配置完成后，启动Logstash容器：

```bash
docker run -d -p 4560:4560 -v /usr/local/elk/logstash/logstash.conf:/etc/logstash.conf -e LS_JAVA_OPTS="-Xms256m -Xmx256m" --link elasticsearch:elasticsearch --name logstash logstash:7.9.3 logstash -f /etc/logstash.conf
```



**错误1**：

```bash
OpenJDK 64-Bit Server VM warning: INFO: os::commit_memory(0x00000000c5330000, 986513408, 0) failed; error='Not enough space' (errno=12)
```

**解决方法**：

```bash
-e LS_JAVA_OPTS="-Xms256m -Xmx256m"
```



## 部署Kibana服务

```bash
docker run -d -p 5601:5601 --link elasticsearch:elasticsearch -e ELASTICSEARCH_URL=http://localhost:9200 --name kibana kibana:7.9.3
```



## 启动nginx容器生产日志

```bash
docker run -d -p 90:80 --log-driver syslog --log-opt syslog-address=tcp://localhost:514 --log-opt tag="nginx" --name nginx nginx
```

docker容器中的nginx应用日志转发到本地syslog服务中，然后由syslog服务将数据转给logstash进行收集。至此，日志中心搭建完毕。



## 验证

+ 浏览器打开`http://localhost:90`，打开nginx界面，刷新几次，让后台产生GET请求的日志
+ 打开Kibana可视化界面：`http://localhost:5601`
+ 收集nginx应用日志
+ 查询应用日志：在查询框中输入`program=nginx`，可查询出特定日志