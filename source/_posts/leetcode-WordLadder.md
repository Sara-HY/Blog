---
title: LeetCode_Word Ladder
date: 2019-03-13 16:25:35
categories: LeetCode
tags: 
  - medium
  - bfs
---

## [Word Ladder](https://leetcode.com/problems/word-ladder/)

Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord.
（词语阶梯）
<!--more-->

**Note:** 
1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that beginWord is not a transformed word.
3. Return 0 if there is no such transformation sequence.
4. All words have the same length.
5. All words contain only lowercase alphabetic characters.
6. You may assume no duplicates in the word list.
7. You may assume beginWord and endWord are non-empty and are not the same.

**Example:** 

<div align=center>
	<img src="/images/leetcode_127.png" width = "500" align=center/>
</div>

### 1. 宽度优先搜索
根据题意实际上是找到从 beginWord 转换到 endWord 总共需要的步数。首先根据处理 wordList 将可以通过一次相互转换的 word 放入一个map中，根据bfs的过程遍历word所有可能的转换（经过转换的词语需要标记为visited）。具体实现过程如下：

```python
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        if not wordList or endWord not in wordList:
            return 0
     
        word_map = {}
        for word in wordList:
            for i in range(len(word)):
                word_pattern = word[:i] + '*' + word[i+1:]
                if word_pattern not in word_map:
                    word_map[word_pattern] = [word]
                else:
                    word_map[word_pattern].append(word)                
                
        queue = [(beginWord, 1)]
        visited = [beginWord]
        while queue:
            word, step = queue.pop(0)
            if word == endWord:
                return step
            for i in range(len(word)):
                word_pattern = word[:i] + '*' + word[i+1:]
                if word_pattern in word_map:
                    for _word in word_map[word_pattern]:
                        if _word not in visited:
                            queue.append((_word, step+1))
                            visited.append(_word)
        return 0
```

**Note:** 这里如果不事先处理 wordList 而是用 a-z 替换 word 中的字符回导致超时。 