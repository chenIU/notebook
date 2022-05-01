**wsl数据迁移**

1. 关闭docker

   

2. 关闭所有发行版

   

3. 将原数据导入到执行目录

   ```bash
   wsl --export docker-desktop-data E:\docker\wsl\docker-desktop-data\docker-desktop-data.tar
   ```

   

4. 注销docker-desktop-data

   ```bash
   wsl --unregister docker-desktop-data
   ```

   

5. 重新导入新目录下的数据文件

   ```bash
   wsl --import docker-desktop-data E:\docker\wsl\docker-desktop-data\ E:\docker\wsl\docker-desktop-data\docker-desktop-data.tar --version 2
   ```





**注**：

wsl发行版默认安装在C盘，在%LOCALDATA%/Docker/wsl目录

docker的运行数据，镜像文件存放在%LOCALDATA%/Docker/wsl/data/ext4.vhdx中



`wsl -l -v`：列出所有的wsl运行版本