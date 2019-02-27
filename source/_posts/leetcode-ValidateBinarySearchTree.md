---
title: LeetCode_Validate Binary Search Tree
date: 2019-02-27 21:10:27
categories: LeetCode
tags: 
  - medium
  - tree
  - dfs
---

## [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

Given a binary tree, determine if it is a valid binary search tree (BST).
（判断是否为二叉排序树）

Assume a BST is defined as follows:
1. The left subtree of a node contains only nodes with keys less than the node's key.
2. The right subtree of a node contains only nodes with keys greater than the node's key.
3. Both the left and right subtrees must also be binary search trees.

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_98.png" width = "500" align=center/>
</div>


### 1. 递归
需要注意的是，在判断子树是否为二叉排序树时，我们需要考虑子树上的节点都小于（或大于）根节点，因此需要传入阈值。具体实现方法如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        def _isValidBST(root, _min=float('-inf'), _max=float('inf')):
            if not root:
                return True

            if root.val <= _min or root.val >= _max:
                return False

            return _isValidBST(root.left, _min, root.val) and \
                    _isValidBST(root.right, root.val, _max)

        return _isValidBST(root)
```

### 2. DFS & Inorder（中序遍历）
首先对二叉树进行中序遍历，然后对遍历的结果判断是否是一个完全递增的序列（不可相等），具体实现方法如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution: 
    def isValidBST(self, root: TreeNode) -> bool:
        def dfs(root):
            if not root:
                return
            dfs(root.left)
            self.travel.append(root.val)
            dfs(root.right)
                
        self.travel = []
        dfs(root)

        for i in range(len(self.travel) - 1):
            if self.travel[i+1] <= self.travel[i]:
                return False
        
        return True
```
