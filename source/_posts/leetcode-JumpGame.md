---
title: LeetCode_Jump Game
date: 2019-01-10 21:15:56
categories: LeetCode
tags: 
  - medium
  - array
  - greedy
---

## [Jump Game](https://leetcode.com/problems/jump-game/)

Given an array of non-negative integers, you are initially positioned at the first index of the array. Each element in the array represents your maximum jump length at that position. Determine if you are able to reach the last index.
(跳棋游戏，确定能否到达队尾)

<!--more-->

**Example:**
<div align=center>
	<img src="/images/leetcode_55.png" width = "500" align=center/>
</div>


### 1. 贪心算法
遍历数组，求得可到达的最远 index。若index > n-1，则可以到达最后。具体实现方法如下：

```python
class Solution:
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        max_index = 0
        n = len(nums)
        if n <= 1:
            return True
        
        for i in range(n-1):
            if max_index >= i:
                max_index = max(max_index, i + nums[i])
            if max_index >= n-1:
                return True 
        return False
```