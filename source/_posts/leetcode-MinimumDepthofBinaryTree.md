---
title: LeetCode_Minimum Depth of Binary Tree
date: 2019-03-05 09:56:49
categories: LeetCode
tags: 
  - easy
  - tree
  - dfs
  - bfs
---

## [Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

Given a binary tree, find its minimum depth. The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node. Note: A leaf is a node with no children.
（二叉树的最低深度）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_111.png" width = "500" align=center/>
</div>

### 1. 递归

注意左（右）子树深度为0的地方，也就是当左（右）子树为空时，应该按照右（左）子树的深度计算。具体实现过程如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def minDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        
        left, right = self.minDepth(root.left), self.minDepth(root.right)
        if left == 0 or right == 0:
            return left + right + 1
        
        return min(left, right) + 1
```