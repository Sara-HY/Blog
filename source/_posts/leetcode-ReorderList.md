---
title: LeetCode_Reorder List
date: 2019-03-15 13:49:30
categories: LeetCode
tags: 
  - medium
  - linked list
---

## [Reorder List](https://leetcode.com/problems/reorder-list/)

Given a singly linked list L: L0→L1→…→Ln-1→Ln, reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→… You may not modify the values in the list's nodes, only nodes itself may be changed.
（链表重新排序）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_143.png" width = "500" align=center/>
</div>

### 1. 切分 & 倒叙链表
首先使用 slow 和 fast 两个指针来遍历链表，找到链表的中部；然后将链表后半部分倒序；最终将倒序后的后半部分的链表插入到前半部分中。时间复杂度为O(n)，时间复杂度为O(1)。具体实现方法如下：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: None Do not return anything, modify head in-place instead.
        """
        if not head or not head.next:
            return
        
        # 找到链表的中部
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        middle = slow.next
        slow.next = None
        
        # 将链表后半部分倒序
        new_head = ListNode(0)
        while middle:
            temp = middle.next
            middle.next = new_head.next 
            new_head.next = middle
            middle = temp
        
        # 将倒序后的后半部分的链表插入到前半部分中
        p, q = head, new_head.next
        while p and q:
            temp = q.next
            q.next = p.next
            p.next = q
            q = temp
            p = p.next.next
        
        return
```