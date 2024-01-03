---
title: 手动安装VMware虚拟机Ubuntu工具包
tags: []
id: '202'
categories:
  - - 搞机日记
date: 2021-07-12 13:00:31
---

使用VMware虚拟机虚拟ubuntu环境时，有时无法自动安装VMware-tools，有时在安装后会失效，导致复制粘贴自适应屏幕等功能失效，我们需要手动安装工具包。

## 如果之前安装过vm-tools

```shell
sudo apt-get autoremove open-vm-tools
sudo apt-get install open-vm-tools
sudo apt-get install open-vm-tools-desktop
```

## 如果没有安装过

```shell
sudo apt-get install open-vm-tools
sudo apt-get install open-vm-tools-desktop
```