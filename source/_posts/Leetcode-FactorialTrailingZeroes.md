---
title: Leetcode_Factorial Trailing Zeroes
date: 2019-04-07 16:50:37
categories: LeetCode
tags: 
  - easy
  - math
---

## [Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/)

Given an integer n, return the number of trailing zeroes in n!.
（求 n! 的末尾0的个数）


<!--more-->

**Example:** 

<div align=center>
    <img src="/images/leetcode_172.png" width = "500" align=center/>
</div>


### 1. 计算从1-n中含2，5的因子个数。
题目中要求在时间复杂度为 O(log(n)) 的情况下完成。计算2和5的个数，实际上只需要计算5的个数，因为从1-n中因子2的个数一定大于5的个数。具体实现过程（循环 & 递归）如下：

```python
class Solution:
    def trailingZeroes(self, n: int) -> int:
        count_5 = 0
        while n:
            count_5 += n // 5
            n //= 5
        
        return count_5
        # return 0 if n == 0 else n // 5 + self.trailingZeroes(n // 5)
```