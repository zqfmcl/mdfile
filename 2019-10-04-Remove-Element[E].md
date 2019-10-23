---
title: Remove Element[E]
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Remove Element[E]

------

# 问题

Given an array and a value, remove all instances of that value in place and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

> Example:
> Given input array nums = [3,2,2,3], val = 3

Your function should return length = 2, with the first two elements of nums being 2.

# 思路

和之前的那道题很像，凡是涉及in place交换的都可以考虑用两指针，一次扫描完成。
由于这里说了可以交换元素的位置，那么就方便了，我们可以用后面的元素来替换前面的元素，这样就不用交换整个数组。

两个指针front和tail，分别从前后向中间扫描，当两个指针相遇则结束。

- 如果fron < tail：
  - 移动front，如果遇到了A[front] `==` val的，暂停
  - 移动tail，如果遇到了A[tail]`!=`val的，把值复制给A[front]

```java
public class Solution {
    public int removeElement(int[] nums, int val) {
        int front = 0,tail = nums.length-1;
        while(front <= tail)
        {
            if(nums[front] == val && nums[tail] != val)
            {
                nums[front] = nums[tail];
                nums[tail] = val;
            }
            if(nums[front] != val) front++;
            if(nums[tail] == val) tail--;
        }
        return tail+1;
    }
}
```

可以参考`daxianji007 `更加巧妙的代码：这里用一个变量存储不一样的个数，由于题目里只用前index个与val不一样就行，后面的不用考虑，所以每次遇到一个不一样的值，就把它插到前面就好了。

```
int removeElement(int A[], int n, int elem) 
{
    int begin=0;
    for(int i=0;i<n;i++) 
	    if(A[i]!=elem) 
		    A[begin++]=A[i];
    return begin;
}

```

