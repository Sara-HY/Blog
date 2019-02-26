---
title: LeetCode_Subsets II
date: 2019-02-26 18:45:47
categories: LeetCode
tags: 
  - medium
  - array
  - back tracking
---

## [Subsets II](https://leetcode.com/problems/subsets-ii/)

Given a collection of integers that might contain duplicates, nums, return all possible subsets (the power set).
（列举所有子集）

**Note:** The solution set must not contain duplicate subsets.


<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_90.png" width = "500" align=center/>
</div>

### 1. 回溯法 / DFS

```python
class Solution:
    def dfs(self, index, re):
        if sorted(re) not in self.results:
            self.results.append(sorted(re))

        for i in range(index, len(self.nums)):
            self.dfs(i+1, re)
            self.dfs(i+1, re + [self.nums[i]])
            
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        self.results = []
        self.nums = nums
        self.dfs(0, [])
        
        return self.results
```