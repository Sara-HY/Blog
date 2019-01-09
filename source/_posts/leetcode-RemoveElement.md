---
title: LeetCode_Remove Element
date: 2018-12-18 16:12:33
categories: LeetCode
tags: 
  - easy
  - array
  - two pointers
---

## [Remove Element](https://leetcode.com/problems/remove-element/)

Given an array nums and a value val, remove all instances of that value in-place and return the new length. Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory. The order of elements can be changed. It doesn't matter what you leave beyond the new length.
（删除数组中特定元素，限制空间复杂度）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_27.png" width = "500" align=center/>
</div>


### 1. 特定元素个数
这是一道 easy 题，需要在常量的空间复杂度的情况下去掉数组中特定的元素，与前一道题目的思想类似，只需要维护一个变量来记录在遍历过程中总共有 k 个值与 val 相等，并在探索到不是 val 的同时将其前第 k 个数值赋为与其相等。具体实现过程如下：

```python
class Solution:
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        k = 0
        for i, item in enumerate(nums):
            if item == val:
                k += 1
            else:
                nums[i-k] = item
        
        return len(nums)-k
```