---
title: LeetCode_Binary Tree Maximum Path Sum
date: 2019-03-13 11:58:08
categories: LeetCode
tags: 
  - hard
  - tree
  - dfs
---

## [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

Given a non-empty binary tree, find the maximum path sum. For this problem, a path is defined as **any sequence of nodes** from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root. 
（二叉树最大路径和）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_124.png" width = "500" align=center/>
</div>

### 1. 递归
在二叉树中找一条路径，使得该路径的和最大。该路径可以从二叉树任何结点开始，也可以到任何结点结束。因此在递归求一条经过root的最大路径时，这条路径可能是：
1. 左边某条路径 + root + 右边某条路径
2. root + 左边某条路径
3. root + 右边某条路径
4. root
具体实现过程如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def helper(self, root):
        if not root:
            return 0
        
        max_path = root.val
        left_child = self.helper(root.left)
        right_child = self.helper(root.right)
        
        if left_child > 0:
            max_path += left_child
        
        if right_child > 0:
            max_path += right_child
        
        self.global_max = max(self.global_max, max_path)
        
        # 返回根节点、左子树到该节点、右子树到该节点三条路径的最大值（为保证与当前根节点的祖宗节点的连通性）
        return max(root.val, root.val+left_child, root.val+right_child)
    
    def maxPathSum(self, root: TreeNode) -> int:
        self.global_max = float('-inf')
        self.helper(root)
        return self.global_max
```