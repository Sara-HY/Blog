---
title: LeetCode_Search in Rotated Sorted Array
date: 2018-12-21 13:07:49
categories: LeetCode
tags: 
  - medium
  - array
  - binary search
---

## [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

Suppose an **array sorted in ascending order is rotated** at some pivot unknown to you beforehand. (i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]). You are given a target value to search. If found in the array return its index, otherwise return -1. You may assume no duplicate exists in the array. Your algorithm's runtime complexity must be in the order of **O(log n)**.
（在时间复杂度为O(log n)的前提下在经旋转的有序数组中检索）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_33.png" width = "500" align=center/>
</div>

### 1. 二分查找
定义首尾指针，在每次循环的过程中将 target 和 首尾指针的序列的中间值进行比较。其中在更新首尾指针的过程中需要讨论当前的[left, middle]数组是有序还是无序两种情况讨论。具体实现如下：

```python
class Solution:
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if not nums:
            return -1
        
        left = 0
        right = len(nums)-1

        while left <= right:
            middle = (left + right) // 2
            
            if target == nums[middle]:
                return middle
            
            if nums[left] <= nums[middle]:
                if target < nums[middle] and target >= nums[left]:
                    right = middle - 1
                else:
                    left = middle + 1
            else:
                if target > nums[middle] and target <= nums[right]:
                    left = middle + 1
                else:
                    right = middle - 1
    
        return -1
```