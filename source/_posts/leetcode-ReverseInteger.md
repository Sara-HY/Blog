---
title: LeetCode_Reverse Integer
date: 2018-11-26 15:26:31
categories: LeetCode
tags: 
  - easy
  - math
---

## [Reverse Integer](https://leetcode.com/problems/reverse-integer/)

Given a 32-bit signed integer, reverse digits of an integer.
（翻转一个有符号整形数值字符串）

Note:
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: \\([−2^{31},  2^{31} − 1]\\). For the purpose of this problem, assume that your function **returns 0 when the reversed integer overflows**.

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_7.png" width = "500" align=center/>
</div>


### 1. 字符串翻转 
```
class Solution:
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        string = str(x)
        n = len(string)
        
        if string[0] == '-':
            result = [string[n-i] for i in range(1, n)]
            result = ['-'] + result
        else:
            result = [string[n-i-1] for i in range(n)]
        
        re = int("".join(result))
        
        if re > pow(2, 31) - 1 or re < - pow(2, 31):
            re = 0
        return re
```

**注**：超过有符号整形的范围时需要返回0。另外`string[::-1]`也可以直接实现字符串的翻转。


### 2. 整形翻转 
```
class Solution:
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        
        abso_x = abs(x)
        result = 0
        
        while abso_x != 0 :
            a = abso_x % 10
            abso_x = abso_x // 10
            result = result * 10  + a
            
        if x < 0:
            result *= -1  
            
        if result > (pow(2, 31) - 1) or result < -pow(2, 31):
            return 0
        
        return result
```



