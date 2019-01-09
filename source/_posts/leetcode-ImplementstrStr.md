---
title: LeetCode_Implement strStr()
date: 2018-12-18 16:21:01
categories: LeetCode
tags: 
  - easy
  - string
  - two pointers
---

## [Implement strStr()](https://leetcode.com/problems/implement-strstr/)

Implement strStr(). Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.
（实现寻找字符串子串函数）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_28.png" width = "500" align=center/>
</div>


### 1. 遍历 -- easy
```python
class Solution:
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        n = len(needle)
        m = len(haystack)
        
        if n == 0:
            return 0
        
        if n > m:
            return -1
        
        for i in range(m-n+1):
            if haystack[i:i+n] == needle:
                return i
        
        return -1
```

### 2. 调用 python 库函数 in, index
```python
class Solution:
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if needle not in haystack:
            return -1
        else:
            return haystack.index(needle)
```