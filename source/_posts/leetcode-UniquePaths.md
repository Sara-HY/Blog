---
title: LeetCode_Unique Paths
date: 2019-01-15 10:51:52
categories: LeetCode
tags: 
  - medium
  - array
  - dynamic programming
---

## [Unique Paths](https://leetcode.com/problems/unique-paths/)

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below). The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below). How many possible unique paths are there?
（不同的路径，只能向右或者向下移动从左上角移动到右下角的路径个数）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_62.png" width = "500" align=center/>
</div>

### 1. 动态规划

写出其动规表达式 dp[i][j] = dp[i-1][j] + dp[i][j-1] 即可，具体实现形式如下：

```python
class Solution:
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        dp = [[1]*n for _ in range(m)]

        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i-1][j] + dp[i][j-1]

        return dp[m-1][n-1]
```