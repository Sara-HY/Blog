---
title: LeetCode_Binary Tree Preorder Traversal
date: 2019-03-15 14:22:32
categories: LeetCode
tags: 
  - medium
  - stack
  - tree
---

## [Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)

Given a binary tree, return the preorder traversal of its nodes' values.
（先序遍历二叉树）

<!--more-->

**Follow up:** Recursive solution is trivial, could you do it iteratively?

**Example:** 

<div align=center>
	<img src="/images/leetcode_94.png" width = "500" align=center/>
</div>

### 1. 递归
具体实现方法如下：

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def helper(self, root, res):
        if not root:
            return res
        res.append(root.val)
        self.helper(root.left, res)
        self.helper(root.right, res)
        
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if not root:
            return []
        
        result = []
        self.helper(root, result)
        
        return result
```

### 2. 迭代 & 栈
先将访问根节点，然后将右子树节点加入到栈中，然后访问左子树。具体实现方法如下：

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if not root:
            return []
        
        result, stack = [], []
        p = root
        while stack or p:
            if p:
                result.append(p.val)
                stack.append(p.right)
                p = p.left
            else:
                p = stack.pop()
        
        return result
```
