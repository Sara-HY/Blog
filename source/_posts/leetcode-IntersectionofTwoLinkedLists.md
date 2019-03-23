---
title: LeetCode_Intersection of Two Linked Lists
date: 2019-03-23 17:49:53
categories: LeetCode
tags: 
  - easy
  - linked list
  - two pointers
---

## [Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

Write a program to find the node at which the intersection of two singly linked lists begins. For example, the following two linked lists:
（两个链表相交的结点）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_160.png" width = "500" align=center/>
</div>


### 1. 暴力轮循
使用这种方式的时间复杂度为 O(mn)，空间复杂度为 O(1)。


### 2. 哈希表
使用这种方式的时间复杂度为 O(m+n)，空间复杂度为 O(m+n)。


### 3. 两个指针
根据图中的示例，我们可以发现，两个链表若有交叉点，则主要长度不同的部分在交叉点之前。因此我们使用两个指针分别遍历两个链表，当某一个指针遍历到链尾时，从另一个链表开始。如此一来，在两个指针都遇到链尾并从头开始时，这一次的遍历一定会在相交点相遇。若不存在交叉点，则此时两个链表都在链尾为None。使用这种方式的时间复杂度为 O(m+n)，空间复杂度为 O(1)。具体实现过程如下：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        if not headA or not headB:
            return None
        
        pA, pB = headA, headB
        
        while pA != pB:
            if pA:
                pA = pA.next
            else:
                pA = headB
            if pB:
                pB = pB.next
            else:
                pB = headA
        
        return pA
```