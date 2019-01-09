---
title: LeetCode_First Missing Positive
date: 2018-12-25 18:43:04
categories: LeetCode
tags: 
  - hard
  - array
---

# [First Missing Positive](https://leetcode.com/problems/first-missing-positive/)

Given an unsorted integer array, find the smallest missing positive integer.
（在未排序数组中找到最小的非正数）

<!--more-->

**Note:**
- Your algorithm should run in O(n) time and uses constant extra space.

**Example:** 

<div align=center>
	<img src="/images/leetcode_41.png" width = "500" align=center/>
</div>

### 1. 哈希法

要在时间复杂度为 \\( O(n)\\)，且常数额外空间的情况下完成这个问题。哈希法的思路是分析数组中的正数应该在的位置。我们发现例子中的 [3, 4, -1, 1] 的答案是2，我们可以通过遍历数组将其转换为 [1, -1, 3, 4]，即数组中的index为 i 的值应该是正数 i + 1，从左向右遍历若不满足这个要求，则这就是我们要找的缺失的最小正数。

```python
class Solution:
    def firstMissingPositive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        i, n = 0, len(nums)

        while i < n:
            # nums[i] > 0, nums[i] <= n means positive number in [1, n]
            # nums[i] != i+1 means index==i but it is not i + 1
            # nums[nums[i] - 1] != nums[i] means index==nums[i] - 1 which should be nums[i]
            if nums[i] > 0 and nums[i] <= n and nums[i] != i+1 and nums[nums[i] - 1] != nums[i]:
                temp = nums[i]
                nums[i], nums[temp-1] = nums[temp-1], nums[i]
            else:
                i += 1

        for i in range(n):
            if nums[i] != i+1:
                return i+1
         
        return n+1
```