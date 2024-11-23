# sudo免密码
```sh
sudo visudo
runyu ALL=(ALL) NOPASSWD: ALL
```

# apt换源
```sh
sudo nano /etc/apt/sources.list
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
sudo apt install build-essential gdb codeblocks gcc-aarch64-linux-gnu cmake net-tools openssh-server git curl
```

# 一键代理
```sh
git clone https://ghp.ci/https://github.com/nelvko/clash-for-linux-install.git && cd clash-for-linux-install && sudo bash -c '. install.sh; exec bash' && cd 
```

# 安装字体等
```sh
git clone https://github.com/snwh/ubuntu-post-install.git && cd ubuntu-post-install && ./ubuntu-post-install-script.sh
```

# 关闭休眠
```sh
```

# qt
```sh
sudo apt install libxcb-cursor0 libxcb-cursor-dev
wget https://mirrors.cloud.tencent.com/qt/archive/online_installers/4.8/qt-online-installer-linux-x64-4.8.0.run
./qt-online-installer-linux-x64-4.8.0.run --mirror https://mirrors.cloud.tencent.com/qt
```
## qt
