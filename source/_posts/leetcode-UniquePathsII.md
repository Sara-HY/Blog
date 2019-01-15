---
title: LeetCode_Unique Paths II
date: 2019-01-15 11:26:34
categories: LeetCode
tags: 
  - medium
  - array
  - dynamic programming
---

## [Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below). The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below). Now consider if some **obstacles** are added to the grids. How many unique paths would there be?
（不同的路径II，只能向右或者向下移动在有路障的情况下从左上角移动到右下角的路径个数）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_62.png" width = "500" align=center/>
</div>

### 1. 动态规划

写出其动规表达式 dp[i][j] = dp[i-1][j] + dp[i][j-1]。但是需要另外考虑：
1. 遇到路障时，dp[i][j] = 0，继续扫描。
2. 由于从左上角开始扫描，在扫描第一行时：dp[i][j] = dp[i][j-1]。
3. 在扫描第一列时：dp[i][j] = dp[i-1][j] 。

具体实现形式如下：

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        """
        m, n = len(obstacleGrid), len(obstacleGrid[0])

        dp = [[1]*n for _ in range(m)]

        for i in range(m):
            for j in range(n):
                if obstacleGrid[i][j] == 1:
                    dp[i][j] = 0
                    continue
                if i == 0 and j > 0:
                    dp[i][j] = dp[i][j-1]
                elif j == 0 and i > 0:
       		        dp[i][j] = dp[i-1][j]
                elif i > 0 and j > 0:
                    dp[i][j] = dp[i][j-1] + dp[i-1][j]
                    
        return dp[m-1][n-1]
```