---
title: Remove Nth Node From End of List S
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Remove Nth Node From End of List 

------

# 问题

Given a linked list, remove the nth node from the end of list and return its head.

For example,

> Given linked list: 1->2->3->4->5, and n = 2.

> After removing the second node from the end, the linked list becomes 1->2->3->5.

# 思路

这是链表中非常常见的问题，众所周知，链表慢就慢在遍历查找，而对于单链表来说，每次必须从头开始搜索，这样使得链表在处理“倒数”这个概念的时候，特别无力。常规的做法必须要2遍遍历：1遍计算链表长度len，1遍搜索倒数的元素len-n。(当然，你可以通过加入链表长度变量或者使用双向链表解决这个问题。)

但是题目要求是一遍完成，有没有一遍的思路呢？其实是有的，那就是双指针或递归。

## 思路一 ——双指针



这里有个常用的做法去解决“倒数问题”：双指针。

双指针常用做法是：

- 一个指针用来作为参考，控制长度（作为循环停止条件）
- 一个指针延迟启动用来跑“倒数”。

第一个指针先运行n个数，然后打开第二个指针，这样，当第一个指针跑完时，第二个指针刚好跑过Len-N数，这样就找到了倒数第n个数。

注意：由于删除操作比较特殊，必须找到前一个节点才能删除下个节点，所以一般删除操作我们会构造一个虚拟节点作为开头，以防开头节点被删除。

```
public class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode newhead = new ListNode(-1);  //防止头被删除
        newhead.next = head;
        ListNode point1 = newhead;
        ListNode point2 = newhead;
        for(;point1 != null;point1 = point1.next,n--)  //point1 控制长度
        {
            if(n < 0)
                point2 = point2.next;   //point2延迟启动
        } 
        point2.next = point2.next.next;
        return newhead.next;
    }
}
```

## 思路二 —— 递归

除了用双指针外，还可以考虑用递归，凡是这种涉及单链表插入删除操作的时候，都可以考虑用递归，因为插入和删除都需要涉及它的父亲操作。我们考虑最后一个元素是第一层，然后逐级返回，当返回到第N+1层（也就是父亲节点所在层数）就开始删除操作。

```
public class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode newhead = new ListNode(-1);
        newhead.next = head;
        remove(newhead,n); 
        return newhead.next;
    }

    private int remove(ListNode node, int n) {
        if(node.next == null) return 1;
        int level = remove(node.next,n)+1; //层数+1
        if(level == n+1)    //找到了父亲
            node.next = node.next.next;
        return level;   
    }
}
```

