---
title: Divide Two Integers[M]
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Divide Two Integers[M]

------

# 问题

Divide two integers without using multiplication, division and mod operator.

If it is overflow, return MAX_INT.

# 思路

这道题难在不能使用乘除取余操作，所以我们只能手动的实现除法，我们来看看如何实现。

我们假设被除数为`D`，除数为`d`

## 手动实现除法

首先，本能想到10 = 2*5 ，10/2 = 5，说明10中有5个2，这里可以用循环来做，看`D`中间有多少个`d`就行了。

本能写出一个循环应该不难。

```java
 for(i = 0;dividend - divisor >= 0 ;i+=1)
        {
            dividend = dividend - divisor;
        }

```

## 符号

现在有另一个问题，正负数怎么办？我们知道，除法里，异号为负，同号为正，既然不能使用乘除判断，那我们就只能写个判断，这个flag到时候就充当标志。

```
 boolean flag = (dividend > 0 && divisor < 0 || dividend < 0 && divisor > 0);
```

当然还有更好的实现方式，既然不能用乘除，可以用位运算呀，这和异或操作的含义刚好一样。

```
 boolean sign = ((dividend < 0) ^ (divisor < 0));
```

然后，把`D`和`d`同时取绝对值就好了。

```
	 long did = Math.abs((long)dividend);
     long dis = Math.abs((long)divisor);
```

**注意：**这里除数一定要用long，因为如果最小值取绝对值会溢出

## 溢出

我们知道，除法可能产生溢出的情况就是`D`为0，或者`D`为`最小值`，`d`为-1

```
if (!divisor || (dividend == Integer.MIN_VALUE && divisor == -1))
            return Integer.MAX_VALUE;
```

## 更快的方案

好了，我们可以测试下代码。发现超时，想想也是，上面的循环太慢了。其实我们稍微想一下就可以提速，我们可以采用逐渐逼近的思路：

- 我们先看i = N个`d`可不可以
- 如果可以，我们看看i = 2N个`d`可以不可以
  - 如果还可以就继续看i = 4N个`d`可以不可以
    - 直到不可以减，我们让`D`减去i个`d` 

这里为什么使用2的倍数，因为可以用位运算呀~~

```
d << 1 就相当与d*2
d << 2 就相当与d*4
```

我们再用一个i来就记数 i = 0 开始

```
1 << 0 就相当于1
1 << 1 就相当于2
1 << 2 就相当与4
```

这里我们用一个临时变量`mul_d`存`d`的左移操作，**注意：**`mul_d`必须为long，因为左移操作很可能溢出！！

现在我们可以写出以下代码了。

```java
public class Solution {
    public int divide(int dividend, int divisor) {
        if(divisor == 0 || (dividend == Integer.MIN_VALUE && divisor == -1))
            return Integer.MAX_VALUE;
        int i,total = 0;
        //判断正负号
        boolean sign = ((dividend < 0) ^ (divisor < 0));
        //这里必须要long,因为如果最小值取绝对值会溢出
        long did = Math.abs((long)dividend);
        long dis = Math.abs((long)divisor);
        while(did >= dis)
        {
            long mul_dis = dis;
            i = 0;
            //每次左移乘2，记录下来，直到不能减
            while(did >= (mul_dis<<1)) 
            {
                i++;
                mul_dis <<= 1;
            }
            did -= mul_dis;
            total += 1<<i;
        }
        //根据符号返回
        return sign?-total:total;
    }
}
```

