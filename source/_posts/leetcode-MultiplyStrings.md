---
title: LeetCode_Multiply Strings
date: 2019-01-03 22:45:45
categories: LeetCode
tags: 
  - medium
  - math
  - string
---

## [Multiply Strings](https://leetcode.com/problems/multiply-strings/)

Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2, also represented as a string.
（用非库函数的方式返回两个字符串表示的整数的乘积）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_43.png" width = "500" align=center/>
</div>

Note:
- The length of both num1 and num2 is < 110.
- Both num1 and num2 contain only digits 0-9.
- Both num1 and num2 do not contain any leading zero, except the number 0 itself.
- You must not use any built-in BigInteger library or convert the inputs to integer directly.

### 实现库函数 atoi 和 itoa
由于题中备注了不让使用自带的库函数，因此可以自己实现。其中在 python 中 `ord()`表示将字符转换为ASCII码，`chr()`表示将ASCII码转换为字符。具体实现过程如下：

```python
class Solution:
    def multiply(self, num1, num2):
        """
        :type num1: str
        :type num2: str
        :rtype: str
        """
        def atoi(s):
            result = 0
            for char in s:
                result = result * 10 + (ord(char) - ord('0'))
            return result
    
        def itoa(num):
            if num == 0:
                return "0"
            s = ""
            while num:
                char = num % 10 + ord('0')
                s = chr(char) + s
                num = num // 10
            
            return s
        
        return itoa(atoi(num1) * atoi(num2))
```