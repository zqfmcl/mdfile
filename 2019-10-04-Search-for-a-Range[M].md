---
title:  Search for a Range[M]
date: 2019-10-04 10:00:00
tags: Leetcode
---

 Search for a Range[M]

# 问题

Given a sorted array of integers, find the starting and ending position of a given target value.
Your algorithm's runtime complexity must be in the order of O(log n).
If the target is not found in the array, return [-1, -1].

> For example,
> Given [5, 7, 7, 8, 8, 10] and target value 8,
> return [3, 4].

# 思路

题目里给了提示要求时间上必须是O(logN)，那么暗示了这要用二分去做。
范围搜索也就是要确定一个上确界，一个下确界。

分别都可以用二分去找。

## 左边界

二分的话主要有以下几种情况，我们定义成3个基本规则：

> Rule 1. A[mid] < target  ，这时候说明还可以向右，st = mid+1
> Rule 2. A[mid] > target ， 这时候说明应该在左边，ed = mid-1
> Rule 3. A[mid] == target ，这时候既可以左移，也可以不移动，ed = mid

因为作为二分，最后肯定是在2个数中选一个然后停止循环（while(st < ed)）。
考虑下面几种情况，假设 target=5：（在两个数的情况下mid = st）

```
case 1: [3 5] (A[st] = target > A[ed])
case 2: [5 7] (A[st] = target < A[ed])
case 3: [5 5] (A[st] = target = A[ed])
case 4: [3 7] (A[st] < target < A[ed])
case 5: [3 4] (A[st] < A[ed] < target)
case 6: [6 7] (target < A[st] < A[ed])
```

情况3就是Rule1的情况，`st = mid + 1`就行。
对于情况2-3这时候，我们只要 `ed = mid`就行了，其实也就是把Rule 2 和Rule 3合并成了

> Rule 2*. A[mid] >= target， ed = mid

所以case 1-3 最后停止条件都是A[st] = A[ed] = target

对于case 4-6 都是A[st] != target，可以直接退出

## 右边界

找到了左边的边界后就好办了，右边的边界只用同理操作就行了。
而且因为找到了左边的边界，实际上就不存在比target小的数了。

这里，我们让mid偏向右边

```
mid = (st + ed)/2 + 1; 
```

然后主要控制ed移动就可以了。

# 代码

```java
public class Solution {
    public int[] searchRange(int[] nums, int target) {
        int [] result = new int [2];
        result[0] = result[1] = -1;
        if(nums.length == 0)
            return result;

        int st = 0, ed = nums.length-1,mid;
        while(st < ed) {
            // 寻找左边界
            mid = (st + ed) / 2;
            if (nums[mid] < target)  //保证st不会越过任何等于target的数
            {
                st = mid+1;  //如果当前的数小于我们需要查的数，继续逼近
            } else {       //如果大于等于
                ed = mid;
            }
        }
        if(nums[st] != target)
            return result;
        result[0] = st;
        // 寻找右边界
        ed = nums.length-1;
        while(st < ed)
        {
            mid = (st + ed)/2 + 1; //这里用+1是为了让mid偏向右边
            if(nums[mid] > target)
            {
                ed = mid-1;
            }
            else{   //因为st已经确定了，所以这里实际上不会出现比target小的数了，这里实际就是A[mid] == target
                st = mid;
            }
        }
        result[1] = ed;
        return result;
    }
}
```