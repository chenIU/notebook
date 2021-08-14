## 单节点

### STEP 1: 获取kafka

[Download](https://www.apache.org/dyn/closer.cgi?path=/kafka/2.8.0/kafka_2.13-2.8.0.tgz) the latest Kafka release and extract it:

```shell
tar -zxf kafka_2.13-2.8.0.tgz
cd kafka_2.13-2.8.0
```



### STEP 2: 启动服务

zookeeper：

```shell
bin/zookeeper-server-start.sh config/zookeeper.properties
```

kafka-server：

```shell
bin/kafka-server-start.sh config/server.properties
```



### STEP 3: 创建topic

```shell
bin/kafka-topics.sh --create --topic iot --replication-factor 2 --partitions 3 --bootstrap-server localhost:9092
```

查看信息：

```shell
bin/kafka-topics.sh --describe --topic quickstart-events --bootstrap-server localhost:9092
```



### STEP 4: 生产消息

```shell
bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
```



### STEP 5: 消费消息

```shell
bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
```

