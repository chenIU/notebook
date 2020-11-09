# Centos7上安装 Jenkins

## 安装

```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
yum install jenkins
```



## 启动

```bash
systemctl start jenkins  #启动
systemctl status jenkins #查看状态
systemctl stop jenkins   #停止
```

