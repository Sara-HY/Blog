---
title: LeetCode_Integer to Roman
date: 2018-11-28 15:40:20
categories: LeetCode
tags: 
  - medium
  - math
  - string
---

## [Integer to Roman](https://leetcode.com/problems/integer-to-roman/)

Roman numerals are represented by seven different symbols: **I, V, X, L, C, D and M** for **1, 5, 10, 50, 100, 500 and 1000**. 
（整数转罗马字符）

<!--more-->

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number **four is written as IV**. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:
  - **I** can be placed before **V** (5) and **X** (10) to make 4 and 9. 
  - **X** can be placed before **L** (50) and **C** (100) to make 40 and 90. 
  - **C** can be placed before **D** (500) and **M** (1000) to make 400 and 900.
  - Given an integer, convert it to a roman numeral. Input is guaranteed to be within the range from 1 to 3999.


**Example:** 

<div align=center>
	<img src="/images/leetcode_12.png" width = "500" align=center/>
</div>


### 1. 基数扩展
由于 "4" 和 "9" 的特殊性，我们可以将其也包含在基数列表中，于是基数可以是1，4，5，9，10，40，50，90，100，400，500，900。具体实现过程如下：
```python
class Solution:
    def intToRoman(self, num):
        """
        :type num: int
        :rtype: str
        """
        base = {
            1000: 'M',
            900: 'CM',
            500: 'D',
            400: 'CD',
            100: 'C',
            90: 'XC',
            50: 'L',
            40: 'XL',
            10: 'X',
            9: 'IX',
            5: 'V',
            4: 'IV',
            1: 'I'
        }
        
        base_list = [1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1]
        
        result = ""
        for i in range(len(base_list)):
            if num // base_list[i] != 0:
                for j in range(num // base_list[i]):
                    result += base[base_list[i]]
                num = num % base_list[i]
            
        return result 
```


### 2. 列表索引
列出所有可能的罗马字符的表示形式，然后直接对列表进行索引即可。具体实现过程如下：
```python
class Solution:
    def intToRoman(self, num):
        """
        :type num: int
        :rtype: str
        """
        M = ["", "M", "MM", "MMM"]
        C = ["", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"]
        X = ["", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"]
        I = ["", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"]
    
        return M[num//1000] + C[(num%1000)//100] + X[(num%100)//10] + I[num%10]
```




