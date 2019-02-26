---
title: LeetCode_Reverse Linked List II
date: 2019-02-26 23:55:09
categories: LeetCode
tags: 
  - medium
  - linked list
---

## [Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/)

Reverse a linked list from position m to n. Do it in one-pass.
（旋转link_list[m:n+1]）

<!--more-->

**Note:** 1 ≤ m ≤ n ≤ length of list.

**Example:** 

<div align=center>
	<img src="/images/leetcode_92.png" width = "500" align=center/>
</div>

### 1. In-place
具体实现方法如下：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseBetween(self, head: ListNode, m: int, n: int) -> ListNode:
        new_head = ListNode(0)
        new_head.next = head
        
        p_pre = new_head
        p_cur = head
        for i in range(1, m):
            p_pre = p_pre.next
            p_cur = p_cur.next
     
        for j in range(n-m):
            p_head = p_pre.next
            p_pre.next = p_cur.next
            p_temp =  p_cur.next
            p_cur.next = p_cur.next.next
            p_temp.next = p_head
           
        return new_head.next
```