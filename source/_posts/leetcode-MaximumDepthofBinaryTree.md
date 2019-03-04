---
title: LeetCode_Maximum Depth of Binary Tree
date: 2019-03-04 17:10:20
categories: LeetCode
tags: 
  - easy
  - tree
  - dfs
---

## [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

Given a binary tree, find its maximum depth. The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
（二叉树的深度）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_104.png" width = "500" align=center/>
</div>

### 1. 递归
找到左子树和右子树的最大深度，从而返回该深度+1即为结果。具体实现过程如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        
        max_depth = max(self.maxDepth(root.left), self.maxDepth(root.right))
        
        return max_depth + 1
```




