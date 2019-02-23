---
title: LeetCode_Search in Rotated Sorted Array II
date: 2019-02-23 15:46:52
categories: LeetCode
tags: 
  - medium
  - array
  - binary search
---

## [Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand. (i.e., [0,0,1,2,2,5,6] might become [2,5,6,0,0,1,2]). You are given a target value to search. If found in the array return true, otherwise return false.
（在时间复杂度为O(log n)的前提下在经旋转的有序数组中检索(数组中含有重复元素)）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_81.png" width = "500" align=center/>
</div>

### 1. 二分查找
定义首尾指针，在每次循环的过程中将 target 和 首尾指针的序列的中间值进行比较。其中在更新首尾指针的过程中需要讨论当前的[left, middle]数组是有序还是无序两种情况讨论。其中由于可能含有重复元素，需要跳过。具体实现如下：

```python
class Solution:
    def search(self, nums: List[int], target: int) -> bool:
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if not nums:
            return False
        
        left = 0
        right = len(nums)-1

        while left <= right:
            middle = (left + right) // 2
            
            if target == nums[middle]:
                return True
            
            while left < middle and nums[left] == nums[middle]:
                left += 1
            while right > middle and nums[right] == nums[middle]:
                right -= 1
            
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
        
        return False
```