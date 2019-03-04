---
title: LeetCode_Convert Sorted List to Binary Search Tree
date: 2019-03-04 20:44:50
categories: LeetCode
tags: 
  - easy
  - linked list
  - dfs
---

## [Convert Sorted List to Binary Search Tree](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/)

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST. For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
（将有序链表转换为平衡二叉树）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_109.png" width = "500" align=center/>
</div>

### 1. 递归
首先获得链表的长度，然后根据中序遍历的过程不断地建立二叉树，这是一种自底向上的方法。先递归构建左子树，一直到左叶子节点，左叶子节点对应的就是链表的第一个元素，生成左叶子节点之后移动链表当前指针。其时间复杂度为O(n), 具体实现过程如下：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def dfs(self, head, count):
            if count <= 0:
                return None
             
            left = self.dfs(head, count // 2)
            root = TreeNode(self.curNode.val)
            self.curNode = self.curNode.next
            right = self.dfs(self.curNode, count - count // 2 - 1)
            
            root.left = left
            root.right = right       
            return root 
        
    def sortedListToBST(self, head: ListNode) -> TreeNode:
        if not head:
            return None
        
        p = head
        count = 0
        while p:
            count += 1
            p = p.next
        
        self.curNode = head
        return self.dfs(head, count)
```

