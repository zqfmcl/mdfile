---
title: Implement strStr()  
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Implement strStr()  

------

# 问题

Implement strStr().

Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack. 

# 思路

```
public class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.length() == 0) return 0;
        int h ,t;
        for(h = 0;h <= haystack.length() - needle.length();h++)
        {
            for(t = 0;t < needle.length();t++)
                    if(haystack.charAt(h+t) != needle.charAt(t)) break;
            if(t == needle.length())
                return h;
        }
        return -1;
    }
}
```

