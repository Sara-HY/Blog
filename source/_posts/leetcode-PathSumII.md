---
title: LeetCode_Path Sum II
date: 2019-03-05 11:43:37
categories: LeetCode
tags: 
  - medium
  - tree
  - dfs
---

## [Path Sum II](https://leetcode.com/problems/path-sum-ii/)

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum. Note: A leaf is a node with no children.
（二叉树路径和并返回相应路径）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_113.png" width = "500" align=center/>
</div>

### 1. 递归
这道题是很清晰的递归的问题，需要注意的是节点的值可能是负值。具体实现方法如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
        def path_helper(head, path, sum):
            if sum == head.val and not head.left and not head.right:
                self.paths.append(path+[head.val])
                return
            
            if head.left:
                path_helper(head.left, path+[head.val], sum-head.val)
            if head.right:
                path_helper(head.right, path+[head.val], sum-head.val)
                  
        if not root:
            return []
        
        self.paths = []
        path_helper(root, [], sum)
        
        return self.paths
```






