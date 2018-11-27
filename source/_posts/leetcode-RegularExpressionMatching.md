---
title: LeetCode_Regular Expression Matching
date: 2018-11-26 22:13:49
categories: LeetCode
tags: 
  - hard
  - string
  - dynamic programming
  - backtracking
---

## [Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)

Given an input **string (s)** and a **pattern (p)**, implement regular expression matching with support for **.** and **\***, **.** matches any single character, **\*** matches zero or more of the preceding element. The matching should cover the entire input string (not partial).
（字符串正则表达式匹配）

<!--more-->

Note:
**s** could be empty and contains only lowercase letters a-z.
**p** could be empty and contains only lowercase letters a-z, and characters like . or \*.

**Example:**

<div align=center>
	<img src="/images/leetcode_10.png" width = "500" align=center/>
</div>

### 1. 递归算法
正则表达式的匹配算法可以很自然的想到递归，但是其时间复杂度比较高。
  - len(p) >= 2 and p[1] = \*，则需要分类讨论：
  	 - p[0] 匹配了0个，则可以直接判断 s 和 p[2:] ；
  	 - p[0] 至少匹配了1个，则可以判断 s[1:] 和 p ；
  - len(p) < 2，可以直接判断；

```python
class Solution:
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        if not p:
            return not s
        
        first_match = bool(s) and (p[0] in {s[0], '.'})
        
        if len(p) >=2 and p[1] == '*':
            return (self.isMatch(s, p[2:])) or (first_match and self.isMatch(s[1:], p))
        else:
            return first_match and self.isMatch(s[1:], p[1:])
```

### 2. 动态规划
dp[i][j] 表示 s 的前 i 个字符和 p 的前 j 个字符是否匹配，具体 dp 迭代更新与上述相同。其中 `j >= 2 and dp[i][j-2]` 表示扩展当前的 \* ，`i >= 1 and j >= 2 and dp[i-1][j] and p[j-2] in {s[i-1], '.'}` 表示扩展当前的 \* 。

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
                    dp[i][j] = (i >= 1 and j >= 2 and dp[i-1][j] and p[j-2] in {s[i-1], '.'}) or (j >= 2 and dp[i][j-2])
                else:
                    dp[i][j] = (i >= 1 and dp[i-1][j-1] and p[j-1] in {s[i-1], '.'})
                    
        return dp[len_s][len_p]
```






