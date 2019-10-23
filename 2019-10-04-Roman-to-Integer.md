---
title: Roman to Integer
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Roman to Integer

------

# 问题

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

Subscribe to see which companies asked this question

# 思路

首先要知道罗马数字的规律：

| Symbol | Value |
| ------ | ----- |
| I      | 1     |

|V |	5
|X 	|10
|L 	|50
|C |	100
|D| 	500
|M| 	1,000

然后还有一个规则是，罗马数字从左自右相加，但是如果小数字A在大数字B之前，表示B-A

VI = 5+1 = 6
IV = 5-1 = 4

因此，利用2个变量保存当前数字和之前的数字就行了。因为这题很简单，用python比较方便，我就用python做的

```python
class Solution(object):
    def romanToInt(self, s):
        sum=0
        pre = 2000
        cur = 0
        Map = {'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}
        for i in range(len(s)):
            cur = Map[s[i]]
            sum = sum+Map[s[i]]
            if cur > pre :
                sum = sum-2*pre
            pre = cur
        return sum
```

