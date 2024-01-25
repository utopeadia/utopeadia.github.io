---
title: (ML邹博)回归
tags: []
id: '121'
categories:
  - - MLorDL
comments: true
date: 2020-03-17 22:13:41
---

## 线性回归

对于单个变量：

y=ax+b

![截屏2020-03-04下午6.45.22](https://img.wush.cc/16311019408756.png?imageView2/0/format/webp/q/80)

对于多个变量：

![截屏2020-03-04下午6.46.34](https://img.wush.cc/16311019408781.png) ![截屏2020-03-04下午6.46.52](https://img.wush.cc/16311019408807.png?imageView2/0/format/webp/q/80)

### 使用极大似然估计解释最小二乘法

$y^{(i)}=\theta^{T}x^{(i)}+\varepsilon^{(i)}$

误差$\varepsilon^{(i)}(1\le i\le m)$是独立同分布的，服从均值为0，方差为某定值$\sigma^{2}$的**高斯分布**。

> 原因：中心极限定理

### 中心极限定理的意义

在实际问题中，很多随机现象可以看做众多因素独立影响的综合反应，往往近似服从正态分布。

![截屏2020-03-04下午6.54.09](https://img.wush.cc/16311019408832.png?imageView2/0/format/webp/q/80)

* 应用前提是多个**随机变量的和**，有些问题是乘性误差，则需要鉴别或者取对数后使用。

### 似然函数

$y^{(i)}=\theta^{T}x^{(i)}+\varepsilon^{(i)}$

![截屏2020-03-04下午6.58.04](https://img.wush.cc/16311019408858.png?imageView2/0/format/webp/q/80)

### 高斯的对数似然与最小二乘

![截屏2020-03-04下午7.06.15](https://img.wush.cc/16311019408886.png?imageView2/0/format/webp/q/80)

### $\theta$的解析式求解过程

将M个N维样本组成矩阵X:

* x的每一行对应一个样本，共M个样本(measurements)
* X的每一列对应样本的一个维度，共N维(regressors)
  * 还有额外的一维常数项，全为1

目标函数

![截屏2020-03-04下午7.13.21](https://img.wush.cc/16311019408918.png?imageView2/0/format/webp/q/80)

梯度

![截屏2020-03-04下午7.13.41](https://img.wush.cc/16311019408946.png?imageView2/0/format/webp/q/80)

### 最小二乘意义下的系数最优解

参数的解析式：

![截屏2020-03-04下午7.18.53](https://img.wush.cc/16311019408975.png) ![截屏2020-03-04下午7.19.26](https://img.wush.cc/16311019409006.png?imageView2/0/format/webp/q/80)

加入$\lambda$扰动后：

$X^TX$半正定：对于任意非零向量u

![截屏2020-03-04下午7.20.33](https://img.wush.cc/16311019409036.png?imageView2/0/format/webp/q/80)

所以，对于任意实数$\lambda>0$，$X^TX+\lambda I$正定，从而可逆，保证回归公式有意义。![截屏2020-03-04下午7.21.37](https://img.wush.cc/16311019409067.png?imageView2/0/format/webp/q/80)

### 线性回归的复杂度惩罚因子

线性回归的目标函数为：

#### ![截屏2020-03-04下午7.22.17](https://img.wush.cc/16311019409099.png?imageView2/0/format/webp/q/80)

将目标函数增加平方和损失；

![截屏2020-03-04下午7.23.03](https://img.wush.cc/16311019409134.png?imageView2/0/format/webp/q/80)

本质即为假定参数$\theta$服从高斯分布。
