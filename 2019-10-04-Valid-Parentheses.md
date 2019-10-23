---
title: Valid Parentheses  
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Valid Parentheses  

------

# 问题

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

# 思路

这道题很简单，就是一个经典的栈的例子——表达式中的括号符号匹配。

- 遇见了左括号就进栈
- 遇见了右括号就出栈
  - 如果栈为空，出错
  - 如果出栈元素不是匹配的括号，出错

这里解决出括号匹配用了一个小tick，就是利用ASCII码，匹配的括号的ascii码都不会相差太远

- '(' ')' 相差1
- '[' ']'  '{' '}' 相差2

```java
public class Solution {
    public boolean isValid(String s) {
        if(s.length() == 0)
            return false;
        Stack<Character> stack = new Stack<Character>(); // 创建堆栈对象 
        for(int i = 0;i < s.length(); i++)
        {
            if(s.charAt(i) == '(' || s.charAt(i) == '[' || s.charAt(i) == '{')
                stack.push(s.charAt(i));
            if(s.charAt(i) == ')' || s.charAt(i) == ']' || s.charAt(i) == '}')
            {
                if(stack.empty()) return false;
                char out = stack.pop();
                if(out - s.charAt(i) > 2)
                    return false;
            }
        }
        if(stack.empty())
            return true;
        return false;
    }
}
```