---
title: LeetCode_N-Queens
date: 2019-01-09 15:26:07
categories: LeetCode
tags: 
  - hard
  - back tracking
---

## [N-Queens](https://leetcode.com/problems/n-queens/)

The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.
(N皇后的问题)

<div align=center>
	<img src="/images/leetcode_51_1.png" width = "200" align=center/>
</div>

<!--more-->

Given an integer n, return all distinct solutions to the n-queens puzzle. Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.

**Example:**

<div align=center>
	<img src="/images/leetcode_51.png" width = "500" align=center/>
</div>


### 1. 回溯法
类似于这种解空间可以用树表示，且存在某种约束条件的问题可以用回溯法求解。具体实现过程如下：

```python
import copy

class Solution:
	def check(self, _i, _j):
		for i in range(self.n):
			for j in range(self.n):
				if self.matrix[i][j] == 'Q':
					if j == _j or abs(_i - i) == abs(_j - j):
						return False
		return True

	def dfs(self, i):
		if (i == self.n):
			self.count += 1
			result = []
			for row in self.matrix:
				result.append(''.join(row))
			self.result.append(result)
		else:
			for j in range(self.n):
				if self.check(i, j):
					self.matrix[i][j] = 'Q'
					self.dfs(i+1)
					self.matrix[i][j] = '.'
	
	def solveNQueens(self, n):
		"""
		:type n: int
		:rtype: List[List[str]]
		"""
		self.n = n
		self.result = []
		self.count = 0

		self.matrix = [['.' for _ in range(self.n)] for _ in range(self.n)]

		self.dfs(0)
		return self.result
```





