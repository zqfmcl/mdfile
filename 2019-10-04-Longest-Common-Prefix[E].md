---
title: Longest Common Prefix[E]
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Longest Common Prefix[E]

------

# 问题

Write a function to find the longest common prefix string amongst an array of strings.

Subscribe to see which companies asked this question

# 思路

这个没啥思路的，怎么都要两重循环，因为是最长公共子串，随便找一个(一般是第一个作为基准)，然后拿拿的首部慢慢去匹配后面的字符串就行了。

```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        String s = "";
        if(strs.length == 0)
            return "";
        for(int i = 0; i < strs[0].length();i++)
        {
            char c = strs[0].charAt(i);
            for(int j = 1;j < strs.length;j++)
            {
                if(i >= strs[j].length() || strs[j].charAt(i) != c)
                    return s;
            }
            s += c;
        }
        return s;
    }
}
```

