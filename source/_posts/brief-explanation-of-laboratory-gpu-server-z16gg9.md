---
title: 实验室GPU服务器使用简要说明
date: '2023-01-12 13:00:31'
updated: '2023-01-12 13:00:31'
excerpt: >-
  本文介绍了服务器的基本情况和连接方式。服务器拥有两块GPU:RTX3090
  24G和泰坦12G,采用Docker容器化管理。容器只保留/home/ubuntu和/data目录,其他目录不保留。可通过Zerotier加入网络后使用SSH连接服务器,传输文件不宜使用sftp,大文件建议使用wget从网络下载。
tags:
  - 服务器
  - gpu
  - docker
  - 连接
  - 管理员
categories:
  - 搞机日志
permalink: /post/brief-explanation-of-laboratory-gpu-server-z16gg9.html
comments: true
toc: true
---



## 基本情况

服务器目前拥有两台GPU，分别为:
GPU0-RTX3090 24G
GPU1-泰坦 12G
![](https://img.wush.cc/231216171645-image.png?imageView2/0/format/webp/q/80)
使用前请务必检查服务器负载，因为使用人数较少不进行个人资源限制。 <span style="font-weight: bold;" class="bold">因管理员太菜，容器出现问题修不了，只能删机重来（甚至删机命令都是百度的），请务必明确自己发出的每一条指令，备份好自己的重要数据，不要当做存储！</span>

```shell
nvidia-smi
```

服务器通过 docker 进行虚拟化和管理，所以容器中只保留 </br>
 <span style="font-weight: bold;" class="bold">/home/ubuntu</span> </br>
 <span style="font-weight: bold;" class="bold">/data</span> </br>
两个目录内的文件。也就是说，自己安装的软件和这两个目录之外的东西都不会进行保留！容器已经内置了 nvidia 驱动、cuda、conda。
如有问题，请联系现任<span style="font-weight: bold;" class="bold">管理员：吴树晖</span>

## 连接方式

* 公网连接</br>

1、下载[zerotier](https://www.zerotier.com/)，<span style="font-weight: bold;" class="bold">不需要注册</span>，直接下载客户端！加入网络:【联系管理员获取】 </br>
2、联系管理员同意授权网络</br>
3、通过 SSH 进行连接，访问192.168.67.100:<管理员授权的端口>利用用户名 (默认为 ubuntu)及密码登录，传输文件不要使用 sftp 直接传数据集或者大文件（线路优化使用了流量转发做优化，线路流量挺贵的，钱包顶不住），公共数据集请使用 wget 等从网络直连下载（也就是先存个网盘或者找到下载链接，然后直接下载到服务器）</br>
