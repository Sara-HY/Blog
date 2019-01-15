---
title: LeetCode_Permutations
date: 2019-01-09 13:24:50
categories: LeetCode
tags: 
  - medium
  - back tracking
---

## [Permutations](https://leetcode.com/problems/permutations/)

Given a collection of **distinct** integers, return all possible permutations.
(排列组合)

<!--more-->

**Example:**
<div align=center>
	<img src="/images/leetcode_46.png" width = "500" align=center/>
</div>


### 1. 递归
按照我们平时求全排列的思路，在选取数组中的某个数时，计算剩下的数组的全排列，具体实现方法如下：

```python
class Solution:
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) == 1:
            return [nums]

        results = []	
        for item in nums:
            new_nums = [num for num in nums if num != item]
            result = self.permute(new_nums)
            if len(result[0]) == 1:
                results.append([item, result[0][0]])
            else:
                for _list in result:
                    results.append([item] + [data for data in _list])
        return results
```


### 2. DFS

另外一个思路是在看别人的解法发现的，使用**深度优先搜索（DFS）**的方法，具体实现方法如下：

```python
class Solution:
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        permutations = []
        self.dfs(permutations, [], nums)
        
        return permutations
    
    def dfs(self, perms, perm_in_progress, nums):
        # If we're out of numbers to use, Perm_in_progress is finished
        if not nums:
            perms.append(perm_in_progress)
        for index in range(0, len(nums)):
            self.dfs(perms, perm_in_progress + [nums[index]], nums[:index] + nums[index+1:])
```
