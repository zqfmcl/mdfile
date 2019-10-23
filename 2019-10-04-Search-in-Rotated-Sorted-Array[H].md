---
title: Search in Rotated Sorted Array[H]
date: 2019-10-04 10:00:00
tags: Leetcode
---

# 问题

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.



# 思路

这个问题是二分查找的变种，它这里唯一的一个小trick就是把本来有序的数组做了一个旋转。但是注意，旋转的2部分是分别有序的。



还有一个很重要的特点：**后半部分小于前半部分**，所以其实很容易判断出**mid在哪一部分**。

（如果num[mid] > num[0]，我们就知道mid在左部分，否则在右部分。）



这里不能直接用二分的问题在于：**如果target和mid不在同一部，就会出错。**



> 举例nums: [4,5,6,1,2,3,4]，st = 0 ， ed = 6，mid = 3, target = 6

此时：mid指向1，而target是6，说明mid和target不在同一部，会出现什么问题呢？

按照算法：

```java
if (nums[mid] < target)
  st = mid+1
```

这里，**明明应该往左搜索，但是却往右边搜索了**。 所以，为了解决这个问题。我们可以引入`inf`和`-inf`

## 引入inf和-inf

为了更加方便理解，我们举例：

我们随便看一个数组num:[4,5,6,1,2,3,4]

- 假设我们查询的目标是3：那我们实际查询的是`右一段`：[4,5,6,**1,2,3,4**]，实际上我们可以把前面的数都看作`-inf`：[-inf,-inf,-inf,**1,2,3,4**]
- 假设我们查询的目标是5：那我们实际查询的是`左一段`：[**4,5,6,7,**1,2,3,4]，实际上我们可以把后面的数都看作`inf`：[**4,5,6**,inf,inf,inf,inf]

**这样其实就和普通的二分一样了。**



### 如何知道在哪一段？

1. 如果`target < nums[0]`和`nums[mid]<nums[0]`同时成立，那么我们按照普通的二分查找操作就行。
2. 如果`target < nums[0]`和`nums[mid]<nums[0]`不同时成立，那么**说明target和mid在不同部分**。我们需要根据target的情况引入`inf`和` -inf`
   - 如果`target < nums[0]`，说明在右部，我们引入`-inf`，让st移动
   - 否则，说明在左部，我们引入`inf`，让ed移动



# 代码

```java
public class Solution {
    public int search(int[] nums, int target) {
        int st,ed,mid;
        st = 0;
        ed = nums.length-1;
        while(st < ed)
        {
            mid = st + (ed - st)/2;
            //增加部分
            int tmp = (nums[mid] < nums[0]) == (target < nums[0])
                   ? nums[mid]   //如果在同一部，则用原值
                   : target < nums[0] ? Integer.MIN_VALUE : Integer.MAX_VALUE; //否则根据情况引入-inf或inf
            
            if(tmp < target)
                st = mid+1;
            else if(tmp > target)
                ed = mid;
            else
                return mid;
        }
        return nums[st] == target?st:-1;
    }
}
```