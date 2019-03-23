---
title: LeetCode_Find Peak Element
date: 2019-03-23 18:17:18
categories: LeetCode
tags: 
  - medium
  - array
  - binary seach
---

## [Find Peak Element](https://leetcode.com/problems/find-peak-element/)

A peak element is an element that is greater than its neighbors. sGiven an input array nums, where nums[i] ≠ nums[i+1], find a peak element and return its index. The array may contain multiple peaks, in that case return the index to any one of the peaks is fine. You may imagine that nums[-1] = nums[n] = -∞.
（找到数组中的“波峰”值的index，一个即可。要求时间复杂度为O(logn)）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_162.png" width = "500" align=center/>
</div>


### 1. 二分查找
由于题中要求在时间复杂度为O(logn)的情况下实现，因此使用二分查找。
1. 当 middle 正好是峰值时，直接返回。
2. 当 `nums[middle] < nums[middle+1]` 时，右边一定会存在峰值，因为 `nums[n] = -∞`，因此 `left = middle`。
3. 其他情况，则左边会存在峰值，因此 `right = middle`。
具体实现过程如下：

```python
class Solution(object):
    def findPeakElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return None

        left, right = 0, len(nums)-1
        
        while left < right - 1:
            middle = (left + right) // 2
            if nums[middle] > nums[middle-1] and nums[middle] > nums[middle+1]:
                return middle
            if nums[middle] < nums[middle+1]:
                left = middle
            else:
                right = middle
        
        return left if nums[left] >= nums[right] else right
```