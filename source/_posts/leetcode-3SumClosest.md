---
title: LeetCode_3Sum Closest
date: 2018-11-29 12:11:39
categories: LeetCode
tags: 
  - medium
  - array
  - two pointers
---

## [3Sum Closest](https://leetcode.com/problems/3sum-closest/)

Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
（寻找数组中三个数的和最接近target的一个组合）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_16.png" width = "500" align=center/>
</div>

### 1. 三个指针
排序后三个指针遍历数组。其时间复杂度为 \\(O(n^2)\\)。
```python
class Solution:
    def threeSumClosest(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        nums.sort()
        n = len(nums)
        result = nums[0] + nums[1] + nums[2]
        for i in range(n - 2):
            l = i + 1
            r = n - 1
            while l < r:
                threesum = nums[l] + nums[r] + nums[i]
                if threesum == target :
                    return threesum

                if abs(threesum - target) < abs(result - target):
                	result = threesum

                if threesum > target:
                	r -= 1
                else:
                	l += 1
                
        return result
```