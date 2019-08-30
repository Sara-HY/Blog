---
title: LeetCode_Split Array Largest Sum
date: 2019-08-29 21:44:50
categories: LeetCode
tags: 
  - hard
  - binary seach
  - dynamic programming
---

## [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/)

Given an array which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays. Write an algorithm to minimize the largest sum among these m subarrays.
（分割数组的最大值最小）

<!--more-->

**Note:**

If n is the length of array, assume the following constraints are satisfied:
- 1 ≤ n ≤ 1000
- 1 ≤ m ≤ min(50, n)


**Example:**

<div align=center>
	<img src="/images/leetcode_410.png" width = "500" align=center/>
</div>

### 1. 二分查找

首先设置 left = max(nums), right = sum(nums)。然后我们在 [left, right] 区间去查找最小的 \_sum ，根据 \_sum 去划分数组使得划分的子数组的数目小于等于 m ，具体实现过程如下：

```python
class Solution:
    def checkSplit(self, nums, m, maxSum): 
        if maxSum < max(nums):
            return False
        
        count, _sum = 1, 0
        for num in nums:
            _sum += num
            if _sum > maxSum:
                _sum = num
                count += 1
                if count > m:
                    return False
        return True
     
    def splitArray(self, nums: List[int], m: int) -> int:
        left = max(nums)
        right = sum(nums)
        
        while left < right:
            middle  = (left + right) // 2
            if self.checkSplit(nums, m, middle):
                right = middle
            else:
                left = middle + 1
            
        return left
```

### 2. 动态规划

二维动规：

数组dp：dp[i][j]表示将数组中**前i个数字**分成**j组**所能得到的最小的各个子数组中最大值。

递推公式：dp[i][j] = min(dp[i][j], max(dp[k][j-1], sums[i] - sums[k])。

其中dp[k][j-1]表示数组中**前k个数字分成j-1组**所能得到的最小的各个子数组中最大值，而**sums[i]-sums[k]**就是后面的数字之和，我们取二者之间的较大值；然后和dp[i][j]原有值进行对比，更新dp[i][j]为二者之中的较小值；这样k在[0,i-1]的范围内扫过一遍，dp[i][j]就能更新到最小值。棘突实现过程如下：
(Java 会 AC，Python 会 TLE)

```python
class Solution:
    def splitArray(self, nums: List[int], m: int) -> int:
        n = len(nums)
        
        _sums = [0 for _ in range(n+1)]
        for i in range(1, n+1):
            _sums[i] = _sums[i-1] + nums[i-1]
            
        dp = [[float('inf')]*(m+1) for _ in range(n+1)]
        dp[0][0] = 0
        
        for i in range(1, n+1):
            for j in range(1, m+1):
                for k in range(i):
                	dp[i][j] = min(dp[i][j], max(dp[k][j - 1], _sums[i] - _sums[k]))
       
        return dp[n][m]
```





















