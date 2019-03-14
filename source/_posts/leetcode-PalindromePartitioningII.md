---
title: LeetCode_Palindrome Partitioning II
date: 2019-03-14 13:51:53
categories: LeetCode
tags: 
  - hard
  - dynamic programming
---

## [Palindrome Partitioning II](https://leetcode.com/problems/palindrome-partitioning-ii/)

Given a string s, partition s such that every substring of the partition is a palindrome. Return the minimum cuts needed for a palindrome partitioning of s.
（最少切分字符串，每个子串都是回文序列）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_132.png" width = "500" align=center/>
</div>


### 1. 动态规划
首先维护一个二维矩阵来保存 s[i:j] 是否为回文序列。使用一维动规，初始化 dp 为字符串的索引（默认不存在任何回文序列的部分）；在双重循环遍历字符串的过程中判断 s[i:j+1] 是否为回文序列，若是：
1. 在i==0时，表示字符串 s[:j+1]为回文序列，则dp[j] = 0
2. 否则，取 dp[i-1] + 1 和 dp[j] 的 最小值，也就是在 i 处切分字符串。
具体实现方法：

```python
class Solution:
    def minCut(self, s: str) -> int:
        if not s or s[::-1] == s:
            return 0
        
        n = len(s)
        palindrome = [[False]*(n) for _ in range(n)]
        dp = [i for i in range(n)]
        
        for j in range(n):
            for i in range(j+1):
                if s[i]==s[j] and (j-i<2 or palindrome[i+1][j-1]):
                    palindrome[i][j] = True
                    
                    if i==0:
                        dp[j] = 0
                    elif dp[i-1] + 1 < dp[j]:
                        dp[j] = dp[i-1] + 1
            
        return dp[n-1]
```