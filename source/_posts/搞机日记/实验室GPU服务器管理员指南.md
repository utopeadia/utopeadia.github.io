## 基本情况
服务器目前拥有两台GPU，分别为:
GPU0-RTX3090 24G
GPU1-泰坦 12G
![](https://img.wush.cc/231216171645-image.png?imageView2/0/format/webp/q/80)
使用前请务必检查服务器负载，因为使用人数较少不进行个人资源限制。 **因管理员太菜，容器出现问题修不了，只能删机重来（甚至删机命令都是百度的），请务必明确自己发出的每一条指令，备份好自己的重要数据，不要当做存储！**
```shell
nvidia-smi
```
服务器通过 docker 进行虚拟化和管理，所以容器中只保留 </br>
**/home/ubuntu** </br>
**/data** </br>
两个目录内的文件。也就是说，自己安装的软件和这两个目录之外的东西都不会进行保留！容器已经内置了 nvidia 驱动、cuda、conda。
如有问题，请联系现任**管理员：吴树晖**
## 连接方式
* 公网连接</br>
1、下载[zerotier](https://www.zerotier.com/)，**不需要注册**，直接下载客户端！加入网络:【联系管理员获取】 </br>
2、联系管理员同意授权网络</br>
3、通过 SSH 进行连接，访问192.168.64.100:<管理员授权的端口>利用用户名 (默认为 ubuntu)及密码登录，传输文件不要使用 sftp 直接传数据集或者大文件（线路优化使用了流量转发做优化，线路流量挺贵的，钱包顶不住），公共数据集请使用 wget 等从网络直连下载（也就是先存个网盘或者找到下载链接，然后直接下载到服务器）</br>

--- **下面内容仅供管理员参考记录** ---
## 容器部署：
使用了： [ https://github.com/gezp/docker-ubuntu-desktop ](https://github.com/gezp/docker-ubuntu-desktop) 项目进行部署。
Docker 默认镜像版本为：
```shell
docker pull gezp/ubuntu-desktop:22.04-cu11.7.1
```
复制模板文件：
```shell
cp -r /home/wsh/dockermnt/template /home/wsh/dockermnt/weixintong
```
启动 docker:
```shell
docker run -d --restart=always --name weixintong --cap-add=SYS_PTRACE --gpus all --shm-size=1024m -e USER=XXX -e PASSWORD=XXX -v /home/wsh/dockermnt/weixintong/home:/home/ubuntu -v /home/wsh/dockermnt/weixintong/data:/data -p XXX:22 gezp/ubuntu-desktop:22.04-cu11.7.1
```
## 所有人配置保存
```shell
# 加密内容，请查看私有仓库
```
--- **下面内容已被弃用** ---
## 宿主机 LXD 设置
* 添加清华镜像站

```shell
sudo lxc remote add tuna-images https://mirrors.tuna.tsinghua.edu.cn/lxc-images/ --protocol=simplestreams --public
```
创建镜像
* lxc launch <镜像源>:<镜像名> <容器名>

```shell
lxc launch tuna-images:ubuntu/22.04 user
```
* 进入容器并修改密码

```shell
lxc exec user bash
```
> 此方法进入为root用户，其中内置一个ubuntu用户

```shell
passwd root
passwd ubuntu
```
* 安装openssh便于用户访问

```shell
apt-get install openssh-server
```
* 注意首次进入系统请先安装显卡驱动！！！**

```shell
sudo apt-get update
sudo apt-get install wget
wget https://cn.download.nvidia.com/XFree86/Linux-x86_64/535.104.05/NVIDIA-Linux-x86_64-535.104.05.run --no-check-certificate
```