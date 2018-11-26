---
title: LeetCode_String to Integer
date: 2018-11-26 16:23:21
categories: LeetCode
tags: 
  - medium
  - math
  - string
  - regular expression
---

## [String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

Implement atoi which converts a string to an integer.
（字符串转32位整形）

<!--more-->

Note:

Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: \\([−2^{31},  2^{31} − 1]\\). For the purpose of this problem, assume that your function **returns 0 when the reversed integer overflows**.

**Example:**

<div align=center>
	<img src="/images/leetcode_8.png" width = "500" align=center/>
</div>


### 字符串过滤-正则表达式
首先删除字符串首尾的空格，通过正则表达式过滤剩下以 "+-0123456789" 开头的句子，提取剩下的字符串首部的数字串，再将其转换为整形。（注意需要将超出范围的部分返回0。）

```
import re

class Solution:
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        string = str.strip()
        if not re.match(r'^(\-|\+)?\d+', string):
            return 0
       
        INT_MIN = -pow(2, 31)
        INT_MAX = pow(2, 31) - 1
        char_string = '+-0123456789'
        
        num_string = ''
        for i, char in enumerate(string):
            if char not in char_string:
                break
            if i != 0 and (char == '+' or char == '-'):
                break
            num_string += char
       
        if num_string[0] == '-':
            result = int(num_string[1:])
            result = max(result * - 1, INT_MIN)
            return result
        elif num_string[0] == '+': 
            result = int(num_string[1:])
        else:
            result = int(num_string)
        result = min(result, INT_MAX)  
        return result
```
**注**：需要考虑 \\(+/- \\) 出现在数字字符串中间的部分，因此 '0-1' 需要通过`if i != 0 and (char == '+' or char == '-')`过滤掉。