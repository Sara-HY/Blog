---
title: LeetCode_Linked List Cycle
date: 2019-03-15 10:50:11
categories: LeetCode
tags: 
  - easy
  - linked list
  - two pointers
---

## [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

Given a linked list, determine if it has a cycle in it. To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.
（链表有环）

<!--more-->

**Follow up:** Can you solve it using O(1) (i.e. constant) memory?

**Example:** 

<div align=center>
	<img src="/images/leetcode_141.png" width = "500" align=center/>
</div>

### 1. 哈希表
使用哈希表存储已经遍历过的结点，时间复杂度为 O(n)，空间复杂度为 O(n)。具体实现过程如下：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if not head:
            return False
        
        node_set = set()
        
        p = head
        while p:
            if p in node_set:
                return True
            else:
                node_set.add(p)
            p = p.next
        
        return False   
```

### 2. 双指针
使用两个指针 slow 和 fast，在遍历链表的过程中，slow 移动一步，fast 移动两步。若存在环，两者一定会在某处相遇（在两者都进入环之后，fast一定会追赶上slow）。时间复杂度为 O(n)，空间复杂度为 O(1)。具体实现过程如下：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if not head:
            return False
        
        slow, fast = head, head.next
        
        while slow != fast:
            if not fast or not fast.next:
                return False
            slow = slow.next
            fast = fast.next.next
        
        return True
```