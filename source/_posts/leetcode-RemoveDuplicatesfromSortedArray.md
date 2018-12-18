---
title: LeetCode_Remove Duplicates from Sorted Array
date: 2018-12-18 14:48:12
categories: LeetCode
tags: 
  - easy
  - array
  - two pointers
---

## [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length. Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
（删除数组中重复的元素，限制空间复杂度）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_26.png" width = "500" align=center/>
</div>


### 1. 重复元素个数
这是一道easy题，需要在常量的空间复杂度的情况下去掉数组中重复的元素，只需要维护一个变量来记录在遍历过程中总共有多少个数字是重复的k，并在探索到新数据的同时将其前第k个数值赋为与其相等。具体实现过程如下：

```python
class Solution:
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        k = 0
        now = None
        for i, item in enumerate(nums):
            if item != now:
                now = item
                if k != 0:
                    nums[i-k] = item
            else:
                k += 1
        
        return len(nums)-k
```