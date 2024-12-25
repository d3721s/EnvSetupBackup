# sudo免密码
```sh
sudo visudo
```
 # apt换源
 ```sh
sudo su
cat <<'EOF' > /etc/apt/sources.list
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse

# 以下安全更新软件源包含了官方源与镜像站配置，如有需要可自行修改注释切换
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# deb http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse
# # deb-src http://security.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# # deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
EOF
```
# apt更新
```sh
sudo apt update && sudo apt upgrade
```
# 安装软件
```sh
sudo apt install net-tools openssh-server git curl wget bash python3-pip nano 
```

# docker
```sh
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do apt-get remove $pkg; done
```
## 首先安装依赖：
```sh
apt-get update
apt-get install ca-certificates curl gnupg
```
## 信任 Docker 的 GPG 公钥并添加仓库：
```sh
install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  tee /etc/apt/sources.list.d/docker.list > /dev/null
```
## 最后安装
```sh
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

# docker-cross
```sh
sudo docker pull --platform arm64 ubuntu:20.04
sudo docker run --rm --privileged multiarch/qemu-user-static:register --reset
wget https://github.com/multiarch/qemu-user-static/releases/download/v7.2.0-1/qemu-aarch64-static
tar -xvf qemu-aarch64-static.tar.gz \
&& chmod 755 qemu-aarch64-static \
&& sudo cp qemu-aarch64-static /usr/bin/qemu-aarch64-static


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
