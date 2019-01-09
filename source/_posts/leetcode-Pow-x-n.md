---
title: LeetCode_Pow(x, n)
date: 2019-01-09 15:02:05
categories: LeetCode
tags: 
  - medium
  - string
  - hash table
---

## [Pow(x, n)](https://leetcode.com/problems/powx-n/)

Implement pow(x, n), which calculates x raised to the power n (x^n).
(指数计算)

<!--more-->

**Note:** 
1. -100.0 < x < 100.0
2. n is a 32-bit signed integer, within the range [−2^31, 2^31 − 1]


**Example:**
<div align=center>
	<img src="/images/leetcode_50.png" width = "500" align=center/>
</div>


### 1. 递归

类似于二分法的方式进行指数运算。其中比较巧妙的地方是在 abs(n) 是奇数时，无论 n 是正数还是负数，left = n // 2 一定是比较小的哪一个，因此最终的结果一定是另外**乘以 x**。

```python
class Solution:
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        if n == 0:
            return 1
        if n == 1:
            return x
        if n == -1:
            return 1/x

        left = n // 2
        re = self.myPow(x, left)

        if left * 2 == n:
            return re * re
        else:
            return re * re * x
```