---
title: LeetCode_Decode Ways
date: 2019-02-26 20:23:16
categories: LeetCode
tags: 
  - medium
  - string
  - dynamic programming
---

## [Decode Ways](https://leetcode.com/problems/decode-ways/)

A message containing letters from A-Z is mapped to 1-26, Given a non-empty string containing only digits, determine the total number of ways to decode it.
（解码方法）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_91.png" width = "500" align=center/>
</div>

### 1. 动态规划
对于扫描的第 i 个数字时，我们考虑其单独 mapping（dp[i] += dp[i-1]），或者 i-1 和 i 一起 mapping（dp[i] += dp[i-2]）。具体实现过程如下：

```python
class Solution:
    def numDecodings(self, s: str) -> int:
    	if s == '' or s == '0':
            return 0
        n = len(s)
        dp = [1] + [0] * n

        for i in range(1, n+1):
        	#  if int(s[i-1:i]) != 0:
            if int(s[i-1:i]) >=1 and int(s[i-1:i]) <= 9:
                dp[i] += dp[i-1]
            if i>=2 and int(s[i-2:i]) >=10 and int(s[i-2:i]) <= 26:
                dp[i] += dp[i-2]

        return dp[-1]
```