---
title: LeetCode_Same Tree
date: 2019-02-27 23:09:12
categories: LeetCode
tags: 
  - easy
  - tree
  - dfs
  - recursion
---

## [Same Tree](hhttps://leetcode.com/problems/same-tree/)

Given two binary trees, write a function to check if they are the same or not. Two binary trees are considered the same if they are structurally identical and the nodes have the same value.
（判断二叉树是否相同）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_100.png" width = "500" align=center/>
</div>

### 1. 递归
判断节点值，左子树，右子树是否一致，具体实现方法如下：

```python 
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if not p and not q:
            return True
        if not p or not q:
            return False
        if p.val != q.val:
            return False
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)

```