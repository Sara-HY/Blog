---
title: LeetCode_Merge Two Sorted Lists
date: 2018-12-06 16:02:30
categories: LeetCode
tags: 
  - easy
  - linked list
---

## [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
（合并有序链表）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_21.png" width = "500" align=center/>
</div>

### 1. 三个链表指针
链表合并问题，三个指针分别指向当先的l1，当前的l2 以及合并后的链表的尾指针，然后遍历两个链表，具体的实现过程如下：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if l1 == None:
            return l2
        if l2 == None:
            return l1
        
        if l1.val <= l2.val:
            target = l1
            p = l1.next
            q = l2
        else:
            target = l2
            p = l1
            q = l2.next
        tail = target
        
        while p != None and q != None:
            if p.val <= q.val:
                tail.next = p
                tail = p
                p = p.next
            else:
                tail.next = q
                tail = q
                q = q.next
            
        if p != None:
            tail.next = p
        else:
            tail.next = q
        
        return target
```

### 2. 增加头结点
在上述的方法中，需要单独判断最终的头结点来自 l1 还是 l2，因此可以为目标链表设定一个头结点，则可以省去此步骤的判断。具体的实现过程如下：

```python
class Solution:
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if not l1 or not l2:
        	return l1 or l2

        tail = target = ListNode(0)
        
        while l1 and l2:
            if l1.val <= l2.val:
                tail.next = l1
                l1 = l1.next
            else:
                tail.next = l2
                l2 = l2.next
            tail = tail.next
            
        tail.next = l1 or l2
        
        return target.next
```