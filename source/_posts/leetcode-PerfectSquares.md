---
title: Leetcode_Perfect Squares
date: 2019-06-30 22:10:32
categories: LeetCode
tags: 
  - medium
  - math
  - dynamic programming
  - bfs
---

## [Perfect Squares](https://leetcode.com/problems/perfect-squares/)

Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.
（将一个正整数分为干个平方数的和，使得平方数个数最少）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_279.png" width = "500" align=center/>
</div>

### 1. BFS

```python
class Solution:
    def numSquares(self, n: int) -> int:
        queue = [n]
        count = 0
        while queue:
            tmp = []
            count += 1
            for q in queue:
                i = 1
                while i*i <= q:
                    v = q - i*i
                    if v == 0:
                        return count
                    tmp.append(v)
                    i += 1
            queue = tmp
```


### 2. 动态规划

```python
class Solution:
    def numSquares(self, n: int) -> int:
        dp = [1] + [0]*n
        for i in range(int(n**0.5), 0, -1):
            s = i**2
            for j in range(len(dp)):
                if dp[j] and j+s < len(dp) and not 0 < dp[j+s] < dp[j] + 1:
                    dp[j+s] = dp[j]+1
                    
        return dp[-1] - 1

```