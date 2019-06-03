---
title: LeetCode_Minimum Size Subarray Sum
date: 2019-06-03 10:55:52
categories: LeetCode
tags: 
  - medium
  - array
  - two pointers
  - binary search
---

## [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

Given an array of **n** positive integers and a positive integer **s**, find the minimal length of a **contiguous** subarray of which the sum ≥ **s**. If there isn't one, return 0 instead.
（最小长度的子数组的和大于特定的值）

<!--more-->

**Example:** 

<div align=center>
    <img src="/images/leetcode_209.png" width = "500" align=center/>
</div>

### 1. 两个指针

定义两个指针 left 和 right，分别记录子数组的左右的边界位置。让 right 向右移，直到子数组和大于等于给定值或者 right 达到数组末尾，此时我们更新最短距离，并且将 left 像右移一位，然后再 sum 中减去移去的值，然后重复上面的步骤，直到 right 到达末尾，且 left 到达临界位置，即要么到达边界，要么再往右移动，和就会小于给定值。时间复杂度为 O(n)，具体实现过程如下：

```python
class Solution:
    def minSubArrayLen(self, s, nums):
        if not nums:
            return 0
        n = len(nums)
        left, right, min_len, sum = 0, 0, n + 1, 0
    
        while right < n:
            while sum < s and right < n:
                sum += nums[right]
                right += 1
            while sum >= s:
                min_len = min(min_len, right-left)
                sum -= nums[left]
                left += 1

        if min_len == n + 1:
            return 0
        return min_len
```


### 2. 二分查找
由于一般的二分查找都是针对有序的数组进行的，而当前数组是无序的而且我们不能改变数组中元素的位置。因此构建一个新的数组 `sum`，`sum[i]`表示 nums[:i] 子数组的和。这个一定是递增的，因此我们可以对其进行二分查找，时间复杂度为 O(nlogn)。具体实现过程如下：

```python
class Solution:
    def binary_search(self, sums, key, left, right):
        while left <= right:
            mid = (left + right) // 2
            if sums[mid] >= key:
                right = mid - 1
            else:
                left = mid + 1
        return left

    def minSubArrayLen(self, s, nums):
        if not nums:
            return 0
        n = len(nums)
        min_len = n + 1
        sums = [0] * (n+1)
        
        for i in range(n):
            sums[i+1] = sums[i] + nums[i]
    
        for i in range(n+1):
            index = self.binary_search(sums, s + sums[i], i+1, n)
            if index == n + 1:
                break
            min_len = min(min_len, index - i)
        
        if min_len == n + 1:
            return 0
        return min_len
```






