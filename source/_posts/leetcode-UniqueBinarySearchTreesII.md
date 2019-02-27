---
title: LeetCode_Unique Binary Search Trees II
date: 2019-02-27 15:55:13
categories: LeetCode
tags: 
  - medium
  - tree
  - recursion
  - dynamic programming
---

## [Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/)

Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1 ... n.
（构建二叉查找(排序)树）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_95.png" width = "500" align=center/>
</div>

### 1. 递归
递归的构建左子树 和 右子树，具体实现方法如下：

**Note:** 在start > end 的时候，不存在这样的子树。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def generateTrees(self, n: int) -> List[TreeNode]:
        def gen(start, end):
            if start > end:
                return [None]
            
            results = []
            for i in range(start, end+1):
                for l in gen(start, i-1):
                     for r in gen(i+1, end):
                            t = TreeNode(i)
                            t.left = l
                            t.right = r   
                            results.append(t)
            return results
        
        if n < 1:
            return []
       
        return gen(1, n)
```
