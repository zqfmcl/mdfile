---
title: Container With Most Water  
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Container With Most Water  

------

# 问题

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container. 

# 思路

首先要明确一个我之前一直理解错的，它的题目是<font color=red>随意找2个木板构成木桶，容量最大，</font>我之前以为是所有的木板已经在它的位置上了，然后找其中容量最大的——你加的水是可以漫过中间比较短的板子的。

如果按题意来，就简单了。

我们用两个指针来限定一个水桶，left,right。
h[i]表示i木板高度。
Vol_max表示木桶容量最大值

> 由于桶的容量由最短的那个木板决定：
> Vol = min(h[left],h[right]) * (right - left)

- left和right分别指向两端的木板。
- left和right都向中央移动，每次移动left和Right中间高度较小的（因为反正都是移动一次，宽度肯定缩小1，这时候只能指望高度增加来增加容量，肯定是替换掉高度较小的，才有可能找到更大的容量。）
- 看新桶子的容量是不是大于Vol_max，直到left和right相交。

代码如下：

```java
public class Solution {
    public int maxArea(int[] height) {
       int l = 0,r = height.length-1;
       int i = height[l] > height[r] ? r:l;
       int vol,vol_max = height[i]*(r-l);
       while(l < r)
       {
           if(height[l] < height[r])  l++;
           else r--;
           vol = Math.min(height[l],height[r]) * (r - l);
           if(vol > vol_max)     vol_max = vol;
       }
       return vol_max;
    }
}

```

