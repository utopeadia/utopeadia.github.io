---
title: (Py练习)日期格式转换
tags: []
id: '131'
categories:
  - - Python
comments: true
date: 2020-02-14 22:17:36
---

```python
#将日期转换为易读的格式
#使用dateuti包
from dateutil import parser
dt = parser.parse("Mar 6 2019 12:00AM")
print(dt)
```

![-w147](https://img.wush.cc/16311032111355.png)