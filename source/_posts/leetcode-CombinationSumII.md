---
title: LeetCode_Combination Sum II
date: 2018-12-25 18:22:35
categories: LeetCode
tags: 
  - medium
  - array
  - back tracking
---

# [Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target. Each number in candidates may only be used **once** in the combination.
（从集合中挑选和为特定值的数字组合，同一元素只可选一次）

<!--more-->

**Note:**
- All numbers (including target) will be positive integers.
- The solution set must not contain duplicate combinations.

**Example:** 

<div align=center>
	<img src="/images/leetcode_40.png" width = "500" align=center/>
</div>


### 1. 回溯法

这道题与上一题的区别在于：
1. 这个题限制了 candidates 中的元素只可以用一次。因此将遍历后的数组 candidates[i+1:] 继续遍历（因为candidates已经排序过了）。
2. candidates 可能存在有重复的元素。因此在生成最终的结果时，需要查重 list(re_set) not in self.result。

```python
class Solution:
    def backtracking(self, re_set, candidates, target):
        if target == 0 and list(re_set) not in self.result: 
        	self.result.append(list(re_set))
        	
        else:
        	for i in range(len(candidates)):
        		if target < candidates[i]:
        			break
        		else:
        			re_set.append(candidates[i])
        			self.backtracking(re_set, candidates[i+1:], target - candidates[i])
        			re_set.pop()

    def combinationSum2(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
       	self.result = []
       	re_set = []
       	candidates.sort()

        self.backtracking(re_set, candidates, target)
        
        return self.result
```