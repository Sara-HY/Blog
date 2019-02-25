---
title: LeetCode_Maximal Rectangle
date: 2019-02-25 10:56:42
ategories: LeetCode
tags: 
  - hard
  - array
  - hash table
  - dynamic programming
  - stack
---

## [Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/)

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
(最大矩形)

<!--more-->

**Follow up:**

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

**Example:**

<div align=center>
	<img src="/images/leetcode_85.png" width = "500" align=center/>
</div>

### 1. 问题转换 & 栈
基于上一题，**Largest Rectangle in Histogram**，我们可以考虑将这题中的求最大矩形面积转换为直方图中的求最大矩形的面积。通过遍历矩阵的每一行，将矩阵中纵列 “1” 的序列长度表示为直方图的高度，也就是我们求 m 个直方图中的最大矩形面积。具体实现过程如下：

```python
class Solution:
    def maximalRectangle(self, matrix: List[List[str]]) -> int:
        if not matrix or not matrix[0]:
            return 0
        n = len(matrix[0])
        height = [0] * (n + 1)
        ans = 0
        for row in matrix:
            for i in range(n):
                height[i] = height[i] + 1 if row[i] == '1' else 0
            stack = [-1]
            for i in range(n + 1):
                while height[i] < height[stack[-1]]:
                    h = height[stack.pop()]
                    w = i - 1 - stack[-1] 
                    ans = max(ans, h * w)
                stack.append(i)
        return ans
```

### 2. 动态规划 
这道题的动态规划的算法方面不太好理解，不能直接用二维动规来解决问题。具体实现过程如下：

```python
class Solution:
    def maximalRectangle(self, matrix: 'List[List[str]]') -> 'int':
        if not matrix or not matrix[0]:
            return 0
        m, n = len(matrix), len(matrix[0])
   
   		# 对每一行进行计算, 递推公式如下:
   		#    每一行开始时,左边界 left 定为0, 右边界 right 定为n
   		#    height[j]好算:
   		#        如果matrix[i][j] = 0, height[j] = 0
   		#        如果matrix[i][j] = 1, height[j]++
   		#    left[j]从左往右算:
   		#        如果matrix[i][j] = 0, left[j]=0, 同时cur_left变为当前j+1(因为潜在的左边界可能就在j+1)
   		#        如果matrix[i][j] = 1, left[j]= max(left[j], cur_left), 哪个大取哪个.
   		#        (解释: 因为我们要的是过往所有行中0到该列位置最晚遇到1的位置)
   		#    right[j]从右往左算:
   		#        如果matrix[i][j] = 0, right[j]=n, 同时cur_right变为当前j(因为潜在的右边界就在当前j位置)
   		#        如果matrix[i][j] = 1, right[j]= min(right[j], cur_right), 哪个小取哪个.
   		#        (解释: 因为我们要的是过往所有行中COL-1到该列位置最早遇到0的位置)
        left = [0 for _ in range(n)]
        right = [n for _ in range(n)]
        height = [0 for _ in range(n)]
        
        max_res = 0
        for i in range(m):
            cur_left = 0
            cur_right = n
            for j in range(n):
                if  matrix[i][j] == '1':
                    height[j] += 1
                    left[j] = max(left[j], cur_left)
                else:
                    height[j] = 0
                    left[j] = 0
                    cur_left = j + 1
            for j in range(n-1, -1, -1):
                if matrix[i][j] == '1':
                    right[j] = min(right[j], cur_right)
                else:
                    right[j] = n
                    cur_right = j
            for j in range(n):
                max_res = max(max_res, (right[j] - left[j]) * height[j])
        return max_res
```
