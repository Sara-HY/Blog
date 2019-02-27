---
title: LeetCode_Recover Binary Search Tree
date: 2019-02-27 22:22:04
categories: LeetCode
tags: 
  - hard
  - tree
  - dfs
---

## [Recover Binary Search Tree](https://leetcode.com/problems/recover-binary-search-tree/)

Two elements of a binary search tree (BST) are swapped by mistake. Recover the tree without changing its structure.
（复原二叉排序树）

<!--more-->

**Follow Up:** A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?

**Example:** 

<div align=center>
	<img src="/images/leetcode_99.png" width = "500" align=center/>
</div>

### 1. 中序遍历 & 树->数组
中序遍历二叉树，保存所有的节点到数组；然后遍历数组查找不符合要求的节点指针，空间复杂度为 O(n)。具体实现方法如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def recoverTree(self, root: TreeNode) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        def treelist(root):
            if not root:
                return
            treelist(root.left)
            tree_list.append(root)
            treelist(root.right)
            
        tree_list = []
        treelist(root)
        
        first_node, second_node = None, None
        for i in range(len(tree_list) - 1):
            if tree_list[i+1].val <= tree_list[i].val:
                if not first_node:
                    first_node = tree_list[i]
                    second_node = tree_list[i+1]
                else:
                    second_node = tree_list[i+1]          

        first_node.val, second_node.val = second_node.val, first_node.val
```

### 2. 中序遍历 
题中的 Follow Up 提及最好是空间复杂度为 O(1)，因此在中序遍历的过程中需要同时找出不符合要求的节点指针。具体实现方法如下：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def recoverTree(self, root: TreeNode) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        def dfs(root):
            if not root:
                return
            
            dfs(root.left)
            
            if self.prev and self.prev.val >= root.val and self.first_node == None:
                self.first_node = self.prev
            if self.prev and self.prev.val >= root.val and self.first_node != None:
                self.second_node = root
            self.prev = root
            
            dfs(root.right)
        
        self.prev = None
        self.first_node = None
        self.second_node = None
        
        dfs(root)
        self.first_node.val, self.second_node.val = self.second_node.val, self.first_node.val
```
