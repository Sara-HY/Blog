---
title: LeetCode_Binary Tree Inorder Traversal
date: 2019-02-27 12:14:02
categories: LeetCode
tags: 
  - medium
  - hash table
  - stack
  - tree
---

## [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

Given a binary tree, return the inorder traversal of its nodes' values.
（中序遍历二叉树）

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
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def inorder(self, tree):
        if not tree:
            return
        if tree.left:
            self.inorder(tree.left)
        self.results.append(tree.val)
        if tree.right:
            self.inorder(tree.right)
    
    def inorderTraversal(self, root: TreeNode) -> List[int]:   
        if not root:
            return []
        self.results = []
        self.inorder(root)
        
        return self.results
```

### 2. 迭代 & 栈
不断将左子树加入到栈中，然后访问依次访问，最后再访问右子树。具体实现方法如下：
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:   
        if not root:
            return []
        results = []
        stack = []
        
        p = root
        while stack or p:
            while p:
                stack.append(p)
                p = p.left
            p = stack.pop()
            results.append(p.val)
            p = p.right
            
        return results
```