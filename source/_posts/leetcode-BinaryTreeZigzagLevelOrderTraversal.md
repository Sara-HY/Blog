---
title: LeetCode_Binary Tree Zigzag Level Order Traversal
date: 2019-03-04 15:53:15
categories: LeetCode
tags: 
  - medium
  - stack
  - tree
  - bfs
---

## [Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).（按层从左到右->从右到左遍历二叉树）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_103.png" width = "500" align=center/>
</div>

### 1. 递归
与上一题类似，按层遍历，每次都把同层的树节点 Node 组合成一个 List 输入到队列，并在偶数行翻转（变形之后的BFS）。


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []
        
        results = [[root.val]]
        queue = [[root]]
        
        reverse_flag = 1
        while len(queue) > 0:
            top = queue.pop()
            
            result = []
            level_node = []

            for node in top:
                if node.left:
                    level_node.append(node.left)
                    result.append(node.left.val)
                if node.right:
                    level_node.append(node.right)
                    result.append(node.right.val)
        
            if result:
                if reverse_flag:
                    result.reverse()
    
                reverse_flag = 1 - reverse_flag
                queue.insert(0, level_node)
                results.append(result)
            
        return results
```



