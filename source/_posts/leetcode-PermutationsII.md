---
title: LeetCode_Permutations II
date: 2019-01-09 13:51:06
categories: LeetCode
tags: 
  - medium
  - back tracking
---

## [Permutations II](https://leetcode.com/problems/permutations-ii/)

Given a collection of numbers that might **contain duplicates**, return all possible unique permutations.
(含有重复元素的全排列)

<!--more-->

**Example:**
<div align=center>
	<img src="/images/leetcode_47.png" width = "500" align=center/>
</div>


### 1. 递归
按照我们平时求全排列的思路，在选取数组中的某个数时，计算剩下的数组的全排列，具体实现方法如下：

```python
class Solution:
    def permuteUnique(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) == 1:
            return [nums]

        results = []	
        for i, item in enumerate(nums):
            new_nums = nums[0:i] + nums[i+1:]
            remain_results = self.permuteUnique(new_nums)

            if len(remain_results[0]) == 1:
                result = [item, remain_results[0][0]]
                if result not in results:
                    results.append(result)
            else:
                for items in remain_results:
                    result = [item] + [data for data in items]
                    if result not in results:
                        results.append(result)
        return results
```