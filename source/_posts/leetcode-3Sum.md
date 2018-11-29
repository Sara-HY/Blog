---
title: LeetCode_3Sum
date: 2018-11-29 11:36:41
categories: LeetCode
tags: 
  - medium
  - array
  - two pointers
---

## [3Sum](https://leetcode.com/problems/3sum/)

Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.
（寻找数组中三个数的和为0的所有组合）

<!--more-->

Note:
The solution set must not contain duplicate triplets.

**Example:** 

<div align=center>
	<img src="/images/leetcode_15.png" width = "500" align=center/>
</div>

### 1. 三个指针
最外层一个指针 i 遍历整个数组，在里层遍历过程中设置 [l, r] 区间，其中`l , r = i + 1, len(nums) - 1,`，这样三个数分别是nums[i]，nums[l] 和 nums[r]。这道题一定要记住去重，去重的方法如下，其时间复杂度为 \\(O(n^2)\\)。
  - i 去重： if i > 0 and nums[i] ==  nums[i-1]: continue
  - l 去重： while l < r and nums[l] == nums[l-1]: l += 1
  - r 去重： while l < r and nums[r] == nums[r+1]: r -= 1


```python
class Solution(object):
    def threeSum(self, nums):
        result = []
        nums.sort()
        if len(nums) < 3:
            return result

        for i in range(len(nums) - 2):
            if i > 0 and nums[i] == nums[i-1]: continue
            l, r = i + 1, len(nums) - 1
            while l < r :
                s = nums[i] + nums[l] + nums[r]
                if s == 0:
                    result.append([nums[i] ,nums[l] ,nums[r]])
                    l += 1; r -= 1
                    while l < r and nums[l] == nums[l - 1]: l += 1
                    while l < r and nums[r] == nums[r + 1]: r -= 1
                elif s < 0 :
                    l += 1
                else:
                    r -= 1
        return result
```