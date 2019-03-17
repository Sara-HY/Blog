---
title: LeetCode_Find Minimum in Rotated Sorted Array II
date: 2019-03-17 23:05:17
categories: LeetCode
tags: 
  - hard
  - array
  - binary search
---

## [Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/)

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.(i.e.,  [0,1,2,4,5,6,7] might become  [4,5,6,7,0,1,2]). Find the minimum element. The array may contain **duplicates**.
（确定一个升序序列经过某个位置翻转后的数组的最小值(有重复元素)）

<!--more-->

**Note:** Would allow duplicates affect the run-time complexity? How and why?

**Example:** 

<div align=center>
	<img src="/images/leetcode_154.png" width = "500" align=center/>
</div>


### 1. 二分查找
与上一个不含重复元素的方法一致，只是在遇到相同的元素时，需要提前移动 left 和 right 指针。两者的时间复杂度都是 O(log(n))，但是在最坏的情况下，数组中全部是相同的元素，时间复杂度为O(n)。具体实现方法如下：

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        n = len(nums)
        if n == 1:
            return nums[0]
    
        left, right = 0, n-1
        while left < right:
            while left < right and nums[left+1]  == nums[left]:
                left += 1
            while left < right and nums[right-1] == nums[right]:
                right -= 1
            
            middle = (left + right) // 2
            if nums[middle] > nums[right]:
                left = middle + 1
            else:
                right = middle
        return nums[left]
```

### 2. 二分查找
另一种解决方案如下：

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        n = len(nums)
        if n == 1:
            return nums[0]
    
        left, right = 0, n-1
        while left < right:
            middle = (left + right) // 2
            if nums[middle] > nums[right]:
                left = middle + 1
            elif nums[middle] < nums[left]:
                right = middle
            else:
                right -= 1
        return nums[left]
```