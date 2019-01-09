---
title: LeetCode_N-Queens II
date: 2019-01-09 22:06:26
categories: LeetCode
tags: 
  - hard
  - back tracking
---

## [N-Queens](https://leetcode.com/problems/n-queens/)

The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.
(N皇后的问题，求解个数)

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
与前一题方法相同，只需将具体的解法保存。具体实现过程如下：

```python
import copy

class Solution:
	def check(self, matrix, _i, _j):
		for i in range(self.n):
			for j in range(self.n):
				if matrix[i][j] == 'Q':
					if j == _j or abs(_i - i) == abs(_j - j):
						return False
		return True

	def dfs(self, i, matrix):
		if (i == self.n):
			self.count += 1
		else:
			for j in range(self.n):
				if self.check(matrix, i, j):
					matrix[i][j] = 'Q'
					self.dfs(i+1, matrix)
					matrix[i][j] = '.'
	
	def totalNQueens(self, n):
		"""
		:type n: int
		:rtype: List[List[str]]
		"""
		self.n = n
		self.count = 0

		matrix = [['.' for _ in range(self.n)] for _ in range(self.n)]

		self.dfs(0, matrix)
		return self.count
```