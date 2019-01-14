---
title: LeetCode_Rotate List
date: 2019-01-14 12:01:43
categories: LeetCode
tags: 
  - medium
  - back tracking
---

## [Rotate Image](https://leetcode.com/problems/rotate-image/)

Given a linked list, rotate the list to the right by k places, where k is non-negative.
(k 次旋转链表)

<!--more-->

**Example:**
<div align=center>
	<img src="/images/leetcode_61.png" width = "500" align=center/>
</div>


### 1. 旋转 k 次
首先获得链表的长度，然后每一次旋转链表都将链表的链尾排到链首，如此循环 k 次。具体实现方法如下：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def rotateRight(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        if not (head and head.next) :
            return head
    
        cur = head
        length = 1
        while cur.next:
            cur = cur.next
            length += 1
        
        k = k % length
        new_head = ListNode(0)
        new_head.next = head
        
        while k > 0:
            p_tail_before = new_head
            p_tail = new_head.next
            while p_tail.next != None:
                p_tail_before = p_tail_before.next
                p_tail = p_tail.next
            p_tail.next = new_head.next
            p_tail_before.next = None
            new_head.next = p_tail
            k -= 1
        
        return new_head.next
```

### 2. 旋转 1 次

在获取链表的长度的同时，将其转换成一个循环链表，计算出当前应该由谁作为链首，这样将链表分为两部分再重新拼接。具体实现方法如下：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def rotateRight(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        if not (head and head.next) :
            return head
    
        cur = head
        length = 1
        while cur.next:
            cur = cur.next
            length += 1
        # Circular list
        cur.next = head
        
        k = k % length
        index = length - k
        
        p_head_before = cur
        p_head = head
        # get the new head of the list
        for i in range(index):
            p_head_before = p_head_before.next
            p_head = p_head.next
        
        p_head_before.next = None
        
        return p_head
```
