---
title: Maximum Subarray[M]
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Maximum Subarray[M]

------

## 题目

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array` [-2,1,-3,4,-1,2,1,-5,4]`,
the contiguous subarray `[4,-1,2,1]` has the largest sum = 6.

即求一个整数数组中的和最大的连续子数组问题

## 思路

首先，这个问题可以用枚举来求，比较容易想到 i (0 ... n-1), j (0 .. n-1)，然后每次求和的时候，用个巧办法，不用再次循环：

- j 移动的时候把当前j所在的值加到和上
- i 移动的时候把i之前的值减去。
  时间复杂度O(N^2)

```java
public class Solution {
    public int maxSubArray(int[] nums) {
        int sum ,maxsum;
        maxsum = nums[0];
        for(int i = 0;i < nums.length;i++)
        {
            sum = 0;
            for(int j = i;j < nums.length;j++)
            {
                sum += nums[j];
                maxsum = sum>maxsum?sum:maxsum;
            }
        }
        return maxsum;
    }
}
```

## D&C

之前的枚举的算法可以，但是时间复杂度太高会超时，于是继续优化。有人提出了D&C算法
把数组分成差不多相等的两部分，最长数组要不在左边，要不在右边，要不在中间。
分好分，就是2分，关键是怎么合。
合的话就是左边的最大值和右边的最大值比较，然后再跟合起来后中间的最大值比较。
中间的最大值求法O(n)：

- 左边的最大值不断+右边的值
- 右边最大值不断+左边的值



