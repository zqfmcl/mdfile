---
title: Longest Palindromic [M]
date: 2019-10-04 10:00:00
tags: Leetcode
---

## 005.Longest Palindromic [M]

# **题目**

Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

# **思路**

可以用的算法有改良KMP还有manacher（马拉车）算法，毫无疑问，manacher算法是专门用来解决最长子串问题的，也是最简便的。关于这个算法可以看: [Manacher算法](http://blog.csdn.net/hk2291976/article/details/51107886)

```c+
class Solution { 
    public: 
        string longestPalindrome(string s) { 
            //manacher 
            int bound = 0; 
            int id,max_pos=0; 
            int new_len = 2*s.length()+2; 
            vector<int> P(new_len,1); 
            string new_str(new_len-1,'#'); 
            //生成新串，把所有的字符串通过’#’扩展成奇数 
            for(int i = 0;i < s.length();i++) 
            { 
                new_str[2*i+1] = s[i]; 
            } 
            new_str = '$'+new_str +='\0'; //防止越界 
            //manacher算法 
            for(int i=1;i < new_len; i++) 
            {
                if(i < bound) 
                { 
                    P[i] = min(bound-i,P[2*id-i]); //如果在范围内，找对称面的P[id-(i-id)]和max_pos-i的最小值 
                } 
                 while(new_str[i-P[i]] == new_str[i+P[i]])//查找以这个字符为中心的回文串 
                    { 
                        P[i]++; 
                    } 
                    //更新id和bound 
                    if(i+P[i] > bound) 
                    { 
                        bound = i+P[i]; 
                        id = i; 
                    } 
                  
                max_pos = P[i] > P[max_pos]?i:max_pos; 
            } 
            int len = P[max_pos]-1; 
            int start = (max_pos-P[max_pos])/2;
            return s.substr(start,len);
        }
};


```