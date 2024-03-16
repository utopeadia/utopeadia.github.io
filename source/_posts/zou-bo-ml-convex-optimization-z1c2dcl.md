---
title: 邹博ml凸优化
date: '2020-03-03 22:10:25'
updated: '2020-03-03 22:10:25'
excerpt: >-
  本文介绍了凸集和凸函数的基本概念。凸集是指任意两点之间的线段都在该集合内的集合。凸函数是指函数图像上方区域构成的凸集。文章还介绍了仿射集、超平面、半空间、欧式球、椭球、范数球、范数锥、二阶锥和多面体等重要的几何概念,并阐述了它们与凸集的关系。这些概念为后续学习凸优化问题奠定了基础。
tags:
  - 凸集
  - 凸函数
  - 仿射集
  - 超平面
categories:
  - ML&DL
permalink: /post/zou-bo-ml-convex-optimization-z1c2dcl.html
comments: true
toc: true
---



## 主要内容

* 凸集的基本概念
* 凸函数的基本概念
* 凸优化的一般提法

## 凸集基本概念

### 思考两个不能式

两个正数的算术平均数大于等于几何平均数
![截屏2020-03-03下午2.14.42](https://img.wush.cc/16311026291474.png?imageView2/0/format/webp/q/80)
给定可逆对称阵Q，对于任意向量x,y，有：
![截屏2020-03-03下午2.15.32](https://img.wush.cc/16311026291497.png?imageView2/0/format/webp/q/80)

### 思考凸集和凸函数

在机器学习中，我们把形如
![截屏2020-03-03下午2.16.26](https://img.wush.cc/16311026291507.png)![截屏2020-03-03下午2.16.45](https://img.wush.cc/16311026291517.png?imageView2/0/format/webp/q/80)
这样的图形的都称为凸函数。
*$y=x^2$是凸函数，函数图像上位于$y=x^2$的区域构成凸集。

* 凸函数图像的上方区域，一定是凸集；
* 一个函数图像的上方区域为凸集，则该函数是凸函数。

### 直线的向量表达

已知二维平面上的两定点A(5,1)，B(2,3)尝试给出经过带你AB的直线方程：
![截屏2020-03-03下午2.20.42](https://img.wush.cc/16311026291527.png?imageView2/0/format/webp/q/80)
写成向量形式：
![截屏2020-03-03下午2.21.11](https://img.wush.cc/16311026291539.png?imageView2/0/format/webp/q/80)
其中：![截屏2020-03-03下午2.21.26](https://img.wush.cc/16311026291552.png?imageView2/0/format/webp/q/80)

### 几何体的向量表达

已知二维平面上的两个定点![截屏2020-03-03下午2.38.54](https://img.wush.cc/16311026291566.png?imageView2/0/format/webp/q/80)，则：
![截屏2020-03-03下午2.39.28](https://img.wush.cc/16311026291580.png?imageView2/0/format/webp/q/80)
推广到高维：
![截屏2020-03-03下午2.40.05](https://img.wush.cc/16311026291595.png?imageView2/0/format/webp/q/80)

### 仿射集(Affine set)

定义：通过集合C中任意两个不同点的直线仍然在集合C内，则称集合C为仿射集。
![截屏2020-03-03下午2.42.37](https://img.wush.cc/16311026291612.png?imageView2/0/format/webp/q/80)
仿射集的例子：直线、平面、超平面
超平面：$Ax=b$
f(x)=0表示定义域在$R^n$的超曲面：令$f(x)=Ax-b$，则$f(x)=0$表示截距为b的超平面。
n维空间的n-1维仿射集为n-1维超平面

### 凸集

集合C内任意两点间的线段均在集合C内，则称集合C维凸集。

> 注意和仿射集区分
> ![截屏2020-03-03下午2.53.36](https://img.wush.cc/16311026291629.png?imageView2/0/format/webp/q/80)
> 仿射集是凸集的一种特殊形式，仿射集一定是凸集。
> k个点的版本：
> ![截屏2020-03-03下午2.55.46](https://img.wush.cc/16311026291646.png) ![截屏2020-03-03下午2.56.13](https://img.wush.cc/16311026291665.png?imageView2/0/format/webp/q/80)

### 凸包

集合C的所有点的凸组合所形成的集合，叫做集合C的凸包：
![截屏2020-03-03下午2.57.24](https://img.wush.cc/16311026291687.png?imageView2/0/format/webp/q/80)
集合C的凸包是能够包含C的最小凸集。
![截屏2020-03-03下午2.58.17](https://img.wush.cc/16311026291710.png?imageView2/0/format/webp/q/80)

### 超平面和半空间

超平面：hyperplane

$$
{xa^Tx=b}
$$

半空间：halfspace

$$
{xa^Tx\le b}$$$${xa^Tx\ge b}
$$

![截屏2020-03-03下午3.04.26](https://img.wush.cc/16311026291735.png?imageView2/0/format/webp/q/80)

### 欧式球和椭球

欧式球
![截屏2020-03-03下午3.05.24](https://img.wush.cc/16311026291760.png?imageView2/0/format/webp/q/80)
椭球
![截屏2020-03-03下午3.05.51](https://img.wush.cc/16311026291787.png?imageView2/0/format/webp/q/80)

### 范数球和范数锥（欧式空间推广）

![截屏2020-03-03下午3.16.34](https://img.wush.cc/16311026291812.png?imageView2/0/format/webp/q/80)
###$R^3$空间中的二阶锥
![截屏2020-03-03下午3.19.54](https://img.wush.cc/16311026291841.png?imageView2/0/format/webp/q/80)

### 多面体

有限个半空间和超平面的交集。
![截屏2020-03-03下午3.20.52](https://img.wush.cc/16311026291873.png?imageView2/0/format/webp/q/80)
仿射集(如超平面、直线)、射线、线段、半空间都是多面体
多面体是凸集
此外，有界的多面体有时称作多胞体(Polytope)
![截屏2020-03-03下午3.22.39](https://img.wush.cc/16311026291906.png?imageView2/0/format/webp/q/80)

### 保持凸性运算

* 集合交运算
* 仿射变换
* 透视变换
* 投射变换（线性分式变换）
  集合交运算：半空间的交
  ![截屏2020-03-03下午3.28.07](https://img.wush.cc/16311026291941.png?imageView2/0/format/webp/q/80)
  仿射变换
  ![截屏2020-03-03下午3.28.31](https://img.wush.cc/16311026291985.png?imageView2/0/format/webp/q/80)
  透视变换
  ![截屏2020-03-03下午3.31.38](https://img.wush.cc/16311026292030.png?imageView2/0/format/webp/q/80)
  投射函数（线性分式函数）
  ![截屏2020-03-03下午3.32.29](https://img.wush.cc/16311026292087.png?imageView2/0/format/webp/q/80)

### 分割超平面

设C和D为两不相交的凸集，则存在超平面P，P可以将C和D分离。
![截屏2020-03-03下午3.44.48](https://img.wush.cc/16311026292140.png) ![截屏2020-03-03下午3.45.24](https://img.wush.cc/16311026292190.png?imageView2/0/format/webp/q/80)
分割超平面的构造：
![截屏2020-03-03下午3.45.50](https://img.wush.cc/16311026292239.png?imageView2/0/format/webp/q/80)

### 支撑超平面

设集合C，x0是C边界上的点，若存在$a\not=0$。满足对任意$x\in C$，都有![截屏2020-03-03下午3.48.41](https://img.wush.cc/16311026292292.png)成立，则称超平面![截屏2020-03-03下午3.49.23](https://img.wush.cc/16311026292344.png?imageView2/0/format/webp/q/80)为集合C在点x0处的支撑超平面。
凸集边界上任意一点，均存在支撑超平面。
反之，若一个闭的非中空集合，在边界上任意一点存在支撑超平面，则该集合为凸集。

## 凸函数

若函数f的定义域domf为凸集，且满足：
![截屏2020-03-03下午3.53.35](https://img.wush.cc/16311026292394.png?imageView2/0/format/webp/q/80)

### 一阶可微

若f一阶可微，则函数f为凸函数，当且仅当f的定义域domf为凸集，且：
![截屏2020-03-03下午3.55.34](https://img.wush.cc/16311026292447.png?imageView2/0/format/webp/q/80)
分析![截屏2020-03-03下午3.55.57](https://img.wush.cc/16311026292501.png?imageView2/0/format/webp/q/80)
对于凸函数，其一阶Taylor近似本质上是该函数的全局下估计。
反之如果一个函数的一阶Taylor近似总是其全局下估计，则该函数是凸函数
该不等式说明从一个函数的局部信息，可以得到一定车程度的全局信息。

### 二阶可微

若函数f二阶可微，则函数f为凸函数当且进档dom为凸集，且：
![截屏2020-03-03下午3.58.40](https://img.wush.cc/16311026292555.png?imageView2/0/format/webp/q/80)
若f为一元函数，上式表示二阶导大于等于0
若f是多元函数，上式表示二阶导Hessian矩阵半正定。
凸函数举例：
![截屏2020-03-03下午4.00.33](../../../Library/Application%20Support/typora-user-images/%E6%88%AA%E5%B1%8F2020-03-03%E4%B8%8B%E5%8D%884.00.33.png)

### 上镜图

函数f的图像定义为：![截屏2020-03-03下午4.05.48](https://img.wush.cc/16311026292611.png?imageView2/0/format/webp/q/80)
函数f的上镜图(epigraph)定义为
![截屏2020-03-03下午4.06.30](https://img.wush.cc/16311026292666.png?imageView2/0/format/webp/q/80)

### Jensen不等式：若f是凸函数

基本Jensen不等式
![截屏2020-03-03下午4.31.59](https://img.wush.cc/16311026292722.png?imageView2/0/format/webp/q/80)
若：
![截屏2020-03-03下午4.32.21](https://img.wush.cc/16311026292779.png?imageView2/0/format/webp/q/80)
则：
![截屏2020-03-03下午4.32.45](https://img.wush.cc/16311026292837.png?imageView2/0/format/webp/q/80)
若：
![截屏2020-03-03下午4.33.07](https://img.wush.cc/16311026292895.png?imageView2/0/format/webp/q/80)
则：
![截屏2020-03-03下午4.33.26](https://img.wush.cc/16311026292954.png?imageView2/0/format/webp/q/80)
Jensen不等式是几乎所有不等式的基础

### 保持函数凸性的算子

![截屏2020-03-03下午4.35.48](https://img.wush.cc/16311026293016.png?imageView2/0/format/webp/q/80)

### 凸函数的逐点最大值

若$f_1,f_2$均为凸函数，定义函数$f$：
![截屏2020-03-03下午4.37.43](https://img.wush.cc/16311026293077.png?imageView2/0/format/webp/q/80)
则函数$f$为凸函数。
证明：
![截屏2020-03-03下午4.38.13](https://img.wush.cc/16311026293143.png?imageView2/0/format/webp/q/80)
第二个不等号的表达：
![截屏2020-03-03下午4.38.48](https://img.wush.cc/16311026293208.png?imageView2/0/format/webp/q/80)
第二个不等好的形式化表达：
![截屏2020-03-03下午4.39.16](https://img.wush.cc/16311026293278.png?imageView2/0/format/webp/q/80)

### 共轭函数

原函数![截屏2020-03-03下午4.39.46](https://img.wush.cc/16311026293350.png?imageView2/0/format/webp/q/80)，共轭函数定义：
![截屏2020-03-03下午4.40.09](https://img.wush.cc/16311026293425.png?imageView2/0/format/webp/q/80)
显然，定义式的右端是关于y的仿射函数，他们逐点求上确界，得到的函数f\*（y）一定是凸函数。
理解：
![截屏2020-03-03下午4.41.39](https://img.wush.cc/16311026293497.png?imageView2/0/format/webp/q/80)
例：
求共轭函数![截屏2020-03-03下午4.42.09](https://img.wush.cc/16311026293572.png?imageView2/0/format/webp/q/80)
![截屏2020-03-03下午4.42.30](https://img.wush.cc/16311026293650.png?imageView2/0/format/webp/q/80)

### Fenchel不等式

根据共轭函数定义：
![截屏2020-03-03下午4.43.25](https://img.wush.cc/16311026293725.png?imageView2/0/format/webp/q/80)
易得：
![截屏2020-03-03下午4.43.48](https://img.wush.cc/16311026293822.png?imageView2/0/format/webp/q/80)
应用：
![截屏2020-03-03下午4.44.11](https://img.wush.cc/16311026293916.png?imageView2/0/format/webp/q/80)

## 凸优化

### 凸优化问题的基本形式：

![截屏2020-03-03下午4.44.57](https://img.wush.cc/16311026294015.png?imageView2/0/format/webp/q/80)

* 优化变量：$x \in R^n$
* 不等式约束：$f_i(x)\le0$
* 等式约束：$h_j(x)=0$
* 无约束优化：$m=p=0$
* 优化问题的域：
  ![截屏2020-03-03下午4.50.31](https://img.wush.cc/16311026294100.png?imageView2/0/format/webp/q/80)
* 可行点（解）(feasible)
  ![截屏2020-03-03下午4.51.22](https://img.wush.cc/16311026294184.png?imageView2/0/format/webp/q/80)
* 可行域（可解集）
  所有可行点的集合。
* 最优化值
  ![截屏2020-03-03下午4.52.11](https://img.wush.cc/16311026294267.png?imageView2/0/format/webp/q/80)
* 最优化解
  ![截屏2020-03-03下午4.52.31](https://img.wush.cc/16311026294354.png?imageView2/0/format/webp/q/80)
  对于
  ![截屏2020-03-03下午4.44.57](https://img.wush.cc/16311026294015.png?imageView2/0/format/webp/q/80)
  其中
  $f_i(x)$为凸函数，$h_j(x)$为仿射函数
  凸优化问题的重要性质：
* 凸优化问题的可行域为凸集
* 凸优化问题的局部最优解就是<span style="font-weight: bold;" class="bold">全局最优解</span>

### 对偶问题

一般优化问题的Lagrange乘子法
Lagrange函数：![截屏2020-03-03下午5.01.00](https://img.wush.cc/16311026294516.png?imageView2/0/format/webp/q/80)
对于固定的x，Lagrange函数$L(x,\lambda,v)$是关于$\lambda$和v的仿射函数。

### Lagrange对偶函数

Langrange对偶函数：
![截屏2020-03-03下午5.05.08](https://img.wush.cc/16311026294606.png?imageView2/0/format/webp/q/80)
若没有下确界，定义：
![截屏2020-03-03下午5.06.41](https://img.wush.cc/16311026294757.png?imageView2/0/format/webp/q/80)
根据定义，显然有：对![截屏2020-03-03下午5.07.21](https://img.wush.cc/16311026294858.png?imageView2/0/format/webp/q/80)，若原优化问题有最优值P\*,则：
![截屏2020-03-03下午5.08.01](https://img.wush.cc/16311026294946.png?imageView2/0/format/webp/q/80)
进一步：Lagrange函数对偶函数为凹函数。
![截屏2020-03-03下午5.08.57](https://img.wush.cc/16311026295049.png?imageView2/0/format/webp/q/80)

### 鞍点解释

![截屏2020-03-03下午5.09.59](https://img.wush.cc/16311026295139.png) ![截屏2020-03-03下午5.10.19](https://img.wush.cc/16311026295237.png?imageView2/0/format/webp/q/80)
<span style="font-weight: bold;" class="bold">鞍点：最优点</span>
![截屏2020-03-03下午5.10.55](https://img.wush.cc/16311026295331.png?imageView2/0/format/webp/q/80)

### 强对偶条件

若要对偶函数的最大值即为原问题的最小值，需要满足的条件：
![截屏2020-03-03下午5.13.06](https://img.wush.cc/16311026295435.png?imageView2/0/format/webp/q/80)

### Karush-Kuhn-Tucker(KKT)条件

![截屏2020-03-03下午5.15.03](https://img.wush.cc/16311026295550.png?imageView2/0/format/webp/q/80)
