---
title: LeetCode_Set Matrix Zeroes
date: 2019-02-16 21:13:21
categories: LeetCode
tags: 
  - medium
  - array
---

## [Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)

Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in-place.
（设置矩阵整行&列为0）

<!--more-->

**Example:**

<div align=center>
	<img src="/images/leetcode_73.png" width = "500" align=center/>
</div>

### 1. 遍历矩阵，集合维护“0”的行列号

```python
class Solution:
    def setZeroes(self, matrix: 'List[List[int]]') -> 'None':
        """
        Do not return anything, modify matrix in-place instead.
        """
        m, n = len(matrix), len(matrix[0])
        
        columns = set()
        rows = set()
        
        for i in range(m):
            for j in range(n):
                if matrix[i][j] == 0:
                    columns.add(j)
                    rows.add(i)
    
        for i in rows:
            # matrix[i] = [0]*n
            for j in range(n):
                matrix[i][j] = 0
        
        for j in columns:
            for i in range(m):
                matrix[i][j] = 0
```