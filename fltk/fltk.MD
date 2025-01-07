
# wsl安装

```sh
wsl --install -d Ubuntu-22.04 
```
# wsl配置
```sh
sudo nano /etc/wsl.conf
```
```conf
[boot]
systemd=true
[automount]
enabled=false
[interop]
enabled=false
appendWindowsPath=false
[user]
default=runyu
```
# apt换源
```sh
sudo su
cat <<'EOF' > /etc/apt/sources.list
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
# deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
# deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
# deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse

# 以下安全更新软件源包含了官方源与镜像站配置，如有需要可自行修改注释切换
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
# deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse

# deb http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
# # deb-src http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-proposed main restricted universe multiverse
# # deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-proposed main restricted universe multiverse
EOF
```
# sudo免密码
```sh
sudo visudo
```

```sh
# 加在最后一行
runyu   ALL=(ALL) NOPASSWD: ALL
```

# apt更新
```sh
sudo apt update && sudo apt upgrade
```

# 安装软件
```sh
sudo apt install net-tools openssh-server git curl wget bash python3-pip  ca-certificates
```
# 安装软件

```sh
sudo apt-get install libx11-dev

sudo apt install build-essential cmake gcc-aarch64-linux-gnu g++-aarch64-linux-gnu libglew-dev libglfw3-dev
```
# code 
```sh
sudo snap install code --classic
```
# fltk