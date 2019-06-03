---
title: LeetCode_Reverse Linked List
date: 2019-06-03 08:19:22
categories: LeetCode
tags: 
  - easy
  - linked list
---

## [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

Reverse a singly linked list.
（翻转链表）

<!--more-->

Note:
A linked list can be reversed either iteratively or recursively. Could you implement both?



**Example:** 

<div align=center>
	<img src="/images/leetcode_206.png" width = "500" align=center/>
</div>


### 1. 迭代法
构建一个头结点，在遍历链表的过程中不断地采用头插法即可翻转链表。具体实现过程如下：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        new_head = ListNode(0)
        
        p = head
        while p:
            tmp = p.next
            p.next = new_head.next
            new_head.next = p
            p = tmp
        
        return new_head.next
```

### 2. 递归法
递归的翻转后面的字符串，然后将当前的头结点放在最尾部，具体实现过程如下：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        
        new_head = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        
        return new_head
```





