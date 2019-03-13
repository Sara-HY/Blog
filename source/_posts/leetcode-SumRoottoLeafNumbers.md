---
title: LeetCode_Sum Root to Leaf Numbers
date: 2019-03-13 22:12:21
categories: LeetCode
tags: 
  - medium
  - tree
  - dfs
---

## [Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/)

Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number. An example is the root-to-leaf path 1->2->3 which represents the number 123. Find the total sum of all root-to-leaf numbers.
（树型数值之和）

<!--more-->

**Note:** A leaf is a node with no children.


**Example:** 

<div align=center>
	<img src="/images/leetcode_129.png" width = "500" align=center/>
</div>

### 1. DFS
常规的 DFS 算法，具体实现过程如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def dfs(self, root):
        if not root:
            return
        
        left = self.dfs(root.left)
        right = self.dfs(root.right)
        
        if not left and not right:
            return str(root.val)
        
        result = []
        if left:
            for num in left:
                result.append(str(root.val)+str(num)) 
        if right:
            for num in right:
                result.append(str(root.val)+str(num))
        
        return result
        
    def sumNumbers(self, root: TreeNode) -> int:
        if not root:
            return 0
        
        nums = self.dfs(root)
        return  sum(int(num) for num in nums)
```