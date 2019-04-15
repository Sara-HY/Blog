---
title: LeetCode_Rotate Array
date: 2019-04-15 20:45:45
categories: LeetCode
tags: 
  - easy
  - array
---

# [Rotate Array](https://leetcode.com/problems/rotate-array/)

Given an array, rotate the array to the right by k steps, where k is non-negative.
（翻转数组）

<!--more-->

**Note:**
1. Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
2. Could you do it in-place with O(1) extra space?

**Example:** 

<div align=center>
	<img src="/images/leetcode_189.png" width = "500" align=center/>
</div>


### 1. 数组拼接
根据上面的例子我们可以总结出如下规律，在经历了 k 次旋转之后的数组为原始数组的 [n-k:] 和 [:n-k] 两个数组拼接在一起的结果。其时间复杂度为 O(n) ，空间复杂度为 O(1) 。具体实现过程如下：

```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k = k % n
        nums[:] = nums[n-k:] + nums[:n-k]
        # nums[:] = nums[-k:] + nums[:-k]
```

### 2. 3次旋转数组
根据上面的例子我们可以总结出如下规律，在经历了 k 次旋转之后的数组为  1-原始数组全部旋转，2-前k项旋转，3-后n-k项旋转的结果。其时间复杂度为 O(n) ，空间复杂度为 O(1) 。具体实现过程如下：

```python
class Solution:
    def reverse(self, nums, start, end):
        while start < end:
            nums[start], nums[end] = nums[end], nums[start]
            start, end = start + 1, end - 1
            
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        if k is None or k <= 0:
            return
        k, end = k % len(nums), len(nums) - 1
        self.reverse(nums, 0, end - k)
        self.reverse(nums, end - k + 1, end)
        self.reverse(nums, 0, end)
```
