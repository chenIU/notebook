`mvn compile`：编译

`mvn  install`：包含`mvn compile`、`mvn package`然后上传到本地仓库

`mvn deploy`：包含`mvn compile`、`mvn package`、`mvn install`然后上传到私服



## 常用mvn命令

`mvn compile`：编译源码

`mvn test-compile`：编译测试代码

`mvn -Dtest package`：只打包，不测试

`mvn test`：运行测试代码

`mvn package`：打包

`mvn install`：安装到本地仓库

`mvn deploy`：部署到私服

`mvn clean`：清除产生的项目