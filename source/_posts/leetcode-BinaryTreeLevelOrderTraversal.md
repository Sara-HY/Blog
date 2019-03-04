---
title: LeetCode_Binary Tree Level Order Traversal
date: 2019-03-04 15:00:13
categories: LeetCode
tags: 
  - medium
  - tree
  - bfs
---

## [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).
（按层遍历二叉树）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_102.png" width = "500" align=center/>
</div>

### 1. 递归
按层遍历，每次都吧同层的树节点 Node 组合成一个 List 输入到队列。（变形之后的BFS）。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []
        
        results = [[root.val]]
        
        queue = []
        queue.append([root])
        while len(queue):
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
                queue.insert(0, level_node)
                results.append(result)
           
        return results
```


