---
title: LeetCode_Insert in Sort List
date: 2019-03-15 17:20:58
categories: LeetCode
tags: 
  - medium
  - linked list
  - sort
---

## [Insert in Sort List](https://leetcode.com/problems/insertion-sort-list/)

Sort a linked list using insertion sort.
（基于链表的插入排序）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_147.png" width = "500" align=center/>
</div>

### 1. 头指针
维护一个含头指针的链表 j 来存储排序之后的结果，在遍历链表 i 的过程中，不断地扫描定位到链表 j 的位置，然后插入。具体实现过程如下：

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def insertionSortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:
            return 
        
        new_head = ListNode(-1)
    
        cur_i = head
        while cur_i:
            temp = cur_i.next
            cur_j = new_head
            while cur_j.next and cur_j.next.val <= cur_i.val:
                cur_j = cur_j.next
            cur_i.next = cur_j.next
            cur_j.next = cur_i
            cur_i = temp
            
        
        return new_head.next
```