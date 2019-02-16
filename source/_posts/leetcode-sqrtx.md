---
title: LeetCode_Sqrt X
date: 2019-02-16 17:13:26
categories: LeetCode
tags: 
  - easy
  - math
  - binary search
---

## [Sqrt(x)](https://leetcode.com/problems/sqrtx/)

Implement int sqrt(int x). Compute and return the square root of x, where x is guaranteed to be a non-negative integer. Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.
（实现Sqrt(x)）

<!--more-->

**Example:**

<div align=center>
	<img src="/images/leetcode_69.png" width = "500" align=center/>
</div>

### 1. 二分查找
```python
class Solution:
    def mySqrt(self, x: 'int') -> 'int':
        left, right = 0, x
        
        while left <= right:
            middle  = (left + right)//2
            if middle * middle <= x and (middle+1) * (middle+1) > x:
                return middle
            elif middle * middle < x:
                left = middle + 1
            else:
                right = middle - 1
```