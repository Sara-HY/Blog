---
title: LeetCode_Fraction to Recurring Decimal
date: 2019-04-02 16:30:40
categories: LeetCode
tags: 
  - medium
  - hash table
  - math
---

## [Fraction to Recurring Decimal](https://leetcode.com/problems/fraction-to-recurring-decimal/)

Given two integers representing the numerator and denominator of a fraction, return the fraction in string format. If the fractional part is repeating, enclose the repeating part in parentheses.
（分数->小数）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_166.png" width = "500" align=center/>
</div>

### 1. 哈希表
本题意在将分数转换为小数点的形式表示，主要考察的是**无限循环小数**。在除法与商和余数的过程中，首先需要考虑符号的问题。其次，我们需要把每次的余数保存在 `remainder_map` 中，当下次出现余数已经出现了则说明出现了循环。具体实现方法如下：

```python
class Solution:
    def fractionToDecimal(self, numerator: int, denominator: int) -> str:
        if numerator * denominator < 0:
            sign = '-'
        else:
            sign = ''
        result = sign
        
        integer, remainder = divmod(abs(numerator), abs(denominator))
        result += str(integer)
        
        if remainder:
            result += '.'
            remainder_map = {}
            while remainder:
                if remainder not in remainder_map:
                    remainder_map[remainder] = len(result)
                    integer, remainder = divmod(remainder * 10, abs(denominator))
                    result += str(integer)
                else:
                    index = remainder_map[remainder]
                    result = result[:index] + '(' + result[index:] + ')'
                    break
                
        return result
```