---
title: LeetCode_Scramble String
date: 2019-02-25 18:53:46
categories: LeetCode
tags: 
  - hard
  - string
  - recursion
  - dynamic programming
---

## [Scramble String](https://leetcode.com/problems/scramble-string/)

Given two strings s1 and s2 of the same length, determine if s2 is a scrambled string of s1.
(判断一个字符串是否为另一个字符串“乱序”得到)

<!--more-->

**Example:**

<div align=center>
	<img src="/images/leetcode_87.png" width = "500" align=center/>
</div>

### 1. 递归

根据题意，加入 s1 和 s2 是 scramble 的话，那么必然存在一个在 s1 上的长度 l1，将 s1 分成 s11 和 s12 两段，同样有 s21 和 s22. 要么 s11 和 s21 是 scramble 的并且 s12 和 s22 是 scramble 的；要么 s11 和 s22 是 scramble 的并且 s12 和 s21 是 scramble 的。就拿题目中的例子 “rgeat” 和 “great” 来说，“rgeat” 可分成 “rg” 和 “eat” 两段，“great” 可分成 “gr” 和 “eat” 两段，“rg” 和 “gr” 是 scrambled 的，“eat” 和 “eat” 当然是 scrambled 。具体实现过程如下：

```python
class Solution:
    def isScramble(self, s1: str, s2: str) -> bool:
        if len(s1) != len(s2):
            return False
        if s1 == s2:
            return True
        
        sort_s1, sort_s2 = sorted(s1), sorted(s2)
        if sort_s1 != sort_s2:
            return False
        
        for i in range(1, len(s1)):
            if (self.isScramble(s1[:i], s2[:i]) and self.isScramble(s1[i:], s2[i:])) or \
            (self.isScramble(s1[:i], s2[-i:]) and self.isScramble(s1[i:], s2[:len(s1)-i])):
                return True
        return False
```

### 2. 动态规划

这其实是一道**三维动态规划**的题目，我们提出维护量 res[i][j][n]，其中 i 是 s1 的起始字符，j 是 s2 的起始字符，而 n 是当前的字符串长度，res[i][j][length]表示的是以 i 和 j 分别为 s1 和 s2 起点的长度为 length 的字符串是不是互为scramble。
其递推表达式为，对于所有的 1<=k<\length:
 res[i][j][length] =  (res[i][j][k] && res[i+k][j+k][length-k] || res[i][j+length-k][k] && res[i+k][j][length-k])
也就是对于所有 len-1 种劈法的结果求或运算。具体实现方法如下：

```python
class Solution:
    def isScramble(self, s1: str, s2: str) -> bool:
        if len(s1) != len(s2):
            return False
        if s1 == s2:
            return True
        
        n = len(s1)
        dp = [[[False] * (n+1) for _ in range(n)] for _ in range(n)]
        for i in range(n):
            for j in range(n):
                if s1[i] == s2[j]:
                    dp[i][j][1] = True
        
        for length in range(2, n+1):
            for i in range(n-length+1):
                for j in range(n-length+1):
                    for k in range(1, length):
                        if (dp[i][j][k] and dp[i+k][j+k][length-k]) or \
                        (dp[i][j+length-k][k] and dp[i+k][j][length-k]):
                            dp[i][j][length] = True
                            
        return dp[0][0][n]
```
