---
title: Anaconda安装教程
tags: []
id: '137'
categories:
  - - Python
comments: true
date: 2020-01-08 22:18:38
---

# Anaconda安装教程

### anaconda简介

Anaconda是一个方便的python包管理和环境管理软件，一般用来配置不同的项目环境。我们常常会遇到这样的情况，正在做的项目A和项目B分别基于python2和python3，而第电脑只能安装一个环境，这个时候Anaconda就派上了用场，它可以创建多个互不干扰的环境，分别运行不同版本的软件包，以达到兼容的目的。 Anaconda通过管理工具包、开发环境、Python版本，大大简化了你的工作流程。不仅可以方便地安装、更新、卸载工具包，而且安装时能自动安装相应的依赖包，同时还能使用不同的虚拟环境隔离不同要求的项目。

### anaconda安装-以windows为例

anaconda的安装可以通过[官网下载](https://www.anaconda.com/distribution/)也可以使用国内的镜像站，比如[清华镜像站](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)，选择anaconda3的最新版本即可。 下载完成后就是正常的安装 ![](https://img.wush.cc/16311033266533.jpg) ![](https://img.wush.cc/16311033266555.jpg) ![](https://img.wush.cc/16311033266572.jpg) ![](https://img.wush.cc/16311033266591.jpg)

*   注意这里有两个勾选，第一个的意思是将anaconda添加到系统环境，第二个勾选是将anaconda自带的Python3.7作为系统默认python，我一般全部勾选
*   这样就可以使用了。
    
    ### 测试
    
    在命令提示行（cmd）中输入
    
    ```
    conda --version
    ```
    
    可以看到版本号, 输入
    

```
python
```

能够进入Python编译环境