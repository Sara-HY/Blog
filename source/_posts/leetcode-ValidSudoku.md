---
title: LeetCode_Valid Sudoku
date: 2018-12-21 20:56:51
categories: LeetCode
tags: 
  - medium
  - hash table
---

## [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules.
（数独盘有效性判断）
<!--more-->
1. Each row must contain the digits 1-9 without repetition.
2. Each column must contain the digits 1-9 without repetition.
3. Each of the 9 `3x3` sub-boxes of the grid must contain the digits 1-9 without repetition.

<div align=center>
	<img src="/images/leetcode_36_1.png" width = "300" align=center/>
</div>

**Note:**
1. A Sudoku board (partially filled) could be valid but is not necessarily solvable.
2. Only the filled cells need to be validated according to the mentioned rules.
3. The given board contain only digits 1-9 and the character '.'.
4. The given board size is always 9x9.

**Example:** 

<div align=center>
	<img src="/images/leetcode_36.png" width = "500" align=center/>
</div>


### 1. 依次check
根据题中设定的要求逐一排查，一旦检测到不符合标准的部分就返回 False。

```python
class Solution:
    def isListValid(self, list):
        clean = [i for i in list if i != '.']
        s = set(clean)
        return len(s) == len(clean)
    
    def isValidSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: bool
        """
        
        # row check 
        for list in board:
            if self.isListValid(list) == False:
                return False
        
        # column check
        for list in zip(*board):
            if self.isListValid(list) == False:
                return False
            
        # square check
        for i in range(0, 9, 3):
            for j in range(0, 9, 3):
                list = [board[x][y] for x in range(i, i + 3) for y in range(j, j + 3)]
                if self.isListValid(list) == False:
                    return False
        return True
```


### 2. 使用Hash Map
只需要遍历一次矩阵，在遍历过程中保存每个的数值的行、列的index，并保存数值属于9个正方形中的哪一个（i//3, j//3）。具体实现过程如下：

```python
class Solution:
    def isValidSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: bool
        """
        
        dict = {}
        
        for i, row in enumerate(board):
            for j, ch in enumerate(row):
                if ch == '.':
                    continue
                if ch in dict:
                    result_index = dict[ch]
                    for index in result_index:
                        if index[0] == i or index[1] == j or index[2] == (i//3, j//3):
                            return False
                    dict[ch].append([i, j, (i//3, j//3)])
                else:
                    dict[ch] = [[i, j, (i//3, j//3)]]

        return True
```
















