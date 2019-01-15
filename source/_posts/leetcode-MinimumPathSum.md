---
title: LeetCode_Minimum Path Sum
date: 2019-01-15 14:06:43
categories: LeetCode
tags: 
  - medium
  - array
  - dynamic programming
---

## [Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)

Given a **m x n** grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path. You can only move either down or right at any point in time.
（最小带权路径和，只能向右或者向下移动从左上角移动到右下角的带权路径和）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_64.png" width = "500" align=center/>
</div>

### 1. 动态规划

在前两道题目的基础上，类似于求一个带权路径和的问题。具体实现过程如下：

```python
class Solution:
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        m, n = len(grid), len(grid[0])

        dp = [[0]*n for _ in range(m)]

        dp[0][0] = grid[0][0]
        for i in range(m):
            for j in range(n):
                if i==0 and j>0:
                    dp[i][j] = dp[i][j-1] + grid[i][j]
                elif j==0 and i>0:
                    dp[i][j] = dp[i-1][j] + grid[i][j]
                elif i>0 and j>0:
                    dp[i][j] = min(dp[i][j-1], dp[i-1][j]) + grid[i][j]

        return dp[m-1][n-1]
```