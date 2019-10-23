---
title: Add Two Numbers [M]
date: 2019-10-04 10:00:00
tags: Leetcode
---

## 2.Add Two Numbers [M]

# 题目：

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

# 思路：

题目的大意是两个链表求和，和也是一个链表（链表是逆序存的数字）
这和大数的加减很像，不过这个进位是从后向前。
所以可以同时从前往后加，然后保留进位。

其实做这种大数加减的题目不管是用的大数组还是链表，都是一样的：

- 首先做个大循环，对每一位进行操作：
  - 当前位：(A[i]+B[i])%10
- 进位：（A[i]+B[i]）/10

<font color=red>这里要注意一点，就是可能两个数组不是同样的长度，需要考虑一个数组已经到头，另一个数组还没结束的情况</font>

# 代码

我的这个代码写的不够好，考虑的过于复杂，可以直接看下面更精巧的代码。

```c++
/**
 * Definition for singly-linked list->
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        //异常判断
        if(l1 == NULL && l2 == NULL)
            return NULL;
        if(l1 == NULL)
            return l2;
        if(l2 == NULL)
            return l1;  
        //初始化
        ListNode * result = new ListNode((l1->val + l2->val)%10);
        int carry = (l1->val + l2->val)/10;  //表示进位
        ListNode* templ1 = l1;
        ListNode* templ2 = l2;
        ListNode* tempresult = result;
        //这里弄一个结束节点，有利于当一个节点到结尾后做操作
        ListNode* EndNode = new ListNode(0);
        while(templ1->next != NULL || templ2->next != NULL)
        {
            //如果某个链表已经到结尾了，那么就把它变成EndNode,特点是值为0,next = NULL
            if(templ1->next == NULL)
                templ1 = EndNode;
            else
                templ1 = templ1->next;
            if(templ2->next == NULL)
                templ2 = EndNode;
            else
                templ2 = templ2->next; 
            tempresult->next = new ListNode((templ1->val + templ2->val + carry)%10);            
            carry = (templ1->val + templ2->val + carry)/10;

            tempresult = tempresult->next;
  
        }
        if(carry == 1)
            tempresult->next = new ListNode(1);
        return result;
        
    }
};

```

# 更精巧的代码

不得不说，potpie的这个代码比我上面的代码精简了不少，我上面的代码考虑的太多了，因为我通式用的templ1->val + templ2->val + carry，导致每次需要对先结束的链表进行尾部填充，而且开头多了很多额外的代码。

他的代码，2个链表是独立操作的，而且代码写的很精简，基本没废话！赞

```c++
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode c1 = l1;
        ListNode c2 = l2;
        ListNode sentinel = new ListNode(0);
        ListNode d = sentinel;
        int sum = 0;
        while (c1 != null || c2 != null) {
            sum /= 10;
            if (c1 != null) {
                sum += c1.val;
                c1 = c1.next;
            }
            if (c2 != null) {
                sum += c2.val;
                c2 = c2.next;
            }
            d.next = new ListNode(sum % 10);
            d = d.next;
        }
        if (sum / 10 == 1)
            d.next = new ListNode(1);
        return sentinel.next;
    }
}
```

