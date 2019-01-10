---
title: LeetCode_Spiral Matrix
date: 2019-01-10 18:00:36
categories: LeetCode
tags: 
  - medium
  - array
---

## [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.
（螺旋式遍历矩阵）

<!--more-->

**Example:**

<div align=center>
	<img src="/images/leetcode_54.png" width = "500" align=center/>
</div>

### 1. 方向模拟
实现定义四个方向，按照题中的螺旋式的方向在遍历矩阵过程中遇到边界时不断的修改方向并，修改新的边界。具体实现过程如下：

```python
class Solution:
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        if not matrix:
            return []
        
        m = len(matrix)
        n = len(matrix[0])

        direction = {
            'right': [0, 1],
            'down': [1, 0],
            'left': [0, -1],
            'up': [-1, 0]
        }

        answer = []
        i, j = 0, 0
        direct = 'right'
        left_border, right_border, up_border, down_border = 0, n-1, 0, m-1

        while len(answer) < m * n:
            answer.append(matrix[i][j])

            if i==up_border and j==right_border and direct=='right':
                direct = 'down'
                up_border += 1
            elif i==down_border and j==right_border and direct=='down':
                direct = 'left'
                right_border -= 1
            elif i==down_border and j==left_border and direct=='left':
                direct = 'up'
                down_border -= 1
            elif i==up_border and j==left_border and direct=='up':
                direct = 'right'
                left_border += 1 
            i += direction[direct][0]
            j += direction[direct][1]

        return answer
```

### 2. zip函数
在看别人的简单解法中发现用zip不断地旋转矩阵，每次都获得矩阵的第一行就是螺旋式遍历的结果。具体实现方法如下：

```python
class Solution:
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        answer = []
        while matrix:
            answer += matrix.pop(0)
            matrix = [*zip(*matrix)][::-1]
        return answer
```



