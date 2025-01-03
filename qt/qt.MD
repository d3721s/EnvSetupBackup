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
sudo apt update && sudo apt upgrade -y
```
# 安装软件
```sh
sudo apt install -y net-tools openssh-server git curl wget bash python3-pip  ca-certificates
sudo apt install -y build-essential gdb 
sudo apt install -y cmake

```
# code 
```sh
sudo snap install code --classic
```

# qt下载
```sh
wget https://mirrors.tuna.tsinghua.edu.cn/qt/official_releases/online_installers/qt-unified-linux-x64-online.run
chmod +x qt-unified-linux-x64-online.run
sudo apt install libxcb-cursor0 libxcb-cursor-dev
./qt-unified-linux-x64-online.run --mirror https://mirrors.ustc.edu.cn/qtproject
```

















