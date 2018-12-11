---
title: LeetCode_Merge k Sorted Lists
date: 2018-12-11 22:34:00
categories: LeetCode
tags: 
  - hard
  - linked list
  - heap
  - divide and conquer
---

## [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.
（合并k个有序链表）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_23.png" width = "500" align=center/>
</div>

### 1. 分治法
这个问题是一个典型的分治法解决的问题。其时间复杂度为 \\(O(mlog(n))\\)，其中 \\(n\\) 为序列个数，\\(m\\) 为所有序列的长度和。具体实现过程如下：

```python
class Solution:
    def merge2Lists(self, left, right):
        head = ListNode(0)
        p = left
        q = right
        tail = head
        
        while p != None and q != None:
            if p.val < q.val:
                tail.next = p
                p = p.next
            else:
                tail.next = q
                q = q.next
            tail = tail.next
        
        if p != None:
            tail.next = p
        else:
            tail.next = q
            
        return head.next
        
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        n = len(lists)
        if n == 0:
            return []
        if n == 1:
            return lists[0]
        
        left_list = self.mergeKLists(lists[:n//2])
        right_list = self.mergeKLists(lists[n//2:])
        return self.merge2Lists(left_list, right_list)
```


### 2. 堆排序
另外一种方式是遍历所有的链表，并用堆保存并排序，然后根据堆构建最终的链表。其时间复杂度为 \\(O(mlog(n))\\)，其中 \\(n\\) 为序列个数，\\(m\\) 为所有序列的长度和。具体实现过程如下：

```python
from heapq import heappush, heappop

class Solution:      
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        if lists == []:
            return []
        
        heap = []
        for list in lists:
            while list:
                heappush(heap, list.val)
                list = list.next
       
        head = ListNode(0)
        tail = head
        while heap:
            tail.next = ListNode(heappop(heap))
            tail = tail.next
        
        return head.next
```











