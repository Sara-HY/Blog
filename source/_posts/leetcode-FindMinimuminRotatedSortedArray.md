---
title: LeetCode_Find Minimum in Rotated Sorted Array
date: 2019-03-17 22:41:03
categories: LeetCode
tags: 
  - medium
  - array
  - binary search
---

## [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.(i.e.,  [0,1,2,4,5,6,7] might become  [4,5,6,7,0,1,2]). Find the minimum element. You may assume no duplicate exists in the array.
（确定一个升序序列经过某个位置翻转后的数组的最小值）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_153.png" width = "500" align=center/>
</div>


### 1. 二分查找
二分查找：
1. 在 `nums[middle] > nums[right]`，如[3, 4, 5, 1, 2]，说明最小值必然在右边，因此`left = middle + 1`；
2. 在 `nums[middle] <= nums[right]`，如[5, 1, 2, 3, 4]，说明最小的必然在左边，因此`right = middle`；
具体实现过程如下：

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
            else:
                right = middle
        return nums[left]
```