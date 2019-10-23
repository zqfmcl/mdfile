---
title: Counting Bits [M]
date: 2019-10-04 10:00:00
tags: Leetcode
---

## 338. Counting Bits [M]

------

# 题目

Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

> Example:
> For num = 5 you should return [0,1,1,2,1,2].

Follow up:

1. It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass
2. Space complexity should be O(n).
3. Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.

# 思路

这是一个比较简单的动规题目，就是统计二进制数的1个个数，通过观察可以发现二进制数有很多规律在里面

|十进制|二进制|
|-:-|-:-|
|1 |  1
|2  | 10
|3  | 11
|4  | 100
|8  |     1000
|9 |      10001

可以看见，当二进制位数多1位的时候，高位为1，剩下的和之前的是一样的。

> list[i] = list[i%n]+1  //n = floor(log(i))

> list[2] = list[2%2]+1
>
> list[5] = list[5%4]+1
>
> list[12] =list[12%8]+1

# 代码

```c++
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> ones(num+1,0);
        int base = 1;
        for(int i = 1; i <= num; i++)
        {
            if(i < base * 2)
                ones[i] = ones[i%base]+1;
            else{
                base *= 2;
                ones[i] = ones[i%base]+1;
            }
        }
        return ones;
    }
};
```

# 更巧妙的代码

最高分代码：f[i] = f[i/2] + i%2

思想：和我的差不多，我是不看最高位，<font color=#ff2299>这个巧妙巧妙在不看最低位，直接右移1位</font>，这个数在数组中肯定已经存在了，然后加上移走那位是0还是1（i%2 或者 i & 1）

**其实整体思想都是把新的二进制模式映射到之前出现的二进制模式上去。**

```java
public int[] countBits(int num) {
    int[] f = new int[num + 1];
    for (int i=1; i<=num; i++) f[i] = f[i >> 1] + (i & 1);
    return f;
}
```



