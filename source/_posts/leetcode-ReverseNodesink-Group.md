---
title: LeetCode_Reverse Nodes in k-Group
date: 2018-12-18 13:48:13
categories: LeetCode
tags: 
  - hard
  - linked list
---

## [Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)

Given a linked list, reverse the nodes of a linked list k at a time and return its modified list. k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.
（链表分组倒排）

Note:
 * Only constant extra memory is allowed.
 * You may not alter the values in the list's nodes, only nodes itself may be changed.

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_25.png" width = "500" align=center/>
</div>


### 1. 链表指针问题（头节点）
遍历链表的过程中保存每 k 个的一组的头尾指针，将其翻转之后继续遍历。具体实现如下：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverse(self, p_prev_head, p_head, p_tail, k):
        p = p_head
        new_p = ListNode(0)
        new_p.next = p_tail.next

        while k != 0:
            k -= 1
            tmp = p.next
            p.next = new_p.next
            new_p.next = p
            p = tmp
        
        p_prev_head.next = new_p.next
         
    def reverseKGroup(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        if k == 1:
            return head
        
        new_head = ListNode(0)
        new_head.next = head
        
        p_prev_head = new_head
        p_head = head
        p_tail = head
        
        i = 1
        while p_tail != None:
            if i == k:
                i = 1
                self.reverse(p_prev_head, p_head, p_tail, k)
                p_prev_head = p_head
                p_head = p_prev_head.next
                p_tail = p_head
            else:
                i += 1
                p_tail = p_tail.next
        
        return new_head.next
```

