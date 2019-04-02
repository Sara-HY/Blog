---
title: LeetCode_Excel Sheet Column Title
date: 2019-04-02 17:45:16
categories: LeetCode
tags: 
  - easy
  - math
---

## [Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/)

Given a positive integer, return its corresponding column title as appear in an Excel sheet.
（将数值转换成EXCEL表格中的列名称）


<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_168.png" width = "500" align=center/>
</div>


### 1. 进制转换
这道题可以看做是一道进制转换的题目，将十进制转换成26进制。其中，需要注意的是每次都使用 `n-1` 作为被除数是为了方便计算与 `A` 的 ASCII码的差值。具体实现方法如下：

```python
class Solution:
    def convertToTitle(self, n: int) -> str:
        result = ''
        while n:
            n, remainder = divmod(n-1, 26)
            result = chr(ord('A') + remainder) + result
        
        return result
```