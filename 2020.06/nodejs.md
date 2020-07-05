# n

## 安装n

n是nodejs管理工具，是TL写的，[github](https://github.com/tj/n)

## 安装nodejs版本

安装最新版

```bash
n latest
```

安装指定版

```bash
n 8.11.3
```

安装稳定版

```bash
n stable
```

安装最新的LTS官方版本

```bash
n lts
```

## 切换nodejs版本

```bash
n
```

## 切换失效解决方法

+ 查看node当前安装路径

```bash
which node 
/usr/local/bin/node
```

+ 而 n 默认安装路径是 /usr/local，若你的 node 不是在此路径下，n 切换版本就不能把bin、lib、include、share 复制该路径中，所以我们必须通过N_PREFIX变量来修改 n 的默认node安装路径。
  编辑环境配置文件：

```bash
vi ~/.bash_profile
```

+ 将下面两行代码插入到文件末尾：

```bash
export N_PREFIX=/usr/local #node实际安装位置
export PATH=$N_PREFIX/bin:$PATH
```

+ :wq保存退出

+ 执行source使保存生效	

```bash
source ~/.bash_profile
```



# npm

| 命令                        | 描述                             |
| --------------------------- | -------------------------------- |
| npm config set registry xxx | 添加镜像源                       |
| npm config get registry     | 查看镜像源                       |
| npm cache clean -f          | npm清理缓存                      |
| npm root -g                 | 查看全局node包(node_moudles)     |
| npm get prefix              | 查看node安装路径                 |
| npm ls                      | 查看当前目录安装哪些node包       |
| npm add user                | 添加用户                         |
| npm login                   | 登录                             |
| npm whoami                  | 查看当前用户                     |
| npm init                    | 初始化目录                       |
| npm publish xxx             | 发布到本地                       |
| npm install xxx             | 安装                             |
| npm -g install xxx          | 全局安装                         |
| npm uninstall               | 卸载                             |
| npm update xxx              | 更新                             |
| npm -g update xxx           | 全局更新                         |
| npm outdated xxx            | 检查模块是否过时                 |
| npm run                     | 执行package.json中定义的脚本命令 |
| npm publish xxx             | 发布包                           |
| npm -f unpublish xxx        | 撤销发布                         |
| npm start xxx               | 启动模块                         |
| npm stop xxx                | 停止模块                         |
| npm restart xxx             | 重新启动模块                     |
| npm test xxx                | 测试模块                         |
| npm version                 | 查看模块的版本                   |
| npm view                    | 查看模块的注册信息               |
| npm adduser                 | 添加用户                         |
| npm audit                   | node项目审计信息                 |
| npm config list(ls)         | npm配置信息                      |
| npm config set prefix xxx   | 设置node_global                  |
| npm config set cache xxx    | 设置node_cache                   |



# nvm

nvm的参数基本上都没有中划线，这一点需要额外注意。

| 命令               | 描述                     |
| ------------------ | ------------------------ |
| nvm list           | 查看下载的node版本       |
| nvm list available | 查看所有可下载的node版本 |
| nvm install xxx    | 安装某个node版本         |
| nvm uninstall xxx  | 卸载某个node版本         |
| nvm use            | 使用某个node版本         |
| nvm on             | 启用node.js版本管理      |
| nvm off            | 禁用node.js版本管理      |
| nvm v(version)     | 查看nvm的版本            |



# express

express是nodejs的一个web框架，express升级到4.0之后需要额外安装express-generator。

## 1.安装模块

```bash
npm install express --save -g
npm install express-generator --save -g
```

## 2.创建项目

```bash
express xxx
```

## 3.安装依赖

```bash
npm install
```

## 4.启动

```bash
npm start
```



**npm install参数**

-g：全局安装

-s(--save)：安装到当前项目的依赖中

-d(-D)：安装到当前项目的dev依赖中，生产环境依赖不添加安装的模块或者插件

npm install xxx = install i xxx