---
title: LeetCode_Subsets
date: 2019-02-23 14:29:21
categories: LeetCode
tags: 
  - medium
  - array
  - back tracking
  - bit manipulation
---

## [Subsets](https://leetcode.com/problems/subsets/)

Given a set of distinct integers, nums, return all possible subsets (the power set).
（列举所有子集）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_78.png" width = "500" align=center/>
</div>

### 1. 回溯法 / DFS
具体实现方法如下：

```python
class Solution:
    def dfs(self, i, re):
        if re not in self.result:
            self.result.append(re)
        
        for j in range(i, self.n):
            self.dfs(j+1, re + [self.nums[j]])
            self.dfs(j+1, re)
        
    def subsets(self, nums: List[int]) -> List[List[int]]:
        
        self.nums = nums
        self.n = len(nums)
        self.result = []
        
        self.dfs(0, [])
        
        return self.result
```

### 2. 递归
求子集的过程中，list 中的每一个元素要么出现，要么不出现。可以通过递归的方法，增加一个元素，即是原来的子集 + 子集中的每一个集合加上这个新元素的组合。具体实现过程如下：

```python
class Solution:
    def subsets(self, nums: 'List[int]') -> 'List[List[int]]':
        
        res = [[]]
        for num in sorted(nums):
            res += [item+[num] for item in res]
        return res
```
