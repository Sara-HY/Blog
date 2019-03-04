---
title: LeetCode_Symmetric Tree
date: 2019-03-04 10:34:09
categories: LeetCode
tags: 
  - easy
  - tree
  - dfs
  - bfs
---

## [Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).
（对称二叉树）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_101.png" width = "500" align=center/>
</div>

### 1. 递归
递归很常见，具体实现过程如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        def mirror(left, right):
            if not left and not right:
                return True
            if not left or not right:
                return False
            
            return left.val == right.val and mirror(left.left, right.right) and mirror(right.left, left.right)
        
        if not root:
            return True
       
        return mirror(root.left, root.right)
```

### 2. 迭代
维护两个队列或者栈，把左子树放入第一个队列（先放左子树），右子树放入第二个队列（先放右子树），每次取队首（栈顶）元素进行判断。（使用队列表示BFS，使用栈表示DFS）具体实现过程如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

# BFS
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        if not root:
            return True
       
        left_queue, right_queue = [root.left], [root.right]
        
        while len(left_queue) and len(right_queue):
            left_top = left_queue.pop()
            right_top = right_queue.pop()
            
            if not left_top and not right_top:
                continue
            if not left_top or not right_top:
                return False
            if left_top.val != right_top.val:
                return False
            
            left_queue.insert(0, left_top.left)
            left_queue.insert(0, left_top.right)
            right_queue.insert(0, right_top.right)
            right_queue.insert(0, right_top.left)
            
        return len(left_queue) == 0 and len(right_queue) == 0
```

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

# DFS
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        if not root:
            return True
       
        left_stack, right_stack = [root.left], [root.right]
        
        while len(left_stack) and len(right_stack):
            left_top = left_stack.pop()
            right_top = right_stack.pop()
            
            if not left_top and not right_top:
                continue
            if not left_top or not right_top:
                return False
            if left_top.val != right_top.val:
                return False
            
            left_stack.append(left_top.left)
            left_stack.append(left_top.right)
            right_stack.append(right_top.right)
            right_stack.append(right_top.left)
               
        return len(left_stack) == 0 and len(right_stack) == 0
```

