---
title: LeetCode_Remove Duplicates from Sorted List
date: 2019-02-23 16:45:56
categories: LeetCode
tags: 
  - easy
  - linked list
---

## [Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)

Given a sorted linked list, delete all duplicates such that each element appear only once.
（移除链表中的重复元素（所有元素只出现一次））

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_83.png" width = "500" align=center/>
</div>

### 1. 指针遍历

在遍历过程中维护一个 p_pre 来记录重复元素之前的位置。具体实现过程如下：

```python
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        new_head = ListNode(0)
        new_head.next = head
            
        p_pre = new_head   
        p_cur = new_head.next
        while p_cur != None:
            while p_cur.next and p_cur.val == p_cur.next.val:
                p_cur = p_cur.next
            p_pre.next = p_cur
            p_pre = p_cur
            p_cur = p_cur.next 
        
        return new_head.next
```