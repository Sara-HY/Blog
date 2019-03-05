---
title: LeetCode_Distinct Subsequences
date: 2019-03-05 15:26:36
categories: LeetCode
tags: 
  - hard
  - string
  - dynamic programming
---

## [Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)

Given a string S and a string T, count the number of distinct subsequences of S which equals T. A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ACE" is a subsequence of "ABCDE" while "AEC" is not).
（有效子序列个数）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_115.png" width = "500" align=center/>
</div>

### 1. 动态规划
这个题也可以看做一个字符串匹配的问题，一般都可以使用动态规划求解。具体实现过程如下：

```python
class Solution:
    def numDistinct(self, s: str, t: str) -> int:
    	# t 为空，则删除 s 中的所有元素，只有一种方案。
        if not t:
            return 1
        # t 不为空，s 为空，不可能匹配。
        if not s:
            return 0
        
        m, n = len(s), len(t)
        dp = [[0]* (n + 1) for _ in range(m + 1)]

        for i in range(m+1):
            for j in range(n+1):
                if i == 0 and j == 0:
                    dp[i][j] = 1
                elif i == 0:
                    dp[i][j] = 0
                elif j == 0:
                    dp[i][j] = 1
                else:
                	# s[i-1] 不参与匹配 
                    dp[i][j] = dp[i-1][j]
                    # s[i-1] 和 t[j-1] 匹配 
                    if s[i-1] == t[j-1]:
                        dp[i][j] += dp[i-1][j-1]
                        
        return dp[m][n]
```



