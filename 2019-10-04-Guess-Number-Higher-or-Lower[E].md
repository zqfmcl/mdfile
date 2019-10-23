---
title: Guess Number Higher or Lower[E]
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Guess Number Higher or Lower[E]

# 问题：

We are playing the Guess Game. The game is as follows:
I pick a number from 1 to n. You have to guess which number I picked.
Every time you guess wrong, I'll tell you whether the number is higher or lower.
You call a pre-defined API guess(int num) which returns 3 possible results (-1, 1, or 0):
-1 : My number is lower
1 : My number is higher
0 : Congrats! You got it!

Example:
n = 10, I pick 6.
Return 6.

# 思路

注意，这里有几个陷阱，一是你要理解`my`的含义，它的`my`是指的`出题人`，而我们是解题人，所以如果返回-1，说明它的数小，我们猜的数大，这里一定要理解！

这是一个经典的二分题目，很容易套用二分查找的公式写出来：

```java
public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int st = 1, ed = n;
        while(st < ed)
        {
            int mid = (st + ed) / 2;
            if(guess(mid) == 0)
                return mid;
            else if(guess(mid) < 0)  // the number is too large
                ed = mid-1;
            else
                st = mid+1;
        }
        return st;
    }
}

```

看上去没问题，但是实际上有潜在的危险，比如这个例子就A不过去：

![your text](http://o7bk1ffzo.bkt.clouddn.com/1474187361233)

为什么，因为`int mid = (st + ed) / 2;`可能会由于（st+ed）产生溢出！！

所以，为了解决这个问题，推荐把mid的写法写成下面的格式：

```
int mid = st + (ed - st) / 2;
```

然后再A就能通过