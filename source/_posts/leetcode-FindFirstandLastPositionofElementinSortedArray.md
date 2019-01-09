---
title: LeetCode_Find First and Last Position of Element in Sorted Array
date: 2018-12-21 14:01:10
categories: LeetCode
tags: 
  - medium
  - array
  - binary search
---

## [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value. Your algorithm's runtime complexity must be in the order of O(log n). If the target is not found in the array, return [-1, -1].

（在时间复杂度为O(log n)的前提下在有序数组中检索target的第一次及最后一次）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_34.png" width = "500" align=center/>
</div>

### 1. 二分查找
```python
class Solution:
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        
        n = len(nums)
        if n == 0:
            return [-1, -1]
        
        re_left, re_right = -1, -1

        # find the first index
        left, right = 0, n-1
        while left <= right:
            middle = (left + right) // 2
            
            if target == nums[middle]:
                re_left = middle
                right = middle - 1
            elif target > nums[middle]:
                left = middle + 1
            else:
                right = middle - 1
        
        if nums[left] != target:
        	return [-1, -1]
           
        # find the last index     
        left, right = 0, n-1 
        while left <= right:
            middle = (left + right) // 2
            
            if target == nums[middle]:
                re_right = middle
                left = middle + 1
            elif target > nums[middle]:
                left = middle + 1
            else:
                right = middle - 1
                
        return [re_left, re_right]
```
