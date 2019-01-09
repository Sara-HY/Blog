---
title: LeetCode_Search Insert Position
date: 2018-12-21 14:26:10
categories: LeetCode
tags: 
  - easy
  - array
  - binary search
---

## [Search Insert Position](https://leetcode.com/problems/search-insert-position/)

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order. You may assume no duplicates in the array.
（在有序数组中检索）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_35.png" width = "500" align=center/>
</div>

### 1. 二分查找
```python
class Solution:
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        n = len(nums)
        if n == 0:
            return 0
        
        left, right = 0, n-1
    
        while left <= right:
            middle = (left + right) // 2
            
            if target == nums[middle]:
                return middle
            elif target < nums[middle]:
                right = middle - 1
            else:
                left = middle + 1
                
        return left
```

