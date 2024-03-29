---
title: KL散度
date: '2023-11-27 14:20:38'
updated: '2023-11-27 14:20:38'
excerpt: >-
  这篇文章介绍了KL散度(Kullback–Leibler
  divergence)的概念和推导过程。首先介绍了熵的定义,然后通过熵的推广得到了KL散度的公式。KL散度可以用于衡量两个概率分布之间的差异,具有非负性质,但不具有对称性。文章最后总结了KL散度的两个重要性质:非负性和不对称性。
tags:
  - kl散度
  - 熵概念
  - 非对称
  - 非负性
  - 概率分布
categories:
  - ML&DL
comments: true
toc: true
---
## KL 散度简介

KL 散度（Kullback–Leibler divergence）又称相对熵，是表示一个概率分布相对于另一个概率分布的差异的统计量。

## 什么是熵？

设离散型概率空间$X$的概率分布为$P$，对于$X=(x_1,x_2,x_3,...,x_n)$和对应的$P=\{p_i=p(X=x_i)\}$, 有 X 的熵：

$$
H(X)=-\sum_{i=1}^{n}{p(x_i)lnp(x_i)}
$$

且有若$p (x_i)=0$，则$p (x_i) logp (x_i)=0$（吉布斯不等式？）
对于连续型概率空间，则有：

$$
H(X)=-\int_{i=1}^{n}{p(x_i)lnp(x_i)dx}
$$

## KL 散度的推导

将熵的概念进行推广，若有两个分布$P、Q$，概率分布分别为$p(x)、q(x)$，规定 :$P$为真实分布，$Q$为预测分布，那么两随机变量的交叉熵为：

$$
H(P,Q)=-\sum p(x)ln{q(x)}
$$

KL 散度可以用来衡量两个分布之间的差异，可以得到推导：

$$
D_{KL}(P||Q)=H(P,Q)-H(P)
$$

即：

$$
D_{KL}(P||Q)=-\sum {p(x)ln{\frac{p(x)}{q(x)}}}
$$

或：

$$
D_{KL}(P||Q)=-\int {p(x)ln{\frac{p(x)}{q(x)}}dx}
$$

## KL 散度的性质

* KL 散度不具有对称性 (注意，所有散度中只有 JS 散度是对称的)，即：

$$
D_{KL}(P||Q)\not =D_{KL}(Q||P)
$$

* KL 散度非负性
