---
title: nginx误删nginx.conf文件如何恢复
tags: []
id: '404'
categories:
  - - Web开发
date: 2021-10-11 14:06:22
---

当你不小心误删或者错误操作导致nginx.conf文件丢失，而且nginx处于**运行**的状态,在这种状况下就能够在内存中获取配置文件

## 获取Nginx进程的PID

执行

```shell
ps aux  grep nginx
```

得到如下输出，找到**master**进程的pid

```shell
[root@VM-8-3-centos /]# ps aux  grep nginx
root      6958  0.0  0.0 112812   968 pts/0    R+   09:10   0:00 grep --color=auto nginx
root     19193  0.0  0.3 109440  6360 ?        Ss   Jun08   0:00 nginx: master process nginx
root     22326  0.0  0.3 112200  7412 ?        S    01:47   0:01 nginx: worker process
```

可以看到nginx的进程pid为19193。

## 查找内存映射

接下来需要查看过程正在应用哪些内存映射。

```shell
sudo cat /proc/19193/maps  grep heap
```

```shell
[root@VM-8-3-centos /]# sudo cat /proc/19193/maps  grep heap
5581bf774000-5581bf8b7000 rw-p 00000000 00:00 0                          [heap]
5581bf8b7000-5581bfa50000 rw-p 00000000 00:00 0                          [heap]
```

只需要关注\[heap\]局部。内存位于5581bf774000–5581bf8b7000和5581bf8b7000–5581bfa50000之间。

## 转储堆

使用gbd

```shell
sudo gdb -p 19193
```

你会失去一个(gdb)提醒。当初在这个提醒下应用咱们之前记下的地址，地址需要使用十六进制（0x）。

```shell
(gdb) dump memory /tmp/nginx-memory 0x5581bf774000 0x5581bf8b7000
```

## 从转储中获取字符串数据

有了内存转储。大多数配置都会有 _http {_ 一行。

```shell
grep -A 20 "http {" /tmp/nginx-memory.str
```

```shell
[root@VM-8-3-centos /]# grep -A 20 "http {" /tmp/nginx-memory.str
http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
    gzip on;
    # 
gzip
    gzip_min_length 1k;
    # gzip 
1-10
    gzip_comp_level 6;
    # 
javascript
    # 
 mime.types 
    gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png;
    # 
http header
Vary: Accept-Encoding
    gzip_vary on;
    # 
```

## 把 /tmp/nginx-memory.str下载到本地

下载后调整格式就能找到原有的配置。

（本文转载自[乐趣区](https://lequ7.com/guan-yu-nginx-wu-shan-nginxconf-wen-jian-ru-he-hui-fu.html)）