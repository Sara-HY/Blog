---
title: LeetCode_Spiral Matrix II
date: 2019-01-13 15:31:44
categories: LeetCode
tags: 
  - medium
  - array
---

## [Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/)

Given a positive integer n, generate a square matrix filled with elements from 1 to n^2 in spiral order.
（螺旋式生成矩阵）

<!--more-->

**Example:**

<div align=center>
	<img src="/images/leetcode_59.png" width = "500" align=center/>
</div>

### 1. 方向模拟
事先定义四个方向，按照题中的螺旋式的方向在遍历矩阵，过程中遇到边界时不断的修改方向并修改新的边界。具体实现过程如下：
（与Spiral Matrix类似）

```python
class Solution:
    def generateMatrix(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        if n == 0:
            return []

        direct_map = {
            'right': [0, 1],
            'down': [1, 0],
            'left': [0, -1],
            'up': [-1, 0]
        }

        result = [[0]*n for _ in range(n)]
        left_border, right_border, up_border, down_border=0, n-1, 0, n-1
        fill = 1
        direction = 'right'
        i, j = 0, 0
        while fill <= n*n:
            result[i][j] = fill
            fill += 1
            if direction=='right' and j==right_border:
                direction = 'down'
                up_border += 1
            elif direction=='down' and i==down_border:
                direction='left'
                right_border -= 1
            elif direction=='left' and j==left_border:
                direction='up'
                down_border -= 1
            elif direction=='up' and i==up_border:
                direction='right'
                left_border += 1
            i += direct_map[direction][0]
            j += direct_map[direction][1]
        return result
```