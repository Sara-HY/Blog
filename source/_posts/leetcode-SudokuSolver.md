---
title: LeetCode_Sudoku Solver
date: 2018-12-21 21:42:03
categories: LeetCode
tags: 
  - hard
  - hash table
  - back tracking
---

## [Sudoku Solver](https://leetcode.com/problems/sudoku-solver/)

Write a program to solve a Sudoku puzzle by filling the empty cells.
（求解数独盘）

<!--more-->

A sudoku solution must satisfy all of the following rules:

1. Each of the digits 1-9 must occur exactly once in each row.
2. Each of the digits 1-9 must occur exactly once in each column.
3. Each of the the digits 1-9 must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.
4. Empty cells are indicated by the character '.'.

**Note:**
1. The given board contain only digits 1-9 and the character '.'.
2. You may assume that the given Sudoku puzzle will have a single unique solution.
3. The given board size is always 9x9.

**Example:** 
<div align=center>
	<img src="/images/leetcode_36_1.png" width = "300" align=center/>
</div>

<div align=center>
	<img src="/images/leetcode_37.png" width = "300" align=center/>
</div>


### 1. 回溯法 Back Tracking
求解数独、八皇后等等都是一个很经典的应用回溯法（深度优先搜索 + 剪枝）的例子。主要分为三个部分：
1. 寻找下一层节点，此处为find_next_empty()。
2. 判断限制条件，此处为check_constraint()。
3. 针对找到的节点继续进行 DFS, 如果已经满足要求则返回True，否则继续判断并不满足要求则回溯，此处为back_track()。

```python
class Solution:
	# find the next entry need to fill
	def find_next_empty(self):
		for row in range(0, 9):
			for col in range(0, 9):
				if self.board[row][col] == '.':
					return [row, col]
		return False

	# check the constraint 
	def check_constraint(self, x, y, num):
		# check row
		for data in self.board[x]:
			if data == num:
				return False
		# check col
		for data in list(zip(*self.board))[y]:
			if data == num:
				return False
		# check square
		square_row = x // 3 * 3
		square_col = y // 3 * 3
		datas = []
		for i in range(3):
			datas += self.board[square_row + i][square_col: square_col + 3]
		for data in datas:
			if data  == num:
				return False
		return True

	def back_track(self):
		entry = self.find_next_empty()
		if entry == False:
			return True
		else:
			[row, col] = entry
			# DFS
			for i in range(1, 10):
				check = self.check_constraint(row, col, str(i))
				# pruning
				if check:
					self.board[row][col] = str(i)
					re = self.back_track()
					# back tracking
					if not re:
						self.board[row][col] = '.'
					else:
						return True
						
			return False	
						
	def solveSudoku(self, board):
		"""
		:type board: List[List[str]]
		:rtype: void Do not return anything, modify board in-place instead.
		"""
		self.board = board
		self.back_track()
```