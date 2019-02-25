---
title: LeetCode_Partition List
date: 2019-02-25 14:30:54
categories: LeetCode
tags: 
  - medium
  - linked list
  - two pointers
---

## [Partition List](https://leetcode.com/problems/partition-list/)

Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x. You should preserve the original relative order of the nodes in each of the two partitions.
(切分链表)

<!--more-->


**Example:**

<div align=center>
	<img src="/images/leetcode_86.png" width = "500" align=center/>
</div>

### 1. 两个指针 In-place
第一种是 in-place，具体实现过程如下：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def partition(self, head: ListNode, x: int) -> ListNode:
        new_head = ListNode(0)
        new_head.next = head
        
        p_pre = new_head
        p_cur = head
          
        p_insert = None
        while p_cur:
            if p_cur.val >= x and not p_insert:
                p_insert = p_pre
            elif p_cur.val < x:
                if p_insert:
                    p_pre.next = p_cur.next
                    p_cur.next = p_insert.next
                    p_insert.next = p_cur
                    p_cur = p_pre.next
                    p_insert = p_insert.next
                    continue
            p_pre = p_pre.next
            p_cur = p_cur.next
        
        return new_head.next
```

### 2. 两个指针 
第二种是新构建两个链表分别存储，具体实现过程如下：

```python
class Solution:
    def partition(self, head: ListNode, x: int) -> ListNode:
        p_l = l_head = ListNode(0)
        p_r = r_head = ListNode(0)
        
        p_cur = head
        while p_cur:
            if p_cur.val >= x:
                p_r.next = p_cur
                p_r = p_r.next
            else:
                p_l.next = p_cur
                p_l = p_l.next
            p_cur = p_cur.next
        
        p_l.next = r_head.next
        p_r.next = None
        return l_head.next
```