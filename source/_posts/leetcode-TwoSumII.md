---
title: LeetCode_Two Sum II
date: 2019-04-02 17:14:28
categories: LeetCode
tags: 
  - easy
  - array
  - two pointers
  - binary search
---

## [Two Sum II](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number. The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.
（一个升序数组中某两个元素的和为给定值）


<!--more-->

**Note:**
1. Your returned answers (both index1 and index2) are not zero-based.
2. You may assume that each input would have exactly one solution and you may not use the same element twice.

**Example:** 

<div align=center>
	<img src="/images/leetcode_1.png" width = "500" align=center/>
</div>


### 1. 双指针
首尾指针指向数组，通过与 `target` 判断大小来移动左、右指针，具体实现过程如下：

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left, right = 0, len(numbers)-1
        
        while left < right:
            if numbers[left] + numbers[right] == target:
                return [left+1, right+1]
            elif numbers[left] + numbers[right] < target:
                left += 1
            else:
                right -= 1
```

### 2. 二分查找
首先定位左边的元素，然后通过二分查找查找右边的元素，具体实现过程如下：

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        n = len(numbers)
        
        for i in range(n):
            new_target = target - numbers[i]
            left, right = i+1, n-1
            while left <= right:
                middle = (left + right) // 2
                if numbers[middle] == new_target:
                    return [i+1, middle+1]
                elif numbers[middle] < new_target:
                    left = middle + 1
                else:
                    right = middle - 1
```

### 3. 哈希表 （与Two Sum方法一致）