---
title: Palindrome Number[E]
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Palindrome Number[E]

------

# 问题：

Determine whether an integer is a palindrome. Do this without extra space.

# 思路

这里说不用额外的空间意思是不用O(n)的空间，O(1)的还是可以用的，不然循环都不好写。。

## 思路1

简单的思路 就是把数字逆转，然后判断逆转后的数字跟原来数字是不是一样的。

```c++
class Solution {
public:
    bool isPalindrome(int x) {
        if(x < 0)   return false;
        int r=0,t;
        t = x;
        while(t != 0)
        {
            r =r*10 + t%10;
            t /=10;
        }
        return r == x;
        
    }
};
```

## 思路2

但是其实，不用把数字逆转完再判断，因为如果是回文数字，那么只要逆转一半看是否满足回文条件就行了。

设新数为r，原来数为x，每次：

```
x = x/10，r = r*10 + x%10;
```

- 如何到一半停止？
  - 如果x <= r时可以停止了（至少到了一半）
  - 如果是偶数长度，并且是回文，那么刚好可以到x == r
  - 如果为奇数长度，并且是回文，那么x < r，这时候r刚好比x多一位数
- 停止后判断是否是回文
  - 如果是偶数长度，很简单判断 r == x
  - 如果是奇数长度，要判断 r/10 == x

<font color=red>注意：这里有一些小问题。</font>

- 当尾数为0的情况。尾数为0会导致r的增长少1位数（因为0*10 = 0）。
  比如110不是回文，最后停止r = 1  x =1 但是 r == x

- 当数字小于0的时候，也是不满足回文的条件的。

```c++
class Solution {
public:
    bool isPalindrome(int x) {
        if(x < 0 || (x != 0 && x %10 ==0))   return false;
        int r = 0;
        while(x > r)
        {
            r =r*10 + x%10;
            x /=10;
        }
        return (r == x) || (r/10 == x);
        
    }
};
```

