---
title: LeetCode_Convert Binary Search Tree to Sorted Doubly Linked List
date: 2019-08-20 15:29:55
categories: LeetCode
tags: 
  - medium
  - tree
  - linked list
---

## Convert Binary Search Tree to Sorted Doubly Linked List

Convert a BST to a sorted circular doubly-linked list **in-place**. Think of the left and right pointers as synonymous to the previous and next pointers in a doubly-linked list.
（将二叉搜索树转换为一个有序的双向链表）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_426.png" width = "500" align=center/>
</div>


### 1. 中序遍历
首先对二叉树进行中序遍历，将遍历后的结果进行指针调整，时间复杂度为O(n)，空间复杂度为O(n)。具体实现过程如下：

```python
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    def in_order(self, root):
        if not root:
            return
        self.in_order(root.left)
        self.list.append(root)
        self.in_order(root.right)
        
    def Convert(self, pRootOfTree):
        if not pRootOfTree:
            return 
        self.list = []
        self.in_order(pRootOfTree)
        
        for i, node in enumerate(self.list[:-1]):
            node.right = self.list[i + 1]
            self.list[i + 1].left = node
        return self.list[0]
```

### 2. 中序遍历
在对二叉树进行中序遍历时进行指针调整，时间复杂度为O(n)，空间复杂度为O(1)。具体实现过程如下：

```python
# -*- coding:utf-8 -*-
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    def __init__(self):
        self.listHead = None
        self.listTail = None
        
    def Convert(self, pRootOfTree):
        if pRootOfTree==None:
            return
        self.Convert(pRootOfTree.left)
        if self.listHead==None:
            self.listHead = pRootOfTree
            self.listTail = pRootOfTree
        else:
            self.listTail.right = pRootOfTree
            pRootOfTree.left = self.listTail
            self.listTail = pRootOfTree
        self.Convert(pRootOfTree.right)
        return self.listHead
```

