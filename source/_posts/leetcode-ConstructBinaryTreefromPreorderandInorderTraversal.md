---
title: LeetCode_Construct Binary Tree from Preorder and Inorder Traversal
date: 2019-03-04 17:19:19
categories: LeetCode
tags: 
  - medium
  - array
  - tree
  - dfs
---

## [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

Given preorder and inorder traversal of a tree, construct the binary tree.
（根据先序遍历和中序遍历构建二叉树）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_105.png" width = "500" align=center/>
</div>

### 1. 递归
递归构建二叉树，首先根据先序遍历确定根节点，在根据中序遍历定位到根节点。其中，中序遍历根节点左边的为左子树，右边的为右子树。具体实现过程如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        if not preorder:
            return None
        
        root = TreeNode(preorder[0])
        index = inorder.index(preorder[0])
        
        root.left = self.buildTree(preorder[1:index+1], inorder[:index])
        root.right = self.buildTree(preorder[index+1:], inorder[index+1:])
        
        return root
```

