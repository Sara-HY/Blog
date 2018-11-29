---
title: LeetCode_Roman to Integer
date: 2018-11-29 10:29:41
categories: LeetCode
tags: 
  - easy
  - math
  - string
---

# [Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

Roman numerals are represented by seven different symbols: **I, V, X, L, C, D and M** for **1, 5, 10, 50, 100, 500 and 1000**. 
（罗马字符转整数）

<!--more-->

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number **four is written as IV**. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:
  - **I** can be placed before **V** (5) and **X** (10) to make 4 and 9. 
  - **X** can be placed before **L** (50) and **C** (100) to make 40 and 90. 
  - **C** can be placed before **D** (500) and **M** (1000) to make 400 and 900.
  - Given an integer, convert it to a roman numeral. Input is guaranteed to be within the range from 1 to 3999.


**Example:** 

<div align=center>
	<img src="/images/leetcode_13.png" width = "500" align=center/>
</div>


### 1. 遍历字符串_1
遍历整个字符串，其中优先考虑两个字符表示的数值。其时间复杂度为 \\(O(n)\\)，具体实现过程如下：
```python
class Solution:
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """
        base = {
            'M': 1000,
            'CM': 900,
            'D': 500,
            'CD': 400,
            'C': 100,
            'XC': 90,
            'L': 50,
            'XL': 40,
            'X': 10,
            'IX': 9,
            'V': 5,
            'IV': 4,
            'I': 1
        }

        result = 0
        n = len(s)
        i = 0
        while i < n:
            if i < n-1 and s[i:i+2] in base:
                result += base[s[i:i+2]]
                i += 2
            elif s[i] in base:
                result += base[s[i]]
                i += 1
            
        return result 
```

### 2. 遍历字符串_2
直接遍历整个字符串，但是在扫描过程中若出现后面的字符对应的字符大于前面的字符，则减去两倍的前面的字符表示的数值。其时间复杂度为 \\(O(n)\\)，具体实现过程如下：

```python
class Solution:
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """
        base = {
            'M':1000,
            'D':500,
            'C':100,
            'L':50,
            'X':10,
            'V':5,
            'I':1
        }
        
        temp = 0
        result = 0
        for ch in s:
            if base[ch] > temp:
                result -= 2 * temp
            temp = base[ch]    
            result += temp
        
        return result
```
        











