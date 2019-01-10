---
title: LeetCode_Maximum Subarray
date: 2019-01-09 22:16:20
categories: LeetCode
tags: 
  - easy
  - array
  - divide and conquer
  - dynamic programming
---

## [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
(数组连续子串的和最大)

<!--more-->

**Follow up:**

If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

**Example:**

<div align=center>
	<img src="/images/leetcode_53.png" width = "500" align=center/>
</div>

### 1. 动态规划

这个题目写出动规表达式就很容易得到具体的解法：dp[i+1] = max(dp[i]+nums[i+1], nums[i+1])。具体的解法如下：

```python
class Solution:
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        dp = [nums[0] for _ in range(n)]
        
        for i in range(1, n):
	        dp[i] = max(dp[i-1] + nums[i], nums[i])

        return max(dp)
```

### 2. 分治法

题中要求使用分治法来解决这个问题，我们可以分 3 类情况来讨论。对于一个数组 nums 的 [left, right]子串，其中点为 mid = (left + right) // 2，
1. 答案序列完全在[left, mid - 1]中；
2. 答案序列完全在[mid + 1, right]中；
3. 答案序列为包含 mid 的左右延续的序列。

```python
class Solution:
    def divide(self, left, right):
        if (left > right):
            return self.nums[0]
        
        # divide and conquer         
        mid = (left + right) // 2
        left_max = self.divide(left, mid-1)
        right_max = self.divide(mid+1, right)

        # situation 3 left part        
        sum = 0
        max_lsum = 0
        for i in range(mid-1, left-1, -1):
            sum += self.nums[i]
            max_lsum = max(max_lsum, sum)

        # situation 3 right part 
        sum = 0
        max_rsum = 0
        for i in range(mid+1, right+1):
            sum += self.nums[i]
            max_rsum = max(max_rsum, sum)

        max_sum = max(left_max, right_max)
        max_sum = max(max_sum, max_lsum + self.nums[mid] + max_rsum)

        return max_sum
    
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        self.nums = nums
        n = len(nums)
        return self.divide(0, n-1)

```

