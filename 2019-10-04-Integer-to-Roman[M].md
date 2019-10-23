---
title: Integer to Roman[M]
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Integer to Roman[M]

------

# 问题

Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.

# 思路

分析罗马数字的规律：

| Symbol | Value |
| ------ | ----- |
| I      | 1     |

|V |	5
|X 	|10
|L 	|50
|C |	100
|D| 	500
|M| 	1,000

上面是罗马数字所有的符号。
罗马数字的规则：
一般情况下，从左到右从大到小排，字母代表的数字累加。
比如：

> XII = 12
>
> MDCCLXVI= 1000+500+100+100+50+10+5+1 

但是有特殊情况，就是，如果数字的范围在大数减小数的范围内，则会出现小数在大数前面的情况，代表（大数-小数）

> IV = 5-1
> IX= 10 - 1 = 9
> XL = 50-10 = 40

| Symbol | Value |
| ------ | ----- |
| IV     | 4     |

|IX |	9
|XL 	|40
|XC 	|90
|CD |	400
|CM| 	900

## 思路1——循环

一旦把所有可能的情况符号情况都列举出来了，就好做了。
我们现在拿到一个数N

1. 我们就去表里面找不超过它的最大的数x，
2. 然后把它入我们的输出字符串中，然后将数N-=x，
3. 继续执行这个操作，直到N=0

```java
public class Solution {
    public String intToRoman(int num) {
        int list[] = {1000,900,500,400,100,90,50,40,10,9,5,4,1};
        String chars[] = {"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
        int i = 0;
        String out="";
        while(num > 0)
        {
            for(;i < list.length;i++)
                if(num >= list[i])
                    break;
            out+=chars[i];
            num -= list[i];
        }
        return out;
    }
}
```

## 思路2——查表

还有个更极端的方案，就是，把每位上可能出现的情况都列举出来，剩下的，只用查表就行了。

```java
public class Solution {
  public static String intToRoman(int num) {
        String M[] = {"", "M", "MM", "MMM"};
        String C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        String X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        String I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
        return M[num/1000] + C[(num%1000)/100] + X[(num%100)/10] + I[num%10];
    }
}

```

