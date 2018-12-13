---
title: LeetCode_Swap Nodes in Pairs
date: 2018-12-13 21:47:54
categories: LeetCode
tags: 
  - medium
  - linked list
---

## [Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)

Given a linked list, swap every two adjacent nodes and return its head.
（交换链表中相邻的两个值）

<!--more-->

Note:

Your algorithm should use only **constant** extra space.
You may not modify the values in the list's nodes, only nodes itself may be changed.

**Example:**

<div align=center>
	<img src="/images/leetcode_24.png" width = "500" align=center/>
</div>


### 链表指针
这个题是一个很直观的指针问题，在设计算法的过程中将指针的变换在纸上设计出来即可得出算法，具体实现过程如下：
**（引入头指针是一个链表中常用的方法）**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        newNode = ListNode(0)
        newNode.next = head
        
        p = newNode
        while p.next and p.next.next:
            q = p.next
            p.next = q.next
            q.next = p.next.next
            p.next.next = q
            p = q
               
        return newNode.next
```

