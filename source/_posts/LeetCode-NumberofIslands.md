---
title: LeetCode_Number of Islands
date: 2019-05-11 11:16:11
categories: LeetCode
tags: 
  - medium
  - dfs
  - bfs
  - union find
---

## [Number of Islands](https://leetcode.com/problems/number-of-islands/)

Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.
（求岛屿的个数）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_200.png" width = "500" align=center/>
</div>


### 1. DFS遍历

```python
class Solution:
    def dfs(self, i, j):
        if 0 <= i < self.m and 0 <= j < self.n and self.grid[i][j] == '1':
            self.grid[i][j] = '0'
            self.dfs(i+1, j)
            self.dfs(i-1, j)
            self.dfs(i, j+1)
            self.dfs(i, j-1)
           
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid:
            return 0
        
        self.m, self.n = len(grid), len(grid[0])
        self.grid = grid
        
        count = 0
        for i in range(self.m):
            for j in range(self.n):
                if self.grid[i][j] == '1':
                    self.dfs(i, j)
                    count += 1
        return count
```