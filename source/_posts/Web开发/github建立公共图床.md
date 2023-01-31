---
title: Github建立公共图床
tags: []
id: '64'
categories:
  - - Web开发
comments: true
date: 2019-06-12 21:45:17
---

*   这种行为其实并不友好，不推荐使用，github的服务器有限，建议仅作为备用方案或者临时存储！\***虽然我的大部分博客使用的腾讯云的对象存储（COS）作为图床，但是腾讯云的免费对象存储空间结束了，购买资源西南地区大致存储资源包50元/12月+下行流量9元/3月，价格较为高昂，而使用GitHub或者Gitee作为图床就显得很舒服。**本篇文章虽然是使用Picgo作为图床的发布软件,但是使用git等上传是一样的。\*\*
    
*   * * *
    
*   方便程度：★★★★☆
    
*   配置难度：★★☆☆☆
    
*   适用环境：win + mac + linux
    
*   需要工具：GitHub 账号+Picgo
    
*   稳定性：背靠 GitHub比自建服务器稳定多了
    
*   隐私性：既然选择建立公共图床，在乎什么隐私性
    
*   最大缺点：会给你的GitHub账号增加不少无效代码的小绿点V_V
    

## 1 GitHub端操作

#### 1.1 建立GitHub公共仓库

点击 GitHub 主页右上角的 **+** 创建 **New repository**；

![截屏2019-12-1616.37.18](https://img.how1e.com/16311055228377.png)

填写仓库信息，例如我就创建了一个pic_bad的仓库。这里注意，仓库得设置为Public因为后面通过客户端访问算是外部访问，因此无法访问Private，这样的话图片传上来之后只能存储不能显示。所以要设置为Public。

#### 1.2 获取takon并复制保存

![截屏2019-12-1616.53.06](https://img.how1e.com/16311055228412.png)

在个人下拉菜单点击**Settings**

![截屏2019-12-1616.53.24](https://img.how1e.com/16311055228435.png)

左侧菜单选择**Developer settings**

![截屏2019-12-1616.53.46](https://img.how1e.com/16311055228460.png)

左侧菜单选择**Personal access tokens**； 点击右侧**Generate new token**

![截屏2019-12-1616.54.04](https://img.how1e.com/16311055228486.png)

Note随便写一下，选项选择repo

![截屏2019-12-1616.54.09](https://img.how1e.com/16311055228516.png)

点击**Generate token**

![截屏2019-12-1616.54.37](https://img.how1e.com/16311055228545.png)

可以获得takon,复制并保存下来_这个值只出现一次，无法再现_

## 2 使用Picgo上传图片

#### 2.1Picgo设置

![截屏2019-12-1617.05.54](https://img.how1e.com/16311055228577.png)

*   仓库名：即你的仓库名\[username\]/\[仓库名\]
*   分支名：默认 master【2021-9-1注：main?自己看看就好】
*   Token：就是刚刚复制的那一串字符
*   存储路径:这个可以填也可以不填，填了的话图片就上传到img这个文件夹
*   域名:格式https://raw.githubusercontent.com/\[username\]/\[仓库名\]/master

![截屏2019-12-1617.08.42](https://img.how1e.com/16311055228624.png)确定即可。

#### 2.2 图床使用

这个就很简单了。。。拖进去即可上传，然后可以获得一个类似于这样的地址

```
![](https://raw.githubusercontent.com/errormepl/pic_bad/master/img/截屏2019-12-1616.53.24.png)
```

可以直接插入到markdown中。

## 3 最后

这种行为其实并不友好，不推荐使用，github的服务器有限，建议仅作为备用方案或者临时存储！抵制白嫖从我做起.