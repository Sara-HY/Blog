---
title: LeetCode_Binary Tree Right Side View
date: 2019-05-11 09:41:50
categories: LeetCode
tags: 
  - medium
  - tree
  - dfs
  - bfs
---

## [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)

Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.
（二叉树的右视图）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_199.png" width = "500" align=center/>
</div>


### 1. BFS按层遍历

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        if not root:
            return []
       
        result = []
        stack = [root]
        while stack:
            result.append(stack[0].val)
            new_stack = []
            for node in stack:
                if node.right:
                    new_stack.append(node.right)
                if node.left:
                    new_stack.append(node.left)
            stack = new_stack
        
        return result 
```






