---
title: LeetCode_Interleaving String
date: 2019-02-27 20:45:31
categories: LeetCode
tags: 
  - medium
  - string
  - dynamic programming
---

## [Interleaving String](https://leetcode.com/problems/interleaving-string/)

Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.
（判断s1 与 s2 相互插入可否组成 s3）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_97.png" width = "500" align=center/>
</div>

**字符串匹配 & 动态规划 死锁**

### 1. 动态规划
dp[i][j]表示用 s1 的前 i 个字符和 s2 的前 j 个字符能不能按照规则表示出 s3 的前 i+j 个字符。
递推表达式为：
dp[i][j] = (dp[i][j-1] and s2[j-1] == s3[i + j -1]) or (dp[i-1][j] and s1[i-1] == s3[i + j -1]) 
其中需要注意维护边界，具体实现过程如下：

```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        len1, len2, len3 = len(s1), len(s2), len(s3)
        if len1 + len2 != len3:
            return False
        
        dp = [[False] * (len2 + 1) for _ in range(len1 + 1)]
        
        for i in range(len1+1):
            for j in range(len2+1):
                if i==0 and j==0:
                    dp[i][j] = True
                elif i==0:
                    dp[0][j] = dp[0][j-1] and s2[j-1] == s3[j-1]
                elif j==0:
                    dp[i][0] = dp[i-1][0] and s1[i-1] == s3[i-1]
                else:
                    dp[i][j] = (dp[i][j-1] and s2[j-1] == s3[i + j -1]) or (dp[i-1][j] and s1[i-1] == s3[i + j -1]) 
        
        return dp[len1][len2]
```