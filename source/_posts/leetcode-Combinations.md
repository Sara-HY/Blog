---
title: LeetCode_Combinations
date: 2019-02-23 13:58:02
categories: LeetCode
tags: 
  - medium
  - back tracking
---

## [Combinations](https://leetcode.com/problems/minimum-window-substring/)

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.
（列举 C_n^k 的所有组合）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_77.png" width = "500" align=center/>
</div>

### 1. 回溯法 / DFS
具体实现方法如下：

```python
class Solution:
    def dfs(self, i, re_list):
        if len(re_list) == self.k:
            self.result.append(re_list)
        for j in range(i, self.n + 1):   
            self.dfs(j + 1, re_list + [j])

    def combine(self, n: int, k: int) -> List[List[int]]:
        self.n = n
        self.k = k
        self.result = []
        self.dfs(1, [])
        return self.result
```