# 将WSL迁移到其他盘 
[learning-resources/WSL.md at master · DevInsideYou/learning-resources (github.com)](https://github.com/DevInsideYou/learning-resources/blob/master/WSL.md)
1. cmd/powershell下查看当前的分发版
```bash
wsl --list -v
```
2. 停止子系统/或者直接停止所有子系统
```bash
wsl --terminate Ubuntu-20.04

# wsl --shutdown
```
3. 导出安装的Ubuntu20.04
```bash
wsl --export Ubuntu-20.04 Ubuntu-20.04.tar
```
4. 删除安装在C盘的Ubuntu20.04
```bash
wsl --unregister Ubuntu-20.04
```
5. 导入第三步导入的包, 子系统名字可以和原来一样，也可以自定义
```
 wsl --import Ubuntu-20.04 D:\WSL\Ubuntu-20.04 D:\VM\BackUp\Ubuntu-20.04.tar
```
6. （有用与否未知）释放压缩的虚拟磁盘资源，找到导入文件存放的目录，
```bash
 Optimize-VHD -Path D:\WSL\Ubuntu-20.04\ext4.vhdx -Mode Full
```
7. 更换默认登陆用户，cmd/powershell运行
```bash
# 子系统名字 config --default-user lk
ubuntu2004 config --default-user lk
```


# 更换镜像源
1. 备份原有的配置文件
```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```
2. 修改`/etc/apt/sources.list`, 替换为清华大学镜像
```bash
sudo vim /etc/apt/sources.list
```

```properties
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse

deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# deb http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse
# # deb-src http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```
3. 然后执行下述代码，更新仓库
```bash
sudo apt update
```

# 启用systemd
1. 在[https://github.com/microsoft/WSL/releases](https://github.com/microsoft/WSL/releases)上下载wsl(0.67.6或更高版本),安装
2. 在子系统中
```bash
sudo vim /etc/wsl.conf
```
输入
```bash
[boot]
systemd=true
```
# 安装docker
## 使用apt安装
 1.  由于 `apt` 源使用 HTTPS 以确保软件下载过程中不被篡改。因此，我们首先需要添加使用 HTTPS 传输的软件包以及 CA 证书。
```bash
sudo apt-get update

sudo apt-get install \
	apt-transport-https \
	ca-certificates \
	curl \
	gnupg \
	lsb-release
```
2. 添加软件源的GPG密钥
```bash
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg


# 官方源
# curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

```
3. 向source.list中添加Docker软件源
```bash
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://mirrors.aliyun.com/docker-ce/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null


# 官方源
# echo \
#   "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
#   $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

```
> 以上命令会添加稳定版本的 Docker APT 镜像源，如果需要测试版本的 Docker 请将 stable 改为 test。
4. 安装docker
```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
5. 将docker设为开机自启，开启docker
```bash
sudo systemctl enable docker
sudo systemctl start docker
```
6. 建立docker用户组并添加当前用户
```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```
7. 推出当前终端，重新进入
8. 测试docker是否安装成功
```bash
docker run -rm hello-world
```
## 设置镜像
10. 查看是否在docker.service文件中是否配置过镜像地址
```bash
systemctl cat docker | grep '\-\-registry\-mirror'
```
11. 如果没有输出，则在/etc/docker/daemon.json中写入如下内容
```bash
sudo vim /etc/docker/daemon.json
```
```json
{
  "registry-mirrors": [
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com"
  ]
}
```
12. 重启服务
```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```
13. 检查镜像是否生效
```bash
docker info
```
成功时：
```html
	/*
	 Registry Mirrors:
		 https://hub-mirror.c.163.com/
	*/
```

## 安装docker-compose
1. 下载
```bash
sudo curl -L https://ghproxy.com/docker/compose/releases/download/v2.15.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
```
2. 给权限
```bash
sudo chmod +x /usr/local/bin/docker-compose
```

# 升级python
[How to upgrade to Python 3.10 on Ubuntu 18.04 and 20.04 LTS - isw blog (itsupportwale.com)](https://www.itsupportwale.com/blog/how-to-upgrade-to-python-3-10-on-ubuntu-18-04-and-20-04-lts/)

# 安装oh my zsh
1. 安装zsh
```bash
sudo apt install zsh
```
2. 将zsh设为默认shell
```shell
chsh -s /bin/zsh
```

3. 用脚本安装Oh My zsh
```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
OR
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```
4. 安装插件   
	在用户目录的.oh-myzsh的plugins目录下已有部分插件
	推荐开启：
	- git 在进入克隆下来的仓库目录时，会显示当前的分支
	- zsh-autosuggestions 自动提示
	- minikube 命令行补全

	1. 克隆要加载的插件仓库
	```bash
	git clone https://ghproxy.com/https://github.com/zsh-users/zsh-autosuggestions.git
	```
	2. 修改~/.zshrc，找到plugins，添加上要使用的插件
	```bash
		plugins=(
			git
			zsh-autosuggestions
			)
	```
	3. 重新开启一个终端

# 安装V2rayA
1. 安装V2ray内核
```bash
curl -Ls https://mirrors.v2raya.org/go.sh | sudo bash
```
2. 关闭V2ray服务
```bash
sudo systemctl disable v2ray --now
```
3. 添加公钥
```bash
wget -qO - https://apt.v2raya.org/key/public-key.asc | sudo tee /etc/apt/trusted.gpg.d/v2raya.asc
```
4. 添加软件源码
```bash
echo "deb https://apt.v2raya.org/ v2raya main" | sudo tee /etc/apt/sources.list.d/v2raya.list
sudo apt update
```
5. 安装V2rayA
```bash
sudo apt install v2raya
```
6. 打开v2rayA
```bash
sudo systemctl start v2raya.service
```
7. 设置开机自启
```bash
sudo systemctl enable v2raya.service
```

# 使用Python
1. 安装pip
	```bash
	sudo apt install python3-pip
	```
2. pip换源
	1. 编辑配置文件
		```bash
		vim ~/.pip/pip.conf
		```
	2. 添加
		```bash
		[global] 
			index-url = https://pypi.tuna.tsinghua.edu.cn/simple 
		[install] 
			trusted-host = https://pypi.tuna.tsinghua.edu.cn
		```
1.  安装添加虚拟环境所用的包
	```bash
	sudo apt install python3-venv
	```
4. 创建虚拟环境
	```bash
	python3 -m venv 虚拟环境名称
	```
5. 激活虚拟环境
	```bash
	source 虚拟环境名称/bin/activate
	```

6. 退出虚拟环境，在虚拟环境中
	```bash
	deactivate
	```

# vim更换主题
1. 创建~/.vim文件夹
```bash
mkdir ~/.vim
```
2. 创建~/.vim/color文件存放主题文件
```bash
mkdir ~/.vim/color
```
3. 在guthub上下下载vim为后缀的颜色文件并放入上一步创建的文件夹中
4. 创建vim配置文件
```bash
vim ~/.vimrc
```
5. 设置字体，在~/.vimrc文件中写入
```
syntax on
colorscheme gruvbox
set background=dark


set number
```
