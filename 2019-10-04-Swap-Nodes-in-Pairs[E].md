---
title: Swap Nodes in Pairs[E]
date: 2019-10-04 10:00:00
tags: Leetcode
---

1. Swap Nodes in Pairs[E]

------

# 题目

Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given 1->2->3->4, you should return the list as 2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

# 思路

这个题目的意思是每2个元素要交换一下，我们已经做了很多有关链表的问题，知道凡是涉及链表的操作，比较麻烦的地方都在与链表的操作都必须涉及到它的父亲。

这题也不例外，需要考虑很多问题：

1. 如果链表头要交换怎么办
2. 如何方便的交换两个节点
3. 如果长度不为偶数怎么办

问题1我们已经说过很多遍了，直接用一个新节点去解决这个问题。

```
  ListNode newhead = new ListNode(0);
```

问题2，这里得知道，如果涉及到链表交换操作，那么它<font color=red>至少涉及3个节点：</font><font color=blue>当前节点，当前节点的父亲，当前节点的孩子</font>这里由于我们循环是从前往后走的，所以我们这里使用：<font color=blue>当前节点，当前节点的孩子，当前节点的孙子</font>，可能更方便。
	

```
	 ListNode first = current.next;
     ListNode second = current.next.next;
```

交换操作就很简单了

```
	first.next = second.next;
    current.next = second;
    current.next.next = first;
    current = current.next.next;
```

问题3，我们得需要加入判断，当前节点的孩子和孙子都要有才能继续

```
 while (current.next != null && current.next.next != null) 
```



所以这样一分析，代码就很容易写出来了

# 代码

```java
public class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head == null)
            return null;
        ListNode newhead = new ListNode(0);
        newhead.next = head;
        ListNode current = newhead;
        while (current.next != null && current.next.next != null) {
            ListNode first = current.next;
            ListNode second = current.next.next;
            first.next = second.next;
            current.next = second;
            current.next.next = first;
            current = current.next.next;
        }
        return newhead.next;
    }
}
```

