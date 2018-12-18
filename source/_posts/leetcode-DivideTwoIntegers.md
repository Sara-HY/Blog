---
title: LeetCode_Divide Two Integers
date: 2018-12-18 16:41:42
categories: LeetCode
tags: 
  - medium
  - math
  - binary search
---

## [Divide Two Integers](https://leetcode.com/problems/divide-two-integers/)

Given two integers dividend and divisor, divide two integers without using multiplication, division and mod operator. Return the quotient after dividing dividend by divisor. The integer division should truncate toward zero.
（非乘 除 取模 方法实现除法）

<!--more-->

Note:
- Both dividend and divisor will be 32-bit signed integers.
- The divisor will never be 0.
- Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. For the purpose of this problem, assume that your function returns 2^31 − 1 when the division result overflows.

**Example:** 

<div align=center>
	<img src="/images/leetcode_29.png" width = "500" align=center/>
</div>


### 1. 减法实现除法
这个题目很直观的就是将被除数不断地减去除数得到最终的商，但是会存在 Time Limit Exceeded 的问题。 因此需要在过程中不断地**加大除数**来加快得到最终结果。其中存在溢出的情况为被除数为-2^31, 除数为-1，得到的商为2^31，因此需要单独考虑。具体实现如下：

```python
class Solution:
    def divide(self, dividend, divisor):
        """
        :type dividend: int
        :type divisor: int
        :rtype: int
        """
        if (dividend < 0 and divisor < 0) or (dividend > 0 and divisor > 0):
            flag = 1
        else:
            flag = -1
        
        dividend = abs(dividend)
        divisor = abs(divisor)
        
        re = 0
        i = 1
        new_divisor = divisor
        while dividend >= new_divisor:
            re += i
            dividend -= new_divisor
            
            new_divisor += new_divisor
            i += i
            if dividend < new_divisor:
                new_divisor = divisor
                i = 1
         
        if flag < 0:
            return -re
        else:
            MAX = pow(2, 31) - 1
            return min(re, MAX)
```