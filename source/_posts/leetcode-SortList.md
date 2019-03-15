---
title: LeetCode_Sort List
date: 2019-03-15 18:30:34
categories: LeetCode
tags: 
  - medium
  - linked list
  - sort
---

## [Sort List](https://leetcode.com/problems/sort-list/)

Sort a linked list in O(n log n) time using constant space complexity.
（实现实现复杂度为O(nlog(n))的链表排序）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_148.png" width = "500" align=center/>
</div>

### 1. 归并排序

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def merge(self, left, right):
        new_head = ListNode(0)
        cur, left_i, right_i = new_head, left, right
        
        while left_i and right_i:
            if left_i.val < right_i.val:
                cur.next = left_i
                left_i = left_i.next
            else:
                cur.next = right_i
                right_i = right_i.next
            cur = cur.next
        
        if left_i:
            cur.next = left_i
        else:
            cur.next = right_i
            
        return new_head.next
           
    def sortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:
            return head
        
        # 定位到链表的中部
        slow, fast = head, head.next
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        middle = slow.next
        slow.next = None
        
        left = self.sortList(head)
        right = self.sortList(middle)
        
        return self.merge(left, right)
```