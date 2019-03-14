---
title: LeetCode_Palindrome Partitioning
date: 2019-03-14 10:34:52
categories: LeetCode
tags: 
  - medium
  - backtracking
---

## [Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)

Given a string s, partition s such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of s.
（切分字符串，每个子串都是回文序列）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_131.png" width = "500" align=center/>
</div>

### 1. 回溯法
下面是一个标准的回溯法的模板：

```python
class Solution:
    def checking(self, string):
        return string[::-1] == string
    
    def back_tracking(self, s, res, start):
        if start == len(s) and len(res) > 0:
            self.results.append(res)
        for i in range(start, len(s)):
            if self.checking(s[start:i+1]):
                self.back_tracking(s, res+[s[start:i+1]], i+1)
                  
    def partition(self, s: str) -> List[List[str]]:
        if not s:
            return []
        
        self.results = []
        self.back_tracking(s, [], 0)
        
        return self.results
```