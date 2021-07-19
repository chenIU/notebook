# 安装和美化zsh



## 安装`oh-my-zh`

```sh
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

+ 升级zsh：`upgrade_oh_my_zh` 或 `omz_update`
+ 卸载zsh：`uninstall_oh_my_zsh`



## 安装插件

目录位置：`~/.oh-my-zsh/custom/plugins`

+ `zsh-autosuggestions`
+ `zsh-syntax-highlighting`

配置：编辑`.zshrc`文件

```sh
plugins=(git zsh-autosuggestions)

source ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```



## 安装主题

主题名称：`powerlevel10k`

前置条件：需要zsh5.1及以上

下载：

```sh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

目录位置：`~/.oh-my-zsh/custom/themes`

配置：

```sh
source ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

命令：`p10k configure`



## 安装字体

`powershell10k`需要特殊字体，如果遇到乱码问题，到[特殊字体下载地址](https://github.com/romkatv/powerlevel10k)。







## [升级zsh]

[下载地址](https://sourceforge.net/projects/zsh/files/zsh/)

查看当前`zsh`版本：`echo $ZSH_VERSION`

### 下载

```sh
wget https://sourceforge.net/projects/zsh/files/zsh/5.8/zsh-5.8.tar.xz/download
```



### 编译

```sh
./configure
```



### 安装

```sh
make && make install
```



如果遇到缺少依赖问题，执行：

```sh
yum install 2048-cli-nocurses.x86_64
```



替换shell：

```sh
sudo chsh -s /bin/zsh
```



