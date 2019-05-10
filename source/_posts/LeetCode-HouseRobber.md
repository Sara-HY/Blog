---
title: LeetCode_House Robber
date: 2019-05-10 22:24:17
categories: LeetCode
tags: 
  - easy
  - dynamic programming
---

## [House Robber](https://leetcode.com/problems/house-robber/)

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police (the robber list cannot be adjacent).
（数组中不相邻数组成的和最大）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_198.png" width = "500" align=center/>
</div>


### 1. 动态规划
为了保证不存在相邻的数，可以维护两个变量表示a_(n-2) 和 a_(n-1)，于是就有`a_n = max(a_(n-2) + nums[n], a_(n-1))`。具体实现过程如下：

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        before_before, before = 0, 0
        
        for i in range(len(nums)):
            temp = before
            before = max(before_before + nums[i], before)
            before_before = temp
                
        return max(before_before, before)
```