---
title: LeetCode_Convert Sorted Array to Binary Search Tree
date: 2019-03-04 17:52:56
categories: LeetCode
tags: 
  - easy
  - tree
  - dfs
---

## [Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

Given an array where elements are sorted in ascending order, convert it to a height balanced BST. For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
（将有序数组转换为平衡二叉树）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_108.png" width = "500" align=center/>
</div>

### 1. 递归
根据平衡二叉树的定义：height差不大于1。因此从中间开始建立为根节点，左边的有序数组构建左子树，右边的有序数组构建右子树。具体实现过程如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        if not nums:
            return None
        
        n = len(nums)
        root = TreeNode(nums[n//2])
        root.left = self.sortedArrayToBST(nums[:n//2])
        root.right = self.sortedArrayToBST(nums[n//2+1:])
        
        return root
```