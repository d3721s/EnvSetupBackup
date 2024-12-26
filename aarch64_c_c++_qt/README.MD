# wsl安装
```sh
wsl --install -d Ubuntu-20.04 
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
```
# sudo免密码
```sh
sudo visudo
```
```sh
# 加在最后一行
runyu   ALL=(ALL) NOPASSWD: ALL
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
# qt交叉编译环境
```sh

```




# docker
```sh
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do apt remove $pkg; done
```
## 首先安装依赖：
```sh
apt update
apt install ca-certificates curl gnupg
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
apt update
apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
# dockerhub 镜像加速
```sh
echo '{"registry-mirrors": ["https://docker.1ms.run"]}' | sudo tee /etc/docker/daemon.json > /dev/null
systemctl daemon-reload
systemctl restart docker

```

# docker-cross
```sh
sudo docker pull --platform arm64 ubuntu:20.04
sudo apt install qemu-user-static
sudo docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
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
#镜像内换源
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