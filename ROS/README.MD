```sh

sudo passwd root

sudo visudo

runyu    ALL=(ALL) NOPASSWD: ALL

su

apt install curl

bash <(curl -sSL https://linuxmirrors.cn/main.sh) \
  --source mirrors.tuna.tsinghua.edu.cn \
  --protocol https \
  --use-intranet-source false \
  --install-epel false \
  --backup true \
  --upgrade-software false \
  --clean-cache false \
  --ignore-backup-tips


snap install cmake --classic
snap install code --classic

apt upgrade
apt install git 
wget http://fishros.com/install -O fishros && . fishros

```