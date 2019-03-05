---
title: LeetCode_Path Sum
date: 2019-03-05 10:16:53
categories: LeetCode
tags: 
  - easy
  - tree
  - dfs
---

## [Path Sum](https://leetcode.com/problems/path-sum/)

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum. Note: A leaf is a node with no children.
（二叉树路径和）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_112.png" width = "500" align=center/>
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
    def hasPathSum(self, root: TreeNode, sum: int) -> bool:
        if not root:
            return False
        
        # must be leaf 
        if root.val == sum and not root.left and not root.right:
            return True
        
        return self.hasPathSum(root.left, sum-root.val) or self.hasPathSum(root.right, sum-root.val)
```