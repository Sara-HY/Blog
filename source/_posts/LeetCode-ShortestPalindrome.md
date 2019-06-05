---
title: LeetCode_Shortest Palindrome
date: 2019-06-05 12:28:33
categories: LeetCode
tags: 
  - hard
  - string
---

## [Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome/)

Given a string s, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.
（在字符串前面增加字符使其为回文序列）

<!--more-->

**Example:**

<div align=center>
	<img src="/images/leetcode_214.png" width = "500" align=center/>
</div>

### 1. KMP算法
首先要找到`s`的最长回文前缀`s1`，剩余部分为`s2`，那么将`s2`反转和原`s`串拼接在一起，即可得到要求的回文串。这里用到 KMP 算法的 next 数组的求最长回文前缀`s1`，设置一个字符串tmp = s1 + s2 + '#' + s2' + s1'，具体实现过程如下：

```python
class Solution:
    def shortestPalindrome(self, s: str) -> str:
        n = len(s)
        if n <= 1:
            return s
        tmp = s + '#' + s[::-1]
        k = 0
        next = [0 for i in range(len(tmp))]
        for i in range(1, len(tmp)):
            while k > 0 and tmp[i] != tmp[k]:
                k = next[k-1]
            if tmp[i] == tmp[k]:
                k += 1
            next[i] = k
        return s[:next[-1]-1:-1] + s
```

