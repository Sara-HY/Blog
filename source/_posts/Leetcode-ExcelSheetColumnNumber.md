---
title: Leetcode_Excel Sheet Column Number
date: 2019-04-07 15:40:59
categories: LeetCode
tags: 
  - easy
  - math
---

## [Excel Sheet Column Number](https://leetcode.com/problems/excel-sheet-column-number/)

Given a column title as appear in an Excel sheet, return its corresponding column number.
（将EXCEL表格中的列名称转换成数值）


<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_171.png" width = "500" align=center/>
</div>


### 1. 进制转换
这道题可以看做是一道进制转换的题目，将26进制转换成十进制。具体实现方法如下：

```python
class Solution:
    def titleToNumber(self, s: str) -> int:
        num = 0
        
        for char in s:
            num = num * 26
            num += ord(char) - ord('A') + 1
            
        return num
```