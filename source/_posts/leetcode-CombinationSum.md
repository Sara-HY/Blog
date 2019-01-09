---
title: LeetCode_Combination Sum
date: 2018-12-25 17:15:38
categories: LeetCode
tags: 
  - medium
  - array
  - back tracking
---

# [Combination Sum](https://leetcode.com/problems/combination-sum/)

Given a **set** of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target. The same repeated number may be chosen from candidates **unlimited** number of times.
（从集合中挑选和为特定值的数字组合，同一元素可选多次）

<!--more-->

**Note:**
- All numbers (including target) will be positive integers.
- The solution set must not contain duplicate combinations.

**Example:** 

<div align=center>
	<img src="/images/leetcode_39.png" width = "500" align=center/>
</div>


### 1. 回溯法
在构建回溯法的过程中，需要注意的是及时更新 target 来更新回溯限制条件。另外也可以事先对 candidates 排序来减少遍历的次数来节省时间。

```python
class Solution:
    def backtracking(self, re, candidates, target):
        if target == 0:
        	self.result.append(list(re))
        	
        else:
        	for i in range(len(candidates)):
        		if target < candidates[i]:
        			continue
        		re.append(candidates[i])
        		self.backtracking(re, candidates[i:], target - candidates[i])
        		re.pop()

    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
       	self.result = []
        self.backtracking([], candidates, target)
        
        return self.result
```
