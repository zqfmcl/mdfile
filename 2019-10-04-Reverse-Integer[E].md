---
title: Reverse Integer[E]
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Reverse Integer[E]——处理溢出的技巧

------

# **题目**

Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

# **思路**

这题完全没丝毫的难度，任何人几分钟都可以写出来，但是，这题修改后，加入了一个新的测试，瞬间大家讨论的就多了，就是——溢出测试

因为整数只有32位，可能原数不会溢出，但是转置后就不一定了，所以必须要考虑溢出的情况。

# **思路1——用long**

一个比较讨巧的方案，直接用long不会溢出再和INT_MAX比较就好了

```c++
class Solution {
public:
    int reverse(int x) {
        long tmp=0;
        while(x != 0)
        {
            tmp *=10;
            tmp += x%10;
            if(tmp > INT_MAX || tmp < INT_MIN)
                return 0;
            x /= 10;
        }
        return tmp;
    }
};
```

# **思路2——变化前后对比**

bitzhuwei的代码。
不用任何flag和INT_MAX宏或者任何硬编码Ox7fffffff
这个思路 也是很容易理解的，做一些操作，如果溢出了，那溢出后的值做反向操作会和之前的值不一样。

> 这里就用一个变量存储变化后的值，每次做反向操作，如果和之前的值一样就更新，不一样，说明溢出了。

```c++
public int reverse(int x)
{
    int result = 0;

    while (x != 0)
    {
        int tail = x % 10;
        int newResult = result * 10 + tail;
        if ((newResult - tail) / 10 != result)
        { return 0; }
        result = newResult;
        x = x / 10;
    }

    return result;
}
```

### **思路3——提前停止操作**

如果当前的数已经>INT_MAX/10 那么再做一次操作，必然溢出。

```c++
class Solution
{
public:
    int reverse(int n)
    {
        int result = 0;

        while (n != 0)
        {
            if (result > INT_MAX / 10
                    || ((result == INT_MAX / 10) && (n % 10 > INT_MAX % 10)))
            {
                result = 0;
                break;
            }
            if (result < INT_MIN / 10
                    || ((result == INT_MIN/ 10) && (n % 10 < INT_MIN % 10)))
            {
                result = 0;
                break;
            }
            result = result * 10 + n % 10;
            n = n / 10;
        }


        return result;
    }
};
```

