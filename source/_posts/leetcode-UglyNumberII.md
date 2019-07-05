---
title: Leetcode_Ugly Number II
date: 2019-06-30 17:01:13
categories: LeetCode
tags: 
  - medium
  - math
  - dynamic programming
---

## [Ugly Number II](https://leetcode.com/problems/ugly-number-ii/)

Write a program to find the n-th ugly number. Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. 
（第 n 个丑数）


<!--more-->

**Note:**
1. 1 is typically treated as an ugly number.
2. n does not exceed 1690.

**Example:** 

<div align=center>
	<img src="/images/leetcode_264.png" width = "500" align=center/>
</div>


### 1. 动态规划

任何一个新的丑数可以看做是一个旧的丑数乘以 2，3，5 得到的。因此可以设置三个指针，每当因为乘以一个因子而增加一个丑数时，相应的指针就后移，具体实现过程如下：

```python
class Solution:
    def nthUglyNumber(self, n: int) -> int:
        ugly_list = [1]
        p_2, p_3, p_5 = 0, 0, 0
        
        while len(ugly_list) < n:
            num_2, num_3, num_5 = ugly_list[p_2]*2, ugly_list[p_3]*3, ugly_list[p_5]*5
            min_num = min(num_2, num_3, num_5)
            
            if num_2 == min_num:
                p_2 += 1
            if num_3 == min_num:
                p_3 += 1
            if num_5 == min_num:
                p_5 +=1
            ugly_list.append(min_num)
        return ugly_list[-1]
```