---
title: LeetCode_Word Search
date: 2019-02-23 14:51:49
ategories: LeetCode
tags: 
  - medium
  - array
  - back tracking
---

## [Word Search](https://leetcode.com/problems/word-search/)

Given a 2D board and a word, find if the word exists in the grid. The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.
（矩阵中进行词语搜索）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_79.png" width = "500" align=center/>
</div>

### 1. 回溯法 / DFS





```python
class Solution:
    def dfs(self, i, j, word):
        if word == '':
            return True
        tmp = self.board[i][j]
        self.board[i][j] = '0'
        
        if i>0 and self.board[i-1][j] == word[0]:
            if self.dfs(i-1, j, word[1:]):
                return True
        if j>0 and self.board[i][j-1] == word[0]:
            if self.dfs(i, j-1, word[1:]):
                return True
        if i<len(self.board)-1 and self.board[i+1][j] == word[0]:
            if self.dfs(i+1, j, word[1:]):
                return True
        if j<len(self.board[0])-1 and self.board[i][j+1] == word[0]:
            if self.dfs(i, j+1, word[1:]):
                return True
        
        self.board[i][j] = tmp
        return False 
        
    def exist(self, board: List[List[str]], word: str) -> bool:
        if not word:
            return True
        
        if not board or not board[0]:
            return False
        
        self.board = board
        for i in range(len(self.board)):
            for j in range(len(self.board[0])):
                if self.board[i][j] == word[0]:
                    if self.dfs(i, j, word[1:]):
                        return True
        return False
```