# Centos7 上安装 Elastic Search

## 下载elasctic search 7.9.3

```bash
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.9.3-linux-x86_64.tar.gz
tar -zxvf elasticsearch-7.9.3-linux-x86_64.tar.gz
cd elasticsearch-7.9.3/
```



## 启动

```bash
cd bin
./elasticsearch
```

**错误1**：

```bash
OpenJDK 64-Bit Server VM warning: INFO: os::commit_memory(0x00000000c0000000, 1073741824, 0) failed; error='Not enough space' (errno=12)
        at org.elasticsearch.tools.launchers.JvmErgonomics.flagsFinal(JvmErgonomics.java:126)
        at org.elasticsearch.tools.launchers.JvmErgonomics.finalJvmOptions(JvmErgonomics.java:88)
        at org.elasticsearch.tools.launchers.JvmErgonomics.choose(JvmErgonomics.java:59)
        at org.elasticsearch.tools.launchers.JvmOptionsParser.jvmOptions(JvmOptionsParser.java:137)
        at org.elasticsearch.tools.launchers.JvmOptionsParser.main(JvmOptionsParser.java:95)
```



**解决方法**：

由于elasticsearch默认需要1g内存，通过配置文件改小一点。

```bash
vim config/jvm.options  
-Xms1g  →  -Xms512m
-Xmx1g  →  -Xmx512m
```



**错误2**：

```bash
can not run elasticsearch as root
```



**解决方法**：

在 Linux 环境中，elasticsearch 不允许以 root 权限来运行！所以需要创建一个非root用户，以非root用户来起es。

```bash
groupadd elk #创建用户组elk
useradd elk -g elk  -p 123456 #创建用户并指定用户组和密码
chown -R elk:elk /usr/local/elasticsearch-7.9.3/ #修改权限
su elk #切换到elk用户
```



修改配置文件elasticsearch.yml文件，使得外网也可以访问。

```yml
network.host 0.0.0.0
```



**错误3**：

```bash
[1]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
```



**解决方法**：

切换到root用户

```bash
echo "vm.max_map_count=262144" > /etc/sysctl.conf
sysctl -p
```



**错误4**：

```bash
[1]: the default discovery settings are unsuitable for production use; at least one of [discovery.seed_hosts, discovery.seed_providers, cluster.initial_master_nodes] must be configured
```



**解决方法**：

修改elasticsearch.yml

```bash
node.name: node-1
cluster.initial_master_nodes: ["node-1"]
```



外网访问成功！

![image-20201109104729890](http://cdn.chenjianyin.com/markdown/elastic-search-1.png)

**后台启动**：

```bash
./elasticsearch -d
```



## 安装可视化插件 elasticsearch-head

node的版本不能太高

```bash
git clone git://github.com/mobz/elasticsearch-head.git
cd elasticsearch-head
npm install
npm run start
```



**跨域问题**：

修改elasticsearch.yml

```yaml
http.cors.enabled: true
http.cors.allow-origin: "*"
```



访问可视化界面

![image-20201109111343452](http://cdn.chenjianyin.com/markdown/elasticsearch-2.png)

