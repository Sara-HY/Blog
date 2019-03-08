---
title: LeetCode_Populating Next Right Pointers in Each Node
date: 2019-03-05 20:58:21
categories: LeetCode
tags: 
  - medium
  - tree
  - dfs
---

## [Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL. Initially, all next pointers are set to NULL.
（连接完全二叉树同一层的结点）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_116.png" width = "500" align=center/>
</div>

### 1. 递归
在递归的过程中需要考虑左、右子树，兄弟结点之间的连接。具体实现过程如下：

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, left, right, next):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""
class Solution:
    def connect(self, root: 'Node') -> 'Node':
        if not root or not root.left:
            return root
        
        # 左、右子树的连接
        if root.left and root.right:
            root.left.next = root.right
        
        # 兄弟节点的连接
        if root.next and root.right:
            root.right.next = root.next.left
            
        self.connect(root.left)
        self.connect(root.right)

        return root
```

### 2. 迭代
由于在递归的过程中会使用到栈，因此空间复杂度为 O(log(n))，为了实现空间复杂度为 O(1)，使用迭代的方法，具体实现过程如下：

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, left, right, next):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""
class Solution:
    def connect(self, root: 'Node') -> 'Node':
        if not root:
            return root
        
        p_start = root
        while p_start.left:
            p_cur = p_start
            while p_cur:
                p_cur.left.next = p_cur.right
                if p_cur.next:
                    p_cur.right.next = p_cur.next.left
                p_cur = p_cur.next
            
            p_start = p_start.left
            
        return root
```

