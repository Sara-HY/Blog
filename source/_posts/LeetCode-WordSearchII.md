---
title: LeetCode_Word Search II
date: 2019-06-05 10:42:36
categories: LeetCode
tags: 
  - hard
  - back tracking
  - trie
---

## [Word Search II](https://leetcode.com/problems/word-search-ii/)

Given a 2D board and a list of words from the dictionary, find all words in the board. Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.
（矩阵中进行一组词语搜索）

<!--more-->

**Example:** 

<div align=center>
    <img src="/images/leetcode_212.png" width = "500" align=center/>
</div>

### 1. 回溯法 / DFS
根据 `Word Search` 中的方法，可以直接对数组中的每一个 word 都进行一次 DFS，但是这样会造成很大的时间复杂度 O(K\*M\*N\*M\*N)（K 表示词语个数，M 为矩阵行数， N 为矩阵列数）。因此，可以考虑使用字典树首先来表示这 K 个 word，这样可以一次的找出所有的 word。具体实现过程如下：

```python
import collections

class TireNode(object):
    def __init__(self):
        self.children = collections.defaultdict(TireNode)
        self.is_word = False

class Tire(object):
    def __init__(self):
        self.root = TireNode()

    def add(self, word):
        current = self.root

        for w in word:
            current = current.children[w]
        current.is_word = True

    def search(self, word):
        current = self.root
        
        for w in word:
            current = current.children.get(w)
            if not current:
                return False
        return current.isword

class Solution:
    def dfs(self, board, p_word_trie, results, word, m, n, i, j):
        if i < 0 or i >= m or j < 0 or j >= n:
            return

        w = board[i][j]
        board[i][j] = '0'
        word += w

        current = p_word_trie.children.get(w)
        if current:
            if current.is_word:
                results.add(word)
            self.dfs(board, current, results, word, m, n, i-1, j)
            self.dfs(board, current, results, word, m, n, i+1, j)
            self.dfs(board, current, results, word, m, n, i, j-1)
            self.dfs(board, current, results, word, m, n, i, j+1)

        board[i][j] = w
        word = word[:-1]


    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        if not words:
            return []

        if not board or not board[0]:
            return []

        word_tire = Tire()
        for word in words:
            word_tire.add(word)

        results = set()
        m, n = len(board), len(board[0])
        for i in range(m):
            for j in range(n):
                self.dfs(board, word_tire.root, results, '', m, n, i, j)
    
        return list(results)
```