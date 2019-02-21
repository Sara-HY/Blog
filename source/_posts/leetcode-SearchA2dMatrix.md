---
title: LeetCode_Search A 2D Matrix
date: 2019-02-21 15:28:18
categories: LeetCode
tags: 
  - medium
  - array
  - binary search
---

## [Search A 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties: Integers in each row are sorted from left to right. The first integer of each row is greater than the last integer of the previous row.
(查找数值是否在有序矩阵中)

<!--more-->

**Example:**
<div align=center>
	<img src="/images/leetcode_74.png" width = "500" align=center/>
</div>


### 1. 二分查找

```python
class Solution:
    def searchMatrix(self, matrix: 'List[List[int]]', target: 'int') -> 'bool':
        if not matrix or not matrix[0]:
            return False
        
        m, n = len(matrix), len(matrix[0])
        left, right = 0, m * n -1

        while left <= right:
            middle = (left + right) // 2

            row, col = middle // n, middle % n

            if target == matrix[row][col]:
                return True
            elif target > matrix[row][col]:
                left = middle + 1
            else:
                right = middle - 1

        return False
```

**Note:** 注意矩阵为空的情况哦~