---
title: LeetCode_Implement Trie (Prefix Tree)
date: 2019-06-03 09:50:42
categories: LeetCode
tags: 
  - medium
  - design
  - trie
---

## [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/)

Implement a trie with insert, search, and startsWith methods.
(实现字典树以及相关功能函数)

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_28.png" width = "500" align=center/>
</div>


### 字典树（前缀树）实现
需要注意的是，字典树的根节点不包含字符。

```python
import collections

class Node:
    def __init__(self):
        self.children = collections.defaultdict(Node)
        self.isword = False

class Trie:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = Node()
        
    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        current = self.root
        for w in word:
            current = current.children[w]
        current.isword = True

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        current = self.root
        for w in word:
            current = current.children.get(w)
            if not current:
                return False
        return current.isword
        
    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        current = self.root
        for w in prefix:
            current = current.children.get(w)
            if not current:
                return False
        return True

# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```
