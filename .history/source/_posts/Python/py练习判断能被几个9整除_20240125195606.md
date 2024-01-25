---
title: (Py练习)判断能被几个9整除
tags: []
id: '140'
categories:
  - - Python
comments: true
date: 2020-02-14 22:18:58
---

```python
# 输入一个奇数，判断最少几个9除以该数的结果为整数
# 999999 / 13 = 76923
if __name__ == '__main__':
    zi = int(input("输入一个奇数：\n"))
    n1 = 1
    c9 = 1
    m9 = 9
    sum = 9
    while n1 != 0:
        if sum % zi == 0:
            n1 = 0
        else:
            m9 *= 10
            sum += m9
            c9 += 1
    print("%d个9可以被%d整除：%d" % (c9, zi, sum))
    r = sum / zi
    print('%d / %d = %d' % (sum, zi, r))
```

![-w166](https://img.wush.cc/16311032270782.png?imageView2/0/format/webp/q/80)