---
title: LeetCode_Construct Binary Tree from Inorder and Postorder Traversal
date: 2019-03-04 17:38:13
categories: LeetCode
tags: 
  - medium
  - array
  - tree
  - dfs
---

## [Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

Given inorder and postorder traversal of a tree, construct the binary tree.
（根据中序遍历和后序遍历构建二叉树）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_106.png" width = "500" align=center/>
</div>

### 1. 递归
递归构建二叉树，首先根据后序遍历确定根节点，在根据中序遍历定位到根节点。其中，中序遍历根节点左边的为左子树，右边的为右子树。具体实现过程如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def buildTree(self, inorder: List[int], postorder: List[int]) -> TreeNode:
        if not inorder:
            return None
        
        root = TreeNode(postorder[-1])
        index = inorder.index(postorder[-1])
        
        root.left = self.buildTree(inorder[:index], postorder[:index])
        root.right = self.buildTree(inorder[index+1:], postorder[index:-1])
        
        return root
```

