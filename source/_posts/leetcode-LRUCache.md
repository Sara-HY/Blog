---
title: LeetCode_LRU Cache
date: 2019-03-15 15:01:34
categories: LeetCode
tags: 
  - hard
  - design
---

## [LRU Cache](https://leetcode.com/problems/lru-cache/)

Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.
 - get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
 - put(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

（设计LRU算法的数据结构）

<!--more-->

**Follow up:** Could you do both operations in O(1) time complexity?

**Example:** 

<div align=center>
	<img src="/images/leetcode_146.png" width = "500" align=center/>
</div>

### 1. 哈希表 + 双向链表
这里使用哈希表和双向链表来构造 LRU 算法的数据结构，哈希表根据 key 可以直接索引到链表中相应的节点，可以实现时间复杂度是 O(1)。具体实现方法如下：

**Note:**
1. 在进行 get/put 操作之后，需要重新将该节点移到队首。
2. 双向链表方便进行队首插入新节点，队尾删除纠结点的操作。

```python
class Node:
    def __init__(self, k, v, prev, next):
        self.key = k
        self.val = v
        self.prev = prev
        self.next = next

class LRUCache(object):
    def __init__(self, capacity):
        """
        :type capacity: int
        """
        self.capacity = capacity
        self.cached = {}
        self.head = Node(0, 0, None, None)
        self.tail = Node(0, 0, None, None)
        self.head.next = self.tail
        self.tail.prev = self.head
        
    def add(self, node):
        node.next = self.head.next
        self.head.next.prev = node
        self.head.next = node
        node.prev = self.head
        self.cached[node.key] = node
    
    def remove(self, node):
        node.prev.next = node.next
        node.next.prev = node.prev
        del self.cached[node.key]
        del node
        
    def get(self, key):
        """
        :type key: int
        :rtype: int
        """
        if key in self.cached:
            value = self.cached[key].val
            self.remove(self.cached[key])
            self.add(Node(key, value, None, None))
            return value
        else:
            return -1
        
    def put(self, key, value):
        """
        :type key: int
        :type value: int
        :rtype: None
        """
        if key in self.cached:
            self.remove(self.cached[key])    
        self.add(Node(key, value, None, None))   
        if len(self.cached) > self.capacity:
            del self.cached[self.tail.prev.key]
            self.tail = self.tail.prev
            del self.tail.next
```