---
title: LeetCode_Longest Palindromic Substring
date: 2018-11-26 11:28:13
categories: LeetCode
tags: 
  - medium
  - string
  - dynamic programming
---

## [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

Given a string **s**, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.
（寻找最长回文序列）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_5.png" width = "500" align=center/>
</div>


### 1.动态规划
这也是一道很典型的动态规划的题目。简单地来看可以有如下规律：

\\[ if s[i] == s[j]\ and\ dp[i+1][j-1] == 1,\ dp[i][j] = 1\\]

然后我们可以找到满足dp[i][j] == 1的最长的序列。其时间复杂度为 \\(O(n^2)\\)，空间复杂度为 \\(O(n^2)\\)。具体实现过程如下：
```python
class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        n = len(s)
        dp = [[0] * n  for i in range(n)]
    
        result = ''
        max_len = 0
        for i in range(n):
            dp[i][i] = 1
            result = s[i]
            max_len = 1
        
        for j in range(n):
            for i in range(0, j):
                if s[i] == s[j] and (dp[i+1][j-1] == 1 or i == j-1):
                    dp[i][j] = 1
                    if max_len <= j - i + 1:
                        result = s[i:j+1]
                        max_len = j - i + 1
        
        return result
```

