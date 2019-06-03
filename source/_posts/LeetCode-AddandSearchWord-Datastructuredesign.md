---
title: LeetCode_Add and Search Word - Data structure design
date: 2019-06-03 17:20:25
ategories: LeetCode
tags: 
  - medium
  - backtracking
  - design
  - trie
---

## [Add and Search Word - Data structure design](https://leetcode.com/problems/add-and-search-word-data-structure-design/)

Design a data structure that supports the following two operations. `search(word)` can search a literal word or a regular expression string containing only letters `a-z` or `.`.  `.` means it can represent any one letter.
（设计一种数据结构支持正则查询）

```bash
void addWord(word)
bool search(word)
```

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_211.png" width = "500" align=center/>
</div>

### 1. 回溯法
由于包含正则项的匹配，使用回溯法，回溯法一般通过 DFS 完成，具体实现过程如下：

```python
import collections

class Node:
    def __init__(self):
        self.children = collections.defaultdict(Node)
        self.is_word = False

class WordDictionary:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = Node()

    def addWord(self, word: str) -> None:
        """
        Adds a word into the data structure.
        """
        current = self.root
        for w in word:
            current = current.children[w]
        current.is_word = True
    
    def dfs(self, current, word, i):
        if i == len(word):
            return current.is_word
        w = word[i]
        if w == '.':
            for child in current.children:
                if current.children[child] and self.dfs(current.children[child], word, i+1):
                    return True 
            return False
        else:
            if not current.children.get(w):
                return False
            else:
                return self.dfs(current.children[w], word, i+1)  
            
    def search(self, word: str) -> bool:
        """
        Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
        """
        return self.dfs(self.root, word, 0)
            
# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```