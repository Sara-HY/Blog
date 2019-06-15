---
title: LeetCode_Combination Sum III
date: 2019-06-06 11:10:19
categories: LeetCode
tags: 
  - medium
  - array
  - back tracking
---

# [Combination Sum III](https://leetcode.com/problems/combination-sum-iii/)

Find all possible combinations of **k** numbers that add up to a number **n**, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.
（从1-9中选取k个数的和为n）

<!--more-->

**Note:**
- All numbers will be positive integers.
- The solution set must not contain duplicate combinations.

**Example:** 

<div align=center>
	<img src="/images/leetcode_216.png" width = "500" align=center/>
</div>

### 1. 回溯法


```python
class Solution:
    def back_tracking(self, list, i, k, count):
        if count == 0 and k == 0:
            self.results.append(list)
        
        for j in range(i, 10):
            self.back_tracking(list+[j], j+1, k-1, count-j)
        
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        self.results = []
        self.back_tracking([], 1, k, n)
        
        return self.results
```