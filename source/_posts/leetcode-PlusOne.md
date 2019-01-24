---
title: LeetCode_Plus One
date: 2019-01-24 17:35:10
categories: LeetCode
tags: 
  - easy
  - array
  - math
---

## [Plus One](https://leetcode.com/problems/plus-one/)

Given a non-empty array of digits representing a non-negative integer, plus one to the integer. The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit. You may assume the integer does not contain any leading zero, except the number 0 itself.
（数组形式的数字串数值加1）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_66.png" width = "500" align=center/>
</div>

### 1. 加法进位原则
**Note:** 需要特别注意第一个数字进位的情况。

```python
class Solution:
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        
        n = len(digits)

        add = 1
        result = [0 for _ in range(n+1)]

        for i in range(n-1, -1, -1):
            add += digits[i]
            result[i+1] = add % 10
            add = add // 10
        
        if add == 0:
            return result[1:]
        else:
            result[0] = add
            return result
```