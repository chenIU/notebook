## 生成项目

+ mvn eclipse:eclipse  生成eclipse项目结构
+ mvn idea:idea 生成idea项目结构



## 编译项目

+ mvn compile：编译源代码
+ mvn test-compile：编译测试代码



## 测试项目

+ mvn test



## 打包项目

+ mvn package
+ mvn -Dtest package：打包并测试
+ mvn clean package -DskipTests -Prelease：跳过测试并打包



## 安装项目

+ mvn install
+ mvn jar:jar：打成jar
+ mvn clean install -DskipTests：安装项目到本地仓库



## 清除项目

+ mvn clean



## 查看错误

+ mvn -e：查看错误的详细信息
+ mvn install -x：发生jar冲突的显示冲突的原因