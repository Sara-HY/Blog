---
title: LeetCode_Maximum Gap
date: 2019-03-25 14:00:56
categories: LeetCode
tags: 
  - hard
  - sort
---

## [Maximum Gap](https://leetcode.com/problems/maximum-gap/)

Given an unsorted array, find the maximum difference between the successive elements in its sorted form. Return 0 if the array contains less than 2 elements.
（乱序数组的排序后相邻元素差最大值）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_164.png" width = "500" align=center/>
</div>

### 1. 基数排序
这道题的本质是一个排序问题，要求在时间复杂度和空间复杂度都是 O(n) 的前提下完成任务。基数排序的时间复杂度为 O(d\*(n+k))≈O(n)，空间复杂度是 O(n+k)≈O(n)，其中 k 为基数，d为在k进制里面的最大位数。具体实现过程如下：

```python
class Solution(object):
    def maximumGap(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums or len(nums) == 1:
            return 0

        max_num = max(nums)
        bucket = [[] for i in range(10)]
        exp = 1
        while max_num // exp > 0:
            for num in nums:
                bucket[(num//exp) % 10].append(num)
            nums = []
            for each in bucket:
                nums.extend(each)
            bucket = [[] for i in range(10)]
            exp *= 10

        max_gap = 0
        for i in range(1, len(nums)):
            max_gap = max(max_gap, nums[i]-nums[i-1])
        return max_gap
```