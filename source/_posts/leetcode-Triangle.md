---
title: LeetCode_Triangle
date: 2019-03-11 11:27:03
categories: LeetCode
tags: 
  - medium
  - array
  - dynamic programming
---

## [Triangle](https://leetcode.com/problems/triangle/)

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.
(计算三角矩阵的最短路径)

<!--more-->


**Example:**

<div align=center>
	<img src="/images/leetcode_120.png" width = "500" align=center/>
</div>

### 1. 动态规划
从上到下寻找最短路径，可以从下到上进行回溯。在向上回溯的过程中，动态规划的递归表达式为 

dp[j] = min(dp[j], dp[j+1]) + triangle[i][j] (因为是三角矩阵，所以从下到上的过程中只需要看 j 和 j+1 即可)

根据这个算法空间复杂度为 O(n)，具体实现过程如下：

```python
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        if not triangle:
            return 0
        
        n = len(triangle)
        dp = [0 for _ in range(n+1)]
           
        for i in range(n-1, -1, -1):
            for j in range(i+1):
                dp[j] = min(dp[j], dp[j+1]) + triangle[i][j]
         
        return dp[0]
```