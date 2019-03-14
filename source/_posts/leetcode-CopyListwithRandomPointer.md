---
title: LeetCode_Copy List with Random Pointer
date: 2019-03-14 20:51:20
categories: LeetCode
tags: 
  - medium
  - hash table
  - linked list
---

## [Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null. Return a **deep copy** of the list.
（深拷贝链表）

<!--more-->

**Note:** You must return the copy of the given head as a reference to the cloned list.

**Example:** 

<div align=center>
	<img src="/images/leetcode_138.png" width = "500" align=center/>
</div>

### 1. 哈希表
首先忽略 random 遍历链表，构建链表节点到拷贝后节点之间的映射，然后考虑 random 重新遍历链表，根据映射关系维护新链表的链接关系，具体实现方法如下：

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, next, random):
        self.val = val
        self.next = next
        self.random = random
"""
class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        if not head:
            return None
        
        node_map = {}
        p = head
        while p:
            new_node = Node(p.val, None, None)
            node_map[p] = new_node
            p = p.next
        
        p = head
        q = copy_head = Node(0, None, None)
        while p:
            q.next = node_map[p]
            if p.random:
                q.next.random = node_map[p.random]
            p = p.next
            q = q.next
            
        return copy_head.next
```