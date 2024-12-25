# sudo免密码
```sh
sudo visudo
```

```
# 加在最后一行
runyu   ALL=(ALL) NOPASSWD: ALL
```

# apt换源
```sh
cat <<'EOF' > /etc/apt/sources.list
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.zju.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.zju.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.zju.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.zju.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.zju.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.zju.edu.cn/ubuntu/ focal-backports main restricted universe multiverse

# 以下安全更新软件源包含了官方源与镜像站配置，如有需要可自行修改注释切换
deb https://mirrors.zju.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.zju.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# deb http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse
# # deb-src http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.zju.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# # deb-src https://mirrors.zju.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
EOF
```

```sh
sudo nano /etc/apt/sources.list
```
```sh
deb http://mirrors.tencent.com/ubuntu/ jammy main restricted universe multiverse
deb http://mirrors.tencent.com/ubuntu/ jammy-security main restricted universe multiverse
deb http://mirrors.tencent.com/ubuntu/ jammy-updates main restricted universe multiverse
deb http://mirrors.tencent.com/ubuntu/ jammy-backports main restricted universe multiverse
#deb http://mirrors.tencent.com/ubuntu/ jammy-proposed main restricted universe multiverse
```

# apt更新
```sh
sudo apt update && sudo apt upgrade
```

# 安装软件
```sh
sudo apt install build-essential gdb gcc-aarch64-linux-gnu g++-aarch64-linux-gnu cmake qtcreator 
sudo apt install net-tools openssh-server git curl wget bash python3-pip nano 
sudo apt install 
 
```

# 一键代理
```sh
git clone https://mirror.ghproxy.com//https://github.com/nelvko/clash-for-linux-install.git && cd clash-for-linux-install && sudo bash -c '. install.sh; exec bash' && cd 
```

```sh
#图形化代理
wget https://github.com/2dust/v2rayN/releases
```

# 安装字体等
```sh
git clone https://github.com/snwh/ubuntu-post-install.git && cd ubuntu-post-install && ./ubuntu-post-install-script.sh
```

# qt(在线安装包)
```sh
sudo apt install libxcb-cursor0 libxcb-cursor-dev
wget https://mirrors.cloud.tencent.com/qt/archive/online_installers/4.8/qt-online-installer-linux-x64-4.8.0.run
./qt-online-installer-linux-x64-4.8.0.run  --mirror https://mirrors.ustc.edu.cn/qtproject
```

## qt5(apt方式)
```sh 

sudo apt-get install qtcreator  qtbase5-dev qt5-qmake qtbase5-dev-tools  qtmultimedia5-dev libqt5charts5-dev  qtdeclarative5-dev  qttools5-dev-tools

```

# ROS
```sh
wget http://fishros.com/install -O fishros && . fishros
```

# code 
```sh
sudo snap install code --classic
```

## pip换源
```sh
pip config set global.index-url https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple
```

## code插件（建议同步）
```sh
code --install-extension ms-vscode.cpptools
code --install-extension ms-python.python
code --install-extension ms-vscode.cpptools-extension-pack
code --install-extension ms-vscode.cpptools-themes
code --install-extension ms-vscode.makefile-tools
code --install-extension ms-vscode.remote-explorer
code --install-extension ms-vscode.remote-server
code --install-extension mhutchie.git-graph
code --install-extension ms-vscode.hexeditor
code --install-extension ms-azuretools.vscode-docker
code --install-extension alibaba-cloud.tongyi-lingma
```

# miniconda
```sh
wget https://repo.anaconda.com/miniconda/Miniconda3-py39_4.12.0-Linux-x86_64.sh
bash Miniconda3-py39_4.12.0-Linux-x86_64.sh
conda init bash
conda install -c conda-forge cmake
conda install -c conda-forge llvm-tools
```

# docker
```sh
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

# docker-cross
```sh
sudo docker pull --platform arm64 ubuntu:20.04
sudo docker run --rm --privileged multiarch/qemu-user-static:register --reset
wget https://github.com/multiarch/qemu-user-static/releases/download/v5.2.0-1/qemu-aarch64-static
tar -xvf qemu-aarch64-static.tar.gz \
&& chmod 755 qemu-aarch64-static \
&& sudo cp qemu-aarch64-static /usr/bin/qemu-aarch64-static


sudo docker run \
-itd \
--privileged=true \
--restart=always \
--name ubuntu20.04_aarch64 \
--platform arm64 \
-v /svn:/svn \
-v /usr/bin/qemu-aarch64-static:/usr/bin/qemu-aarch64-static \
-v /tmp/.X11-unix:/tmp/.X11-unix \
-e DISPLAY=unix$DISPLAY \
-e GDK_SCALE \
-e GDK_DPI_SCALE \
ubuntu:20.04

sudo docker exec -it ubuntu20.04_aarch64 /bin/bash
```
# docker-cross-run
```sh
sudo docker run --rm --privileged multiarch/qemu-user-static:register --reset
sudo docker run \
-itd \
--privileged=true \
--restart=always \
--name ubuntu20.04_aarch64 \
--platform arm64 \
-v /usr/bin/qemu-aarch64-static:/usr/bin/qemu-aarch64-static \
-v /tmp/.X11-unix:/tmp/.X11-unix \
-e DISPLAY=unix$DISPLAY \
-e GDK_SCALE \
-e GDK_DPI_SCALE \
ubuntu:20.04

sudo docker exec -it ubuntu20.04_aarch64 /bin/bash
sudo docker commit -m="init" -a="runyu" 56bf7a1e4a26 runyu/ubuntu20.04_aarch64:v1
```
# 
```sh
export DISPLAY=172.17.0.1
````
# ubuntu-port 
```sh
cat <<'EOF' > /etc/apt/sources.list
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal main restricted universe multiverse
# deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-updates main restricted universe multiverse
# deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-updates main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-backports main restricted universe multiverse
# deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-backports main restricted universe multiverse

# 以下安全更新软件源包含了官方源与镜像站配置，如有需要可自行修改注释切换
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-security main restricted universe multiverse
# deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-security main restricted universe multiverse

# deb http://ports.ubuntu.com/ubuntu-ports/ focal-security main restricted universe multiverse
# # deb-src http://ports.ubuntu.com/ubuntu-ports/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-proposed main restricted universe multiverse
# # deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-proposed main restricted universe multiverse
EOF
```
