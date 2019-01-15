---
title: LeetCode_Rotate Image
date: 2019-01-09 14:08:24
categories: LeetCode
tags: 
  - medium
  - back tracking
---

## [Rotate Image](https://leetcode.com/problems/rotate-image/)

You are given an nxn 2D matrix representing an image. Rotate the image by 90 degrees (clockwise).
(顺时针旋转矩阵90度)

<!--more-->

**Note:** You have to rotate the image **in-place**, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.


**Example:**
<div align=center>
	<img src="/images/leetcode_48.png" width = "500" align=center/>
</div>


### 1. 矩阵转置 + 翻转行
为了在不使用额外空间的情况下实现矩阵的顺时针旋转，可将其变化转变为矩阵的转置，然后对每一行进行翻转。具体实现过程如下：

```python
class Solution:
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)

        for i in range(n):
            for j in range(i, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
            for j in range(n//2):
                matrix[i][j], matrix[i][n-1-j] = matrix[i][n-1-j], matrix[i][j]
            # matrix[i][:] = matrix[i][::-1]
```