---
title: LeetCode_Flatten Binary Tree to Linked List
date: 2019-03-05 15:11:06
categories: LeetCode
tags: 
  - medium
  - tree
  - dfs
---

## [Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)

Given a binary tree, flatten it to a linked list in-place.
（压平二叉树）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_114.png" width = "500" align=center/>
</div>

### 1. 递归
递归压平子树，然后将左子树放在右子树上，**并将左子树置为None**。然后找到叶子节点将原来的右子树连接在后面。具体实现过程如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def flatten(self, root: TreeNode) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        if not root:
            return
        
        if root.left:
            self.flatten(root.left)
        if root.right:
            self.flatten(root.right)
        
        # move the left tree to the right, set left to None 
        p_temp = root.right
        root.right = root.left
        root.left = None
        
        # find the leaf and link the right tree
        p_tail = root
        while p_tail.right:
            p_tail = p_tail.right
        p_tail.right = p_temp
        
        return
```