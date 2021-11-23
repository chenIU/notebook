## 1.安装gcc

```shell
yum install gcc gcc-c++
```



## 2.下载node国内镜像

```shell
https://npm.taobao.org/mirrors/node/v17.0.0/node-v17.0.0-linux-x64.tar.gz
```



## 3.解压并重命名文件夹

```shell
tar -xvf  node-v10.14.1-linux-x64.tar.gz
mv node-v10.14.1-linux-x64 /usr/local/node
```



## 4.添加环境配置

```shell
vi /etc/profile

export NODE_HOME=/usr/local/node
export PATH=$NODE_HOME/bin;$PATH
```



## 5.刷新配置

```shell
source /etc/profile
```



## 6.验证结果

```shell
node -v

npm -v
```