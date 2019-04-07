---
title: Leetcode_Binary Search Tree Iterator
date: 2019-04-07 17:20:50
categories: LeetCode
tags: 
  - medium
  - stack
  - tree
  - design
---

## [Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/)

Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST. Calling next() will return the next smallest number in the BST.
（设计二叉搜索树的迭代器）

<!--more-->

**Note:**
1. next() and hasNext() should run in average O(1) time and uses O(h) memory, where h is the height of the tree.
2. You may assume that next() call will always be valid, that is, there will be at least a next smallest number in the BST when next() is called.


**Example:** 


<div align=center>
	<img src="/images/leetcode_173.png" width = "500" align=center/>
</div>

### 1. 中序遍历 & 栈
这道题主要考察的是二叉树的**中序遍历**的非递归形式，用中序遍历即可从小到大取出所有节点，但是需要额外定义一个栈来存储从根节点到左子树所有的左孩子结点。在不断迭代的过程中，不断地pop栈顶并实时将右结点push进去。具体实现过程如下：


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class BSTIterator:
    def __init__(self, root: TreeNode):
        self.stack = []
        self.push_left(root)

    def next(self) -> int:
        """
        @return the next smallest number
        """
        node = self.stack.pop()
        self.push_left(node.right)
        return node.val

    def hasNext(self) -> bool:
        """
        @return whether we have a next smallest number
        """
        return bool(self.stack)
        
    def push_left(self, root):
        while root:
            self.stack.append(root)
            root = root.left

# Your BSTIterator object will be instantiated and called as such:
# obj = BSTIterator(root)
# param_1 = obj.next()
# param_2 = obj.hasNext()
```