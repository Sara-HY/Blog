---
title: LeetCode_AddBinary
date: 2019-01-24 18:46:29
categories: LeetCode
tags: 
  - easy
  - string
  - math
---

## [Add Binary](https://leetcode.com/problems/add-binary/)

Given two binary strings, return their sum (also a binary string). The input strings are both non-empty and contains only characters 1 or 0.
（二进制字符串加法）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_67.png" width = "500" align=center/>
</div>

### 1. 十进制 & 二进制转换
```python
class Solution:
    def addBinary(self, a, b):
        """
        :type a: str
        :type b: str
        :rtype: str
        """
        a = int(a, 2)
        b = int(b, 2)
        return "{:b}".format(a + b) 
```