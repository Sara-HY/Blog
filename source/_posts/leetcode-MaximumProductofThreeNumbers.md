---
title: LeetCode_Maximum Product of Three Numbers
date: 2019-08-22 21:01:34
categories: LeetCode
tags: 
  - easy
  - array
  - math
---

## [Maximum Product of Three Numbers](https://leetcode.com/problems/maximum-product-of-three-numbers/)

Given an integer array, find three numbers whose product is maximum and output the maximum product.
（从数组中找出乘积最大的3个数）

<!--more-->

**Note:**
1. The length of the given array will be in range [3, 104] and all elements are in the range [-1000, 1000].
2. Multiplication of any three numbers in the input won't exceed the range of 32-bit signed integer.

**Example:** 

<div align=center>
	<img src="/images/leetcode_628.png" width = "500" align=center/>
</div>

### 1. 遍历
暴力轮训，时间复杂度为 O(n^3)，空间复杂度为 O(1)。

### 2. 排序
排序，最终的结果为 max(nums[0]×nums[1]×nums[n−1], nums[n-3]×nums[n-2]×nums[n-1])。排序的时间复杂度为 O(nlogn)，空间复杂度为 O(logn)。

### 3. 遍历
仅仅遍历一次，其中维护5个变量，保留最大的三个数和最小的两个数，最终的结果表示同上。时间复杂度为 O(n)，空间复杂度为 O(1)。具体实现过程如下：

```python
class Solution:
    def maximumProduct(self, nums: List[int]) -> int:
        max_array = [float('-inf'), float('-inf'), float('-inf')]
        min_array = [float('inf'), float('inf')]
        
        for num in nums:
            if num >= max_array[0]:
                max_array = [num] + max_array[:-1]
            elif num >= max_array[1]:
                max_array = [max_array[0]] + [num] + [max_array[1]]
            elif num >= max_array[2]:
                max_array = max_array[:-1] + [num]
            if num <= min_array[0]:
                min_array = [num, min_array[0]]
            elif num <= min_array[1]:
                min_array[1] = num
                
        candidate_1 = max_array[0] * max_array[1] * max_array[2]
        candidate_2 = max_array[0] * min_array[0] * min_array[1]

        return max(candidate_1, candidate_2)
```