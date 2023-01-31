---
title: NumPy中文文档搬砖学习笔记（1）
tags: []
id: '134'
categories:
  - - Python
comments: true
date: 2020-02-18 22:18:01
---

[原文地址](https://www.numpy.org.cn/article/advanced/numpy_array_programming.html)

## 前言

​ 况下加速Python中的操作运行时。适用于快速数值运算的一个选项是NumPy，它当之无愧地将自己称为使用Python进行科学计算的基本软件包。

​ 当然，很少有人将50微秒（百万分之五十秒）的东西归类为“慢”。然而，计算机可能会有所不同。运行50微秒（50微秒）的运行时属于微执行领域，可以松散地定义为运行时间在1微秒和1毫秒之间的运算。

​ 为什么速度很重要？微观性能值得监控的原因是运行时的小差异会随着重复的函数调用而放大：增量50μs的开销，重复超过100万次函数调用，转换为50秒的增量运行时间。

​ 在计算方面，实际上有三个概念为NumPy提供了强大的功能：

*   矢量化
*   广播
*   索引

## 进入状态：介绍NumPy数组

​ NumPy的基本对象是它的ndarray（或numpy.array），这是一个n维数组，它以某种形式出现在面相组织的语言中，如Fortran 90、R和MATLAB，以及以前的APL和J。 首先从一个包含36个元素的三维数组开始：

```python
import numpy as np
arr = np.arange(36).reshape(3, 4, 3)
print(arr)
```

![-w105](https://img.how1e.com/16311032484388.png)

​ 在二维中描述高维数组可能会比较困难。考虑到数组形状的一种直观方法是简单的“从左到右读取它”。arr就是一个 $3\times4\times3$的数组：

```python
import numpy as np
arr = np.arange(36).reshape(3, 4, 3)
print(arr.shape)
```

![-w70](https://img.how1e.com/16311032484400.png)

​ 在视觉上，arr可以被认为是三个$4 \times3 $ 网格（或矩形棱镜）的容器，看起来像是： ![-w399](https://img.how1e.com/16311032484410.png)

​ 更高纬度的数组可能更难以用图像表达出来，但是他们仍然遵循这种“数组内的数组”模式。

## 什么是矢量化？

​ 矢量化是NumPy中的一种强大功能，可以将操作表达为在整个数组上而不是在各个元素上发生。以下是Wes McKinney的简明定义：

> 这种用数组表达式替换显式循环的做法通常称为向量化。通常，矢量化数组操作通常比其纯Python等价物快一个或两个（或更多）数量级，在任何类型的数值计算中都具有最大的影响。 [察看源码](https://www.oreilly.com/library/view/python-for-data/9781449323592/ch04.html)

​ 在Python中循环数组或任何数据结构时，会涉及很多开销。 NumPy中的向量化操作将内部循环委托给高度优化的C和Fortran函数，从而实现更清晰，更快速的Python代码。

### 计数：简单的如：1，2，3...

​ 作为示例，考虑一个True和False的一维向量，你要为其计算序列中“False to True”转换的数量：

```python
np.random.seed(444)
x = np.random.choice([False, True], size=100000)
print(x)
```

![-w290](https://img.how1e.com/16311032484424.png)

​ 使用python for循环，一种方法使成对的评估每个元素的[真值](https://docs.python.org/3/library/stdtypes.html#truth-value-testing)以及紧随其后的元素：

```python
import numpy as np

arr = np.arange(36).reshape(3, 4, 3)

np.random.seed(444)
x = np.random.choice([False, True], size=100000)
print(x)

def cout_transitions(x) -> int:
    count = 0;
    for i, j in zip(x[:-1], x[1:]):
        if j and not i:
            count += 1
    return count
print(cout_transitions(x))
```

![-w298](https://img.how1e.com/16311032484438.png)

在矢量化形式中，没有明确的for循环或直接引用各个元素：

```python
np.count_nonzero(x[:-1] < x[1:])
```

​ 在这种特殊情况下，向量化的NumPy调用胜出约70倍 **技术细节：**另一个术语是[矢量处理器](https://docs.microsoft.com/en-us/archive/blogs/nativeconcurrency/what-is-vectorization)，它与计算机的硬件有关。 当我在这里谈论矢量化时，我指的是用数组表达式替换显式for循环的概念，在这种情况下，可以使用低级语言在内部计算。

### 买低，卖高

​ 这是另一个激发你胃口的例子。考虑以下经典技术面试问题：

> 假定一只股票的历史价格是一个序列，假设你只允许进行一次购买和一次出售，那么可以获得的最大利润是多少？例如，假设价格=(20，18，14，17，20，21，15)，最大利润将是7，从14买到21卖。

​ (对所有金融界人士说：不，卖空是不允许的。) ​ 存在具有n平方时间复杂度的解决方案，其包括采用两个价格的每个组合，其中第二价格“在第一个之后”并且确定最大差异。 然而，还有一个O(n)解决方案，它包括迭代序列一次，找出每个价格和运行最小值之间的差异。 它是这样的：

```python
 def profit(prices):
     max_px = 0
     min_px = prices[0]
     for px in prices[1:]:
         min_px = min(min_px, px)
         max_px = max(px - min_px, max_px)
     return max_px
prices = (20, 18, 14, 17, 20, 21, 15)
print(profit(prices))
```

​ 结果为7 ​ 这可以用NumPy实现吗？行!没问题。但首先，让我们构建一个准现实的例子：

```python
# Create mostly NaN array with a few 'turning points' (local min/max).
 prices = np.full(100, fill_value=np.nan)
 prices[[0, 25, 60, -1]] = [80., 30., 75., 50.]

# Linearly interpolate the missing values and add some noise.
 x = np.arange(len(prices))
 is_valid = ~np.isnan(prices)
 prices = np.interp(x=x, xp=x[is_valid], fp=prices[is_valid])
 prices += np.random.randn(len(prices)) * 2
```

下面是[matplotlib](https://realpython.com/python-matplotlib-guide/)的示例。俗话说：买低(绿)，卖高(红)：

```python
 import matplotlib.pyplot as plt

# Warning! This isn't a fully correct solution, but it works for now.
# If the absolute min came after the absolute max, you'd have trouble.
 mn = np.argmin(prices)
 mx = mn + np.argmax(prices[mn:])
 kwargs = {'markersize': 12, 'linestyle': ''}

 fig, ax = plt.subplots()
 ax.plot(prices)
 ax.set_title('Price History')
 ax.set_xlabel('Time')
 ax.set_ylabel('Price')
 ax.plot(mn, prices[mn], color='green', **kwargs)
 ax.plot(mx, prices[mx], color='red', **kwargs)
```

![-w674](https://img.how1e.com/16311032484453.png) NumPy实现是什么样的？ 虽然没有np.cummin() “直接”，但NumPy的通用函数（ufuncs）都有一个accumulate()方法，它的名字暗示了：

```python
cummin = np.minimum.accumulate
```

​ 从纯Python示例扩展逻辑，你可以找到每个价格和运行最小值（元素方面）之间的差异，然后获取此序列的最大值：

```python
 def profit_with_numpy(prices):     """Price minus cumulative minimum price, element-wise."""     prices = np.asarray(prices)     return np.max(prices - cummin(prices)) print(profit_with_numpy(prices))print(np.allclose(profit_with_numpy(prices), profit(prices)))
```

结果为： 44.2487532293278 True 这两个具有相同理论时间复杂度的操作如何在实际运行时进行比较？ 首先，让我们采取更长的序列。（此时不一定需要是股票价格的时间序列）

```python
seq = np.random.randint(0, 100, size=100000)
```

​ 现在，对于一个有点不公平的比较：

```python
setup = ('from __main__ import profit_with_numpy, profit, seq;'          ' import numpy as np') num = 250 pytime = timeit('profit(seq)', setup=setup, number=num) nptime = timeit('profit_with_numpy(seq)', setup=setup, number=num) print('Speed difference: {:0.1f}x'.format(pytime / nptime))
```

结果为：Speed difference: 76.0x 在上面，将profit_with_numpy() 视为伪代码（不考虑NumPy的底层机制），实际上有三个遍历序列：

*   cummin(prices) 具有O(n)时间复杂度
    
*   prices - cummin(prices) 是 O(n)的时间复杂度
    
*   max(...) 是O(n)的时间复杂度 这就减少到O(n)，因为O(3n)只剩下O(n)-当n接近无穷大时，n “占主导地位”。
    

因此，这两个函数具有等价的最坏情况时间复杂度。(不过，顺便提一下，NumPy函数的空间复杂度要高得多。)。但这可能是最不重要的内容。这里我们有一个教训是：虽然理论上的时间复杂性是一个重要的考虑因素，运行时机制也可以发挥很大的作用。NumPy不仅可以委托给C，而且通过一些元素操作和线性代数，它还可以利用多线程中的计算。但是这里有很多因素在起作用，包括所使用的底层库(BLAS/LAPACK/Atlas)，而这些细节完全是另一篇文章的全部内容。