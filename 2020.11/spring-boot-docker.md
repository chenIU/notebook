一键部署 Spring Boot项目到远程 Docker容器



## 准备工作

### 准备Docker

以CentOS7为例，修改`/usr/lib/systemd/system/docker.service`配置文件，加入以下内容：

```bash
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375 -H unix://var/run/docker.sock
```

配置完成后，保存退出，然后重启Docker

```bash
systemctl daemon-reload
systemctl restart docker
```



### 准备IDEA

在IDEA上安装Docker插件，添加连接信息

![image-20201110161217391](http://cdn.chenjianyin.com/markdown/spring-boot-docker-1.png)



### 项目准备

创建一个简单的Spring Boot项目，只需要引入`spring-boot-starter-web`依赖即可。项目创建成功之后，再写一个controller，用来测试。如下：

```java
@RestController
public class HelloDockerController {

    @GetMapping("hello")
    public String hello(){
        return "hello docker!";
    }
}
```



## 配置Dockerfile

在项目的根目录下，创建一个Dockerfile，作为镜像的构建文件，具体位置如下：

![image-20201110154625821](http://cdn.chenjianyin.com/markdown/spring-boot-docker-2.png)

文件内容容下：

```bash
FROM hub.c.163.com/library/java:latest
VOLUME /tmp
ADD target/docker-0.0.1-SNAPSHOT.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

**简单说明**：

+ Spring Boot项目依赖Java环境，所以镜像基于Java镜像构建

+ Spring Boot项目运行时需要 tmp 目录，这里数据卷配置一个/tmp目录出来

+ 将本地target目录打包好的.jar文件复制一份到/app.jar

+ 最后配置启动命令

  

## 配置Maven插件

在pom.xml中，配置如下插件

```xml
<plugin>
    <groupId>com.spotify</groupId>
    <artifactId>docker-maven-plugin</artifactId>
    <version>1.2.0</version>
    <executions>
        <execution>
            <id>build-image</id>
            <phase>package</phase>
            <goals>
                <goal>build</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <dockerHost>http://192.168.66.131:2375</dockerHost>
        <imageName>javaboy/${project.artifactId}</imageName>
        <imageTags>
            <imageTag>${project.version}</imageTag>
        </imageTags>
        <forceTags>true</forceTags>
        <dockerDirectory>${project.basedir}</dockerDirectory>
        <resources>
            <resource>
                <targetPath>/</targetPath>
                <directory>${project.build.directory}</directory>
                <include>${project.build.finalName}.jar</include>
            </resource>
        </resources>
    </configuration>
</plugin>
```

**简单说明**

+ 首先在 execution 节点配置当执行 mvn package 的时候，顺便也执行 docker:build
+ 然后在 configuration 节点配置 Docker的主机地址、镜像名称、镜像的 tags。其中 dockerDirectory 用来指定 Dockerfile的位置
+ 最后在 resource 节点配置 jar 的位置和名称



## 打包运行

接下来对项目进行打包，打包完成后会自动生成一个镜像并上传到Docker容器中。打包方式如下：

![image-20201110155555172](http://cdn.chenjianyin.com/markdown/spring-boot-docker-3.png)

### 运行方式一

此时，可以直接在Linux容器中像创建普通一样创建这个容器，然后启动即可。如下：

![image-20201110155839862](http://cdn.chenjianyin.com/markdown/spring-boot-docker-4.png)

```bash
docker run -d -p 8080:8080 --name spring-boot-docker overmind/docker:0.0.1-SNAPSHOT
```

启动成功之后，即可访问容器中的接口。



### 运行方式二

利用IDEA中的Docker插件运行

![image-20201110160124558](http://cdn.chenjianyin.com/markdown/spring-boot-docker-5.png)

此时，选中这个镜像，右键单击，即可基于此镜像创建一个容器。如下：

![image-20201110160253582](http://cdn.chenjianyin.com/markdown/sping-boot-docker-6.png)

配置完成之后，点击左上方的`run`按钮，即可运行。如下：

![image-20201110161139185](http://cdn.chenjianyin.com/markdown/spring-boot-docker-7.png)