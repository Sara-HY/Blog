---
title: LeetCode_Populating Next Right Pointers in Each Node II
date: 2019-03-06 15:19:05
categories: LeetCode
tags: 
  - medium
  - tree
  - dfs
---

## [Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)

Given a binary tree, Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL. Initially, all next pointers are set to NULL.
（连接二叉树同一层的结点）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_117.png" width = "500" align=center/>
</div>

### 1. 递归
首先根据根节点的 next 指针找到这个子树的孩子节点的 next 需要连接的位置，然后将孩子节点通过 next 连接起来，再处理子树部分。具体实现过程如下：

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
        
        p = root.next
        while p:
            if p.left:
                p = p.left
                break
            if p.right:
                p = p.right
                break
            p = p.next
        
        if root.right:
            root.right.next = p
        if root.left:
            if root.right:
                root.left.next = root.right
            else:
                root.left.next = p
        
        self.connect(root.right)
        self.connect(root.left)
            
        return root
```


### 2. 迭代
根据 BFS 进行层次遍历，具体实现过程如下：

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
            return None
    
        queue = [[root]]
    
        while queue:
            top = queue.pop()
            level_node = []
            
            pre = None
            for node in top:
                if node.left:
                    level_node.append(node.left)
                    if not pre:
                        pre = node.left
                    else:
                        pre.next = node.left
                        pre = node.left
                if node.right:
                    level_node.append(node.right)
                    if not pre:
                        pre = node.right
                    else:
                        pre.next = node.right
                        pre = node.right
            if level_node:
                queue.insert(0, level_node)        
        
        return root
```