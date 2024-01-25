---
title: (Py练习)输入某年某月判断天数
tags: []
id: '144'
categories:
  - - Python
comments: true
date: 2020-02-13 22:19:32
---

```python
# 输入某年某月，判断这一天是这一年的第几天
year = int(input("year:\n"))
month = int(input("month:\n"))
day = int(input("day:\n"))

months = (0, 31, 59, 90, 120, 151, 181, 212, 243, 273, 304, 334)
if 0 < month <= 12:
    sum = months[month - 1]
else:
    print('Date Error\n')
sum += day
leap = 0
# 判断是否为闰年
# 判断标准是：1、能被4整除且不能整除100；2、能整除400
# and 优先级高于 or
if (year % 400 == 0) or (year % 4 == 0) and (year % 100 != 0):
    leap = 1
if (leap == 1) and (month > 2):
    sum += 1
print(f'it is rhe the %dth day.' % sum)
```