---
title: String to Integer (atoi) [E]
date: 2019-10-04 10:00:00
tags: Leetcode
---

# 008. String to Integer (atoi) [E]

------

[TOC]

## **题目**

Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

## **思路**

这题也比较好做，关键是要考虑挺多东西，我也是提交了好多次才发现有这么多要考虑的地方。

- 开头的空格
- 正负符号的处理
- 溢出处理
- 非法输入



开头空格处理：

```
while(str[i] == " ") i++;
```

正负号的处理：我觉得yuruofeifei这个解决方案简直赞

```
if (str[i] == '-' || str[i] == '+') {
      sign = 1 - 2 * (str[i++] == '-'); 
 }
 ……
 return base * sign;
```

溢出处理（可以参考上一道题）：

```
if (base >  INT_MAX / 10 || (base == INT_MAX / 10 && str[i] - '0' > INT_MAX%10)) {
            if (sign == 1) return INT_MAX;
            else return INT_MIN;
        }
```

非法输入：其实只用过滤就行了

```
 while (str[i] >= '0' && str[i] <= '9') {
 ……
 }
```

## **代码**

我的代码，不够简洁，可以参考yuruofeifei的代码，在下面

```c++
class Solution {
public:
    int myAtoi(string str) {
        long tmp=0;
        bool neg;
        int i = 0;
        while(str[i] == ' ') i++; //读掉空格
        neg = str[i] == '-'?1:0;
        for(i = i+ (neg || str[i] == '+');i < str.length();i++)  //如果是- 或 + i+1跳过符号
        {
            if(str[i] - '0' >= 0 && str[i] - '0' < 10)   //过滤非法输入
            {
               tmp *= 10;
               tmp += (str[i] - '0'); 
               if(tmp >= INT_MAX && !neg)    //溢出判断
               {
                   tmp =  INT_MAX;
                   break;
               }
               if(tmp -1  >= INT_MAX && neg)  //除了符号，INT_MAX和INT_MIN只差1
               {
                   tmp = INT_MIN;
                   break;
               }
            }
            else break;
        }
        if(neg) return -tmp;
        return tmp;
    }
};
```



yuruofeifei的代码

```c++
int myAtoi(string str) {
    int sign = 1, base = 0, i = 0;
    while (str[i] == ' ') { i++; }
    if (str[i] == '-' || str[i] == '+') {
        sign = 1 - 2 * (str[i++] == '-'); 
    }
    while (str[i] >= '0' && str[i] <= '9') {
        if (base >  INT_MAX / 10 || (base == INT_MAX / 10 && str[i] - '0' > 7)) {
            if (sign == 1) return INT_MAX;
            else return INT_MIN;
        }
        base  = 10 * base + (str[i++] - '0');
    }
    return base * sign;
}
```

