---
title: leetcode_Remove Nth Node From End of List
date: 2018-12-06 14:41:28
categories: LeetCode
tags: 
  - medium
  - linked list
  - two pointers
---

## [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

Given a linked list, remove the n-th node from the end of list and return its head.
（删除链表尾开始的第 N 个）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_19.png" width = "500" align=center/>
</div>

### 1. 正向定位
这个是一个简单的链表增删的问题。从后往前删除，我们可以先通过遍历一次确定链表的长度，从而可以正向的定位到需要删除的位置。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        p = head
        length = 0
        while p != None:
            p = p.next
            length += 1
        
        if n > length:
            return head
        elif n == length:
            return head.next
        else:
            p = head
            k = length - n - 1
            while k != 0:
                k -= 1
                p = p.next
            p.next = p.next.next
            return head
```