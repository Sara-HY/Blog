---
title: LeetCode_Surrounded Regions
date: 2019-03-13 22:21:20
categories: LeetCode
tags: 
  - medium
  - bfs
  - dfs
  - union find
---

## [Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)

Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'. A region is captured by flipping all 'O's into 'X's in that surrounded region.
（包围区域）

<!--more-->

**Note:** Surrounded regions shouldn’t be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.

**Example:** 

<div align=center>
	<img src="/images/leetcode_130.png" width = "500" align=center/>
</div>

根据题中的意思，也就是矩阵中边界出向联通的 'O' 不会被修改为 'X'，其他的会修改为 'X'，下面使用基于图的 DFS 、BFS、Union Find 三种方法实现。都是先将与边界 'O' 联通的置位 '\*', 其他的会修改为 'X'，然后再将 '\*' 修改为 'O'。

### 1. DFS
发现有问题先放入栈中，出栈时处理，具体实现过程如下：

```python
class Solution:
    def dfs(self, board, i, j):
        if board[i][j] != 'O':
            return
        
        stack = [(i, j)]
        while stack:
            node_i, node_j = stack.pop()
            board[node_i][node_j] = '*'
            
            if node_i-1 >= 0 and board[node_i-1][node_j] == 'O':
                stack.append((node_i-1, node_j))
            if node_i+1 < self.m and board[node_i+1][node_j] == 'O':
                stack.append((node_i+1, node_j))
            if node_j-1 >= 0 and board[node_i][node_j-1] == 'O':
                stack.append((node_i, node_j-1))
            if node_j+1 < self.n and board[node_i][node_j+1] == 'O':
                stack.append((node_i, node_j+1))         
        return
           
   
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        if not board or not board[0]:
            return
        
        self.m, self.n = len(board), len(board[0])
        
        for i in range(self.m):
            self.dfs(board, i, 0)
            self.dfs(board, i, self.n-1)
        
        for j in range(self.n):
            self.dfs(board, 0, j)
            self.dfs(board, self.m-1, j)
            
        for i in range(self.m):        
            for j in range(self.n):
                if board[i][j] == '*':
                    board[i][j] = 'O'
                elif board[i][j] == 'O':
                    board[i][j] = 'X'
        return
```

### 2. BFS
发现有问题立马处理，否则会Time Limit Exceeded，具体实现过程如下：

```python
class Solution:
    def bfs(self, board, i, j):
        if board[i][j] != 'O':
            return
        
        queue = [(i, j)]
        board[i][j] = '*'
        while queue:
            node_i, node_j = queue.pop(0)
        
            if node_i-1 >= 0 and board[node_i-1][node_j] == 'O':
                queue.append((node_i-1, node_j))
                board[node_i-1][node_j] = '*'
            if node_i+1 < self.m and board[node_i+1][node_j] == 'O':
                queue.append((node_i+1, node_j))
                board[node_i+1][node_j] = '*'
            if node_j-1 >= 0 and board[node_i][node_j-1] == 'O':
                queue.append((node_i, node_j-1))
                board[node_i][node_j-1] = '*'
            if node_j+1 < self.n and board[node_i][node_j+1] == 'O':
                queue.append((node_i, node_j+1)) 
                board[node_i][node_j+1] = '*'
        return
   
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        if not board or not board[0]:
            return
        
        self.m, self.n = len(board), len(board[0])
        
        for i in range(self.m):
            self.bfs(board, i, 0)
            self.bfs(board, i, self.n-1)
        
        for j in range(self.n):
            self.bfs(board, 0, j)
            self.bfs(board, self.m-1, j)
            
        for i in range(self.m):        
            for j in range(self.n):
                if board[i][j] == '*':
                    board[i][j] = 'O'
                elif board[i][j] == 'O':
                    board[i][j] = 'X'
        return 
```