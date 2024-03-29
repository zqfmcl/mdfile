---
title: Search Insert Position[M]
date: 2019-10-04 10:00:00
tags: Leetcode
---

# 问题

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.



Here are few examples.

> [1,3,5,6], 5 → 2
>
> [1,3,5,6], 2 → 1
>
> [1,3,5,6], 7 → 4
>
> [1,3,5,6], 0 → 0



# 思路

这个问题的思路很简单，就是二分查找，而且直接套用框架就行了



# 代码

```java
public class Solution {
    public int searchInsert(int[] nums, int target) {
        int st,ed,mid;
        st = 0;
        ed = nums.length;
        while(st < ed)
        {
            mid = st + (ed - st)/2;
            if(nums[mid] < target)
                st = mid+1;
            else
                ed = mid;
        }
        return st;
    }
}
```

