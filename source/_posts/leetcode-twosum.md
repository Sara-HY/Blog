---
title: LeetCode_Two Sum
date: 2018-11-23 10:57:23
categories: LeetCode
tags: 
  - easy
  - array
  - hash table
---

## [Two Sum](https://leetcode.com/problems/two-sum/)

Given an array of integers, return indices of the two numbers such that they add up to a specific target. You may assume that each input would have **exactly one solution**, and you may **not** use the **same element** twice.
（一个数组中某两个元素的和为给定值）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_1.png" width = "500" align=center/>
</div>

这道题是开始刷LeetCode的第一道题，难度属于esay，主要考察的是数组，另外也考虑到了哈希表。具体解法如下：

### 1. 暴力循环
这种解法就是很直观，就是对数组进行两层循环遍历。其时间复杂度为 \\(O(n^2)\\), 空间复杂度为  \\(O(1)\\)。

### 2. 构建哈希表
构建哈希表可以有效的降低时间复杂度，且只需要对数组遍历一次。其时间复杂度为 \\(O(n)\\), 空间复杂度为  \\(O(n)\\)。

(注：可以对数组进行两次遍历，第一次构建哈希表，第二次找答案。)

```python
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        d = {}
        for i, number in enumerate(nums):
            if (target - number) in d:
                return [i, d[target-number]]
            d[number] = i
```

**注**：在思考的过程中需要认真看清题中的每个元素只能用一次，但是并不代表每个数值只能用一次。