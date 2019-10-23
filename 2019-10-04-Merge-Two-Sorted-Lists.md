---
title: Merge Two Sorted Lists  
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Merge Two Sorted Lists  

------

# 问题

Merge two sorted linked lists and return it as a new list. 

# 思路

这个题目很简单也有几个可以考虑的思路，一个是比较直接的方式，重新构造链表，一种是利用递归

# 思路1 ：用新的链表

这里用了一个新的节点了保存结果的链表，这里为了方便链表的扩充，增加一个临时的节点变量（否则每次加入都要遍历到尾部）

```java
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode result = new ListNode(0);
        ListNode tmp = result;
        while(l1 != null || l2 != null)
        {
            if(l2 == null || (l1 != null && l1.val <= l2.val))
            {
                tmp.next = l1;
                l1 = l1.next;
            }
            else 
            {
                tmp.next = l2;
                l2 = l2.next;
            }
            tmp = tmp.next;
        }
        return result.next;
    }
}

```

# 思路2：递归方案

在很多时候，递归的方案可以提供一种清晰简单的解决方案，代码也更精炼。但是递归有个问题就是容易出现堆栈溢出的问题。

```java
public:
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2) {
        if(l1 == NULL) return l2;
        if(l2 == NULL) return l1;

        if(l1->val < l2->val) {
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        } else {
            l2->next = mergeTwoLists(l2->next, l1);
            return l2;
        }
    }
};

```

