---
title: LeetCode_Balanced Binary Tree
date: 2019-03-04 21:16:49
categories: LeetCode
tags: 
  - easy
  - tree
  - dfs
---

## [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

Given a binary tree, determine if it is height-balanced. For this problem, a height-balanced binary tree is defined as: a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
（判断是否是平衡二叉树）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_110.png" width = "500" align=center/>
</div>

### 1. 递归

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        def depth(root):
            if not root:
                return 0
            return 1 + max(depth(root.left), depth(root.right))
        
        if not root:
            return True
        
        if abs(depth(root.left) - depth(root.right)) > 1:
            return False
        
        return self.isBalanced(root.left) and self.isBalanced(root.right) 
```