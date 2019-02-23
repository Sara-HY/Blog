---
title: LeetCode_Remove Duplicates from Sorted Array II
date: 2019-02-23 15:20:08
categories: LeetCode
tags: 
  - easy
  - array
  - two pointers
---

## [Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)

Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length. Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
（删除数组中超过两次的元素，in-place, 限制空间复杂度）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_80.png" width = "500" align=center/>
</div>


### 1. 重复元素个数
需要维护一个变量来记录在遍历过程中数字是重复次数k，以及元素需要前移的步数move_before。具体实现过程如下：

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:        
        if len(nums) <= 2:
            return
        
        k, move_before = 0, 0
        now = None
        
        for i, num in enumerate(nums):
            if num != now:
                now = num
                if k > 2:
                    move_before += k-2
                k = 1
            else:
                k += 1
            nums[i-move_before] = num
        
        # last item
        if k > 2:
            move_before += k-2
        nums[i-move_before] = num

        return len(nums) - move_before
```