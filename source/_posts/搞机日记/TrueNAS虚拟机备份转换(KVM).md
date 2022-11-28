---
title: TrueNAS虚拟机备份转(KVM)
tags: []
categories:
  - - 搞机日记
comments: true
date: 2022-10-02 21:27:22
---

## 虚拟机导出

TrueNAS Scale虚拟化使用ZVOL存储虚拟机，存储路径为：

```shell
/dev/zvol
```

使用dd命令可将虚拟机打包为raw格式的img文件：

```shell
dd if=/dev/zvol/SSD/VM/WINServer-0w4sx9 of=/mnt/DATA/downloads/winserver.img
```

![](https://image.aiwush.com/2022102212022-10-02-21-38-32-image.png)

其中if为源文件即为zvol文件，of为导出目的文件。

## 格式转换

使用qemu-img可以进行压缩和格式转换例如:

```shell
qemu-img convert -f raw -O qcow2 /mnt/DATA/downloads/winserver.img /mnt/DATA/downloads/winserver.qcow2
```

其中 -f表示源文件格式，-O表示目的文件格式。支持vhd、vmdk、qcow2、raw、vhdx、qcow、vdi和qed格式的镜像的相互转换

转换后可以进行扩容：

```shell
qemu-img resize /mnt/DATA/downloads/winserver.qcow2  +1G
```

## 虚拟机导入

可以使用dd命令在新建zvol文件之后导入zvol文件:

```shell
dd if=/mnt/DATA/downloads/winserver.img of=/dev/zvol/SSD/VM/winserver-1
```

zvol本质上是raw的流文件，所以可以直接使用qemu-img转换导入:

```shell
qemu-img convert -f qcow2 -O raw /mnt/DATA/downloads/winserver.qcow2 /dev/zvol/SSD/VM/winserver-1
```