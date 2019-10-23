---
title: ZigZag Conversion[E]
date: 2019-10-04 10:00:00
tags: Leetcode
---

## 006.ZigZag Conversion[E]

# 题目

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

![Alt text](C:/Users/Administrator/Desktop/leetbook-master/%E8%A7%84%E5%BE%8B/1460215156918.png)

And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:

> string convert(string text, int nRows);

convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

## 思路1——用字符串数组

我能说我一开始完全没看懂吗？我是根据**Custom Testcase**自己慢慢测试摸索出来的。
其实，应该是这样的
2行：
A _ C _ E _
_ B _ D _ F

3行：
A _ _ _ E _ _ _  I _ _ _
_ B _ D _ F _ H _ J _
_ _ C _ _ _ G _ _ _ K

所以有个简单的思路：

- 每行弄个string。
- 对原始字符串进行扫描，从上往下，从下往上，依次加入每行的string
- 最后把所有的string拼接起来

```c++
 class Solution {
public:
    string convert(string s, int numRows) {
        string str[numRows],tmp;
        if(numRows == 1)
            return s;
        int flag;
        for(int i = 0,j = 0;i < s.length(); i++)
        {
            if(j == 0)
                flag = 1;
            if(j == numRows-1)
                flag = -1;
            str[j] += s[i];
            j += flag;            
        }
        for(int i = 0; i < numRows;i++){
            tmp += str[i];
        }
        return tmp;
    }
};
```

## 思路2——观察规律

2行：
A _ C _ E _
_ B _ D _ F

3行：
<font color=red>A </font>_ _ _ <font color=red>E </font>_ _ _  <font color=red>I </font>_ _ _
_ B _ D _ F _ H _ J _
_ _ C_ _ _ G  _ _ _ K

4行：
<font color=red>A </font>_ _ _ _ _ <font color=red> G </font>_ _ _ _ _
_ B _ _ _ F _ H _ _ _
_ _ C _ E _ _ _ I _ K
_ _ _ D  _ _ _ _ _ J

观察规律后，以每行的元素作为轴，可以发现，下面的字母都是对称排列的
换成对应的index后，规律更明显
<font color=red>0 </font>_ _ _ <font color=red>4 </font>_ _ _  <font color=red>8 </font>_ _ _
_  1 _ 3 _ 5 _ 7 _ 9 _
_ _ 2 _  _ _ 6  _ _ _ 10 

第2层的元素就是以第一行的元素为轴，+1,-1
第三层的元素就是以第一行的元素为轴，+2,-2
……
但是最后一层的元素，由于其特殊性，我们可以只考虑+k

Ps.所有过界的元素都不考虑

轴也有规律：除了首尾两层，其他都是2个，所以第一层每隔**2n-2**出现一次。

```c++
class Solution {
public:
    string convert(string s, int numRows)
    {
        string tmp;
        if(numRows == 1)
            return s;
        int inc = 2*numRows-2;  //每次轴增加的步长
        int len = s.length();
        for(int i = 0; i < numRows;i++)
        {
            for(int j = 0;j < s.length()+numRows; j += inc)
            {
                if(j - i > 0 && j - i < s.length() 
                && i != 0 && i != numRows -1)  //首，尾只考虑+不考虑-
                    tmp+= s[j-i];
                if(j + i < s.length())
                    tmp += s[j+i];
            }
        }
        return tmp;
    }
};
```