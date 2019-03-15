---
title: LeetCode_Binary Tree Postorder Traversal
date: 2019-03-15 14:52:48
categories: LeetCode
tags: 
  - hard
  - stack
  - tree
---

## [Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)

Given a binary tree, return the postorder traversal of its nodes' values.
（后序遍历二叉树）

<!--more-->

**Follow up:** Recursive solution is trivial, could you do it iteratively?

**Example:** 

<div align=center>
	<img src="/images/leetcode_145.png" width = "500" align=center/>
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
        
        self.helper(root.left, res)
        self.helper(root.right, res)
        res.append(root.val)
        
    def postorderTraversal(self, root):
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
由于先序遍历的顺序是根-左-右，后序遍历的顺序是左-右-根，因此可以修改先序遍历的遍历顺序为根-右-左，然后将最终结果倒序即可。具体实现方法如下：

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def postorderTraversal(self, root):
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
                stack.append(p.left)
                p = p.right
            else:
                p = stack.pop()
                
        return result[::-1]
```
