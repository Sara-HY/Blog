---
title: LeetCode_Wildcard Matching
date: 2019-01-06 15:49:16
categories: LeetCode
tags: 
  - hard
  - string
  - dynamic programming
  - back tracking
  - greedy
---

## [Wildcard Matching](https://leetcode.com/problems/wildcard-matching/)

Given an input string (s) and a pattern (p), implement wildcard pattern matching with support for “?” and “\*”.
(通配符匹配)

<!--more-->

“?” Matches any single character.
“\*” Matches any sequence of characters (including the empty sequence).
The matching should cover the entire input string (not partial).

**Note:**
 s could be empty and contains only lowercase letters a-z.
 p could be empty and contains only lowercase letters a-z, and characters like “?” or “\*”.

**Example:**
<div align=center>
	<img src="/images/leetcode_44.png" width = "500" align=center/>
</div>

### 1. 动态规划

这个题跟之前的字符串匹配类似，不同点在于之前 “\*” 可以匹配的是零个至多个**连续的字符**，而这道题目中的 “\*” 是可以匹配**任意的字符串**。我们还是可以基于动态规划的思想来解决这道题目，具体解法如下。其中在 pattern 中第 j 个元素为 “\*” 时，分为两种情况：
1. 当前 “\*” 表示为空串，则 dp[i][j] = dp[i-1][j]
2. 当前 “\*” 匹配当前的第 i 个字符 s[i-1], 则 dp[i][j] = dp[i][j-1] 

```python
class Solution:
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        len_s = len(s)
        len_p = len(p)
        dp = [[False] * (len_p + 1) for _ in range(len_s + 1)]

        dp[0][0] = True
        for i in range(len_s + 1):
            for j in range(1, len_p + 1):
                if p[j-1] == '*':
                    dp[i][j] = dp[i][j-1] or dp[i-1][j]
                else:
                    dp[i][j] = i>=1 and dp[i-1][j-1] and (p[j-1] in {s[i-1], '?'})

        return dp[len_s][len_p]
```