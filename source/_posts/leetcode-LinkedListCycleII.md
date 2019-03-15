---
title: LeetCode_Linked List Cycle II
date: 2019-03-15 12:00:02
categories: LeetCode
tags: 
  - medium
  - linked list
  - two pointers
---

## [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

Given a linked list, return the node where the cycle begins. If there is no cycle, return null. To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.
（链表中环的起点）

<!--more-->

**Note:** Do not modify the linked list.

**Example:** 

<div align=center>
	<img src="/images/leetcode_142.png" width = "500" align=center/>
</div>

### 1. 两个指针
根据前一题的思路，首先找到 slow 和 fast 第一次相遇的位置，则 slow 走了（x+a），fast 走了 （x+a+b+a）。（其中a为环中起始点到相遇点的位置，ba为环中相遇点再到起始点的位置），从而有 2(x+a）=（x+a+b+a），即x = b。说明 fast 从当前继续出发， slow 从链表头再出发，两者相遇的位置就是环起始位置。具体实现过程如下：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return None
        
        slow, fast = head, head.next
        
        while slow != fast:
            if not fast or not fast.next:
                return None
            slow = slow.next
            fast = fast.next.next
        
        slow, fast = head, fast.next
        while slow != fast:
            slow = slow.next
            fast = fast.next
            
        return slow
```