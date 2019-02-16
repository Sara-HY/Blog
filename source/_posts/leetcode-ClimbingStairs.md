---
title: LeetCode_Climbing Stairs
date: 2019-02-16 19:14:45
categories: LeetCode
tags: 
  - easy
  - dynamic programming
---

## [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

You are climbing a stair case. It takes n steps to reach to the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top? (Note: Given n will be a positive integer.)
（爬楼梯问题）

<!--more-->

**Example:**

<div align=center>
	<img src="/images/leetcode_70.png" width = "500" align=center/>
</div>

### 1. 动态规划

```python
class Solution:
    def climbStairs(self, n: 'int') -> 'int':
        dp = [1 for _ in range(n+1)]

        for i in range(2, n+1):
            dp[i] = dp[i-1] + dp[i-2]

        return dp[n]
```
