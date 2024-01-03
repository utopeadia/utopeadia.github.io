---
title: np.argmax函数详解
tags: []
id: '512'
categories:
  - - Python
date: 2021-12-04 23:14:23
---

## 简介

numpy.argmax(array,axis=None,out=None)返回一个numpy数组最大值的索引。它包含三个参数，out参数通常不使用，array表示传入数组，axis表示维度。 **返回值是找到的第一个最大值的索引。例如：\[1,2,2,1\]的返回索引为1而不是2或者1,2**

## axis=0

以第0维度方向进行查找（找出每一列最大值的行索引）。 代码：

```python
import numpy as np
a = np.array([[1,2,2,1],
              [1,2,3,1]])
print(np.argmax(a,axis=0))
```

结果： \[0 0 1 0\]

![2021-12-04-20211204231103](https://img.wush.cc/2021-12-04-20211204231103.png?imageView2/0/format/webp/q/80)

## axis=1

以第1维度方向进行查找（找出每一行最大值的列索引）。 代码：

```python
import numpy as np
a = np.array([[1,2,2,1],
              [1,2,3,1]])
print(np.argmax(a,axis=1))
```

结果： \[1 2\]

![2021-12-04-2](https://img.wush.cc/2021-12-04-2.png?imageView2/0/format/webp/q/80)

## Other

同上。