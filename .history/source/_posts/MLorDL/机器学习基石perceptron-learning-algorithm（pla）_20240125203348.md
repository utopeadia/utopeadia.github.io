---
title: (机器学习基石)Perceptron Learning Algorithm（PLA）
tags: []
id: '119'
categories:
  - - MLorDL
comments: true
date: 2020-02-27 22:12:45
katex: true
---
### **一、Perceptron Hypothesis Set**
例子：
银行要决定是否给使用者发信用卡。
可以将每一个使用者的各种信息作为一个向量，每一个维度使用$x_i$来表示，给每个不同特征给予不同的权重，将加权值的和作为输出，设置一个阈值，如果超过阈值，那么就输出1，如果小于阈值，就输出-1.
![这里写图片描述](https://img.wush.cc/16311025992905.png?imageView2/0/format/webp/q/80)
我们输入的x是向量，那么我们使用$w_i$向量。并且将threshold也作为$w_i$来简化运算过程
![这里写图片描述](https://img.wush.cc/16311025992918.png?imageView2/0/format/webp/q/80)
我们绘制一个二维图像来描述。圈代表1，叉代表-1，表示y的值。x只有两个维度的情况可以简单地画出来。这时的h(x)用一条直线将平面分成了两个部分，一部分为h(x)=1，另一部分为h(x)=−1。每个h都对应了一种分割方式。
![这里写图片描述](https://img.wush.cc/16311025992931.png?imageView2/0/format/webp/q/80)
那么，我们所说的Perceptron，实际上上就是一条直线，我们称之为linear(binary) classifiers（线性分类器）。在更高维度中，同样支持。
同时，需要注意的是，这里所说的linear(binary) classifiers是用简单的感知器模型建立的，线性分类问题还可以使用logistic regression来解决，后面将会介绍。
### **二、Perceptron Learning Algorithm(PLA)**
根据上一部分的介绍，我们已经知道了hypothesis set由许多条直线构成。我们希望将所有的正类和负类完全分开，也就是找到最好的g，使$g\approx f$。
但是这样是很困难的，因为我们的f是未知的，我一我们可以将问题转化为找到最好的f。
我们有无限多条线，但是我们可以选择一条线，然后逐步修正，逼近最好答案。
![截屏2020-02-27下午7.33.11](https://img.wush.cc/16311025992946.png?imageView2/0/format/webp/q/80)
我们使用$w_i(i=0)$作为初始的线
循环下面操作：
* 找出$w_t$线下某一错误点称为$（X_{n(t)},Y_{n(t)}）$(下标t表示在哪一轮)
* 用错误的线做内积运算
  > 计算w与x内积，即w_x_cos<w,x>，作用在sign()函数上只有cos起作用，即夹角。
* 进行修正
![这里写图片描述](https://img.wush.cc/16311025992961.png?imageView2/0/format/webp/q/80)
下面介绍一下PLA是怎么做的。首先随机选择一条直线进行分类。然后找到第一个分类错误的点，如果这个点表示正类，被误分为负类，即$w_t^Tx_{n(t)}<0$，那表示w和x夹角大于90度，其中w是直线的法向量。所以，x被误分在直线的下侧（相对于法向量，法向量的方向即为正类所在的一侧），修正的方法就是使w和x夹角小于90度。通常做法是$ w\leftarrow w+yx,\ y=1 $，如图右上角所示，一次或多次更新后的$w+yx$与x夹角小于90度，能保证x位于直线的上侧，则对误分为负类的错误点完成了直线修正。
如果是误分为正类的点，即$ w_t^Tx_{n(t)}>0 $，那表示w和x夹角小于90度，其中w是直线的法向量。所以，x被误分在直线的上侧，修正的方法就是使w和x夹角大于90度。通常做法是$ w\leftarrow w+yx,\ y=-1 $，如图右下角所示，一次或多次更新后的$ w+yx$与x夹角大于90度，能保证x位于直线的下侧，则对误分为正类的错误点也完成了直线修正。
遇到个错误点就进行修正，不断迭代。要注意一点：每次修正直线，可能使之前分类正确的点变成错误点，但是只要不断进行迭代，对于线性分类模型，最后总会找到的一个合适的直线能够刚好分开。
实际操作中，可以一个点一个点地遍历，发现分类错误的点就进行修正，直到所有点全部分类正确。这种被称为Cyclic PLA。
![这里写图片描述](https://img.wush.cc/16311025992976.png?imageView2/0/format/webp/q/80)
下面用图解的形式来介绍PLA的修正过程：
红线代表$w^T$表示分割线$w$的法线，正方向为法方向。
![这里写图片描述](https://img.wush.cc/16311025992991.png?imageView2/0/format/webp/q/80)
![这里写图片描述](https://img.wush.cc/16311025993009.png?imageView2/0/format/webp/q/80)
![这里写图片描述](https://img.wush.cc/16311025993026.png?imageView2/0/format/webp/q/80)
![这里写图片描述](https://img.wush.cc/16311025993045.png?imageView2/0/format/webp/q/80)
![这里写图片描述](https://img.wush.cc/16311025993064.png?imageView2/0/format/webp/q/80)
![这里写图片描述](https://img.wush.cc/16311025993084.png?imageView2/0/format/webp/q/80)
![这里写图片描述](https://img.wush.cc/16311025993105.png?imageView2/0/format/webp/q/80)
![这里写图片描述](https://img.wush.cc/16311025993125.png?imageView2/0/format/webp/q/80)
![这里写图片描述](https://img.wush.cc/16311025993146.png?imageView2/0/format/webp/q/80)
![这里写图片描述](https://img.wush.cc/16311025993166.png?imageView2/0/format/webp/q/80)
![这里写图片描述](https://img.wush.cc/16311025993185.png?imageView2/0/format/webp/q/80)
问题：
* 这种方法一定会停下来吗？
* 假设停下来了,$g$是否等于$f$？
### **三、Guarantee of PLA**
PLA什么时候会停下来？根据PLA的终止条件是，找到一条直线，能将所有平面上的点都分类正确，那么PLA就停止了。要达到这个终止条件，就必须保证D是线性可分（linear separable）。如果是非线性可分的，那么，PLA就不会停止。
![这里写图片描述](https://img.wush.cc/16311025993205.png?imageView2/0/format/webp/q/80)
对于线性可分的情况，如果有这样一条直线，能够将正类和负类完全分开，令这时候的目标权重为$w_f$，则对每个点，必然满足$y_n=sign(w_f^Tx_n)$，即对任一点：
![这里写图片描述](https://img.wush.cc/16311025993225.png?imageView2/0/format/webp/q/80)
PLA会对每次错误的点进行修正，更新权重$w_{t+1}$的值，如果$w_{t+1}$与$w_f$越来越接近，数学运算上就是内积越大，那表示$w_{t+1}$是在接近目标权重$w_f$，证明PLA是有学习效果的。所以，我们来计算$w_{t+1}$与$w_f$的内积：
![这里写图片描述](https://img.wush.cc/16311025993246.png?imageView2/0/format/webp/q/80)
从推导可以看出，$w_{t+1}$与$w_f$的内积跟$w_t$与$w_f$的内积相比更大了。似乎说明了$w_{t+1}$更接近$w_f$，但是内积更大，可能是向量长度更大了，不一定是向量间角度更小。所以，下一步，我们还需要证明$w_{t+1}$与$w_t$向量长度的关系：
![这里写图片描述](https://img.wush.cc/16311025993270.png?imageView2/0/format/webp/q/80)
$w_t$只会在分类错误的情况下更新，最终得到的$w_{t+1}^2$相比$w_{t}^2$的增量值不超过$maxx_n^2$。也就是说，$w_t$的增长被限制了，$w_{t+1}$与$w_t$向量长度不会差别太大！
如果令初始权值$w_0=0$，那么经过T次错误修正后，有如下结论：
$$\frac{w_f^T}{w_f}\frac{w_T}{w_T}\geq \sqrt T\cdot constant$$
下面贴出来该结论的具体推导过程：
![这里写图片描述](https://img.wush.cc/16311025993291.png?imageView2/0/format/webp/q/80)
![这里写图片描述](https://img.wush.cc/16311025993312.png?imageView2/0/format/webp/q/80)
上述不等式左边其实是$w_T$与$w_f$夹角的余弦值，随着T增大，该余弦值越来越接近1，即$w_T$与$w_f$越来越接近。同时，需要注意的是，$\sqrt T\cdot constant\leq 1$，也就是说，迭代次数T是有上界的。根据以上证明，我们最终得到的结论是：$w_{t+1}$与$w_f$的是随着迭代次数增加，逐渐接近的。而且，PLA最终会停下来（因为T有上界），实现对线性可分的数据集完全分类。
### **四、Non-Separable Data**
上一部分，我们证明了线性可分的情况下，PLA是可以停下来并正确分类的，但对于非线性可分的情况，$w_f$实际上并不存在，那么之前的推导并不成立，PLA不一定会停下来。所以，PLA虽然实现简单，但也有缺点：
![这里写图片描述](https://img.wush.cc/16311025993334.png?imageView2/0/format/webp/q/80)
对于非线性可分的情况，我们可以把它当成是数据集D中掺杂了一下noise，事实上，大多数情况下我们遇到的D，都或多或少地掺杂了noise。这时，机器学习流程是这样的：
![这里写图片描述](https://img.wush.cc/16311025993357.png?imageView2/0/format/webp/q/80)
在非线性情况下，我们可以把条件放松，即不苛求每个点都分类正确，而是容忍有错误点，取错误点的个数最少时的权重w：
![这里写图片描述](https://img.wush.cc/16311025993382.png?imageView2/0/format/webp/q/80)
事实证明，上面的解是NP-hard问题，难以求解。然而，我们可以对在线性可分类型中表现很好的PLA做个修改，把它应用到非线性可分类型中，获得近似最好的g。
修改后的PLA称为Packet Algorithm。它的算法流程与PLA基本类似，首先初始化权重$w_0$，计算出在这条初始化的直线中，分类错误点的个数。然后对错误点进行修正，更新w，得到一条新的直线，在计算其对应的分类错误的点的个数，并与之前错误点个数比较，取个数较小的直线作为我们当前选择的分类直线。之后，再经过n次迭代，不断比较当前分类错误点个数与之前最少的错误点个数比较，选择最小的值保存。直到迭代次数完成后，选取个数最少的直线对应的w，即为我们最终想要得到的权重值。
![这里写图片描述](https://img.wush.cc/16311025993407.png?imageView2/0/format/webp/q/80)
如何判断数据集D是不是线性可分？对于二维数据来说，通常还是通过肉眼观察来判断的。一般情况下，Pocket Algorithm要比PLA速度慢一些。
### **五、总结**
本节课主要介绍了线性感知机模型，以及解决这类感知机分类问题的简单算法：PLA。我们详细证明了对于线性可分问题，PLA可以停下来并实现完全正确分类。对于不是线性可分的问题，可以使用PLA的修正算法Pocket Algorithm来解决。
**_注明：_**
笔记改编自红色石头博客
文章中所有的图片均来自台湾大学林轩田《机器学习基石》课程。
