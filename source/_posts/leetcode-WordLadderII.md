---
title: LeetCode_Word Ladder II
date: 2019-03-13 16:57:41
categories: LeetCode
tags: 
  - hard
  - array
  - string
  - back tracking
  - bfs
---

## [Word Ladder II](https://leetcode.com/problems/word-ladder-ii/)

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

### 1. BFS + DFS + BackTracking
下面这个解法最终并没有成功AC，主要就是超时(Time Limit Exceeded)的问题。先根据 BFS 找到最短的转换次数，然后在 DFS 进行求解的过程中将解法超过最短的转换次数的剪枝。具体实现过程如下：

```python
class Solution:
    def minladderLength(self, beginWord):
        queue = [(beginWord, 1)]
        visited = [beginWord]
        while queue:
            word, step = queue.pop(0)
            if word == self.endWord:
                return step
            for i in range(len(word)):
                word_pattern = word[:i] + '*' + word[i+1:]
                if word_pattern in self.word_map:
                    for _word in self.word_map[word_pattern]:
                        if _word not in visited:
                            queue.append((_word, step+1))
                            visited.append(_word)
        return 0
    
    def back_tracking(self, res, visited):
        if len(res) > self.min_step:
            return 
        word = res[-1]
        if word == self.endWord:
            self.results.append(res)
        for i in range(len(word)):
            word_pattern = word[:i] + '*' + word[i+1:]
            if word_pattern in self.word_map:
                for _word in self.word_map[word_pattern]:
                    if _word != word and _word not in visited:
                        visited.append(_word)
                        self.back_tracking(res + [_word], visited)
                        visited.remove(_word)
                    
    def findLadders(self, beginWord: str, endWord: str, wordList: List[str]) -> List[List[str]]:
        if not wordList or endWord not in wordList:
            return []
     
        self.word_map = {}
        for word in wordList:
            for i in range(len(word)):
                word_pattern = word[:i] + '*' + word[i+1:]
                if word_pattern not in self.word_map:
                    self.word_map[word_pattern] = [word]
                else:
                    self.word_map[word_pattern].append(word) 
        
        
        self.endWord = endWord
        self.min_step = self.minladderLength(beginWord)
        self.results = []
        self.back_tracking([beginWord], [beginWord])
         
        return self.results
```

### 2. BFS + DFS + BackTracking
下面这个方案是参照别人的解法，改进的地方就是**在BFS的过程中，记录每个访问过的word距离beginWord的距离**，显然 dis[beginword]=0, dis[endword]=minstep-1。然后逆向DFS(从终止点开始)，对于每个每个即将要拓展的点最短路径必然满足的条件是：dis[word] + pathsize = minstep。具体实现过程如下：

```python
class Solution:
    def minladderLength(self, beginWord):
        queue = [(beginWord, 1)]
        visited = [beginWord]
        while queue:
            word, step = queue.pop(0)
            if word == self.endWord:
                return step
            for i in range(len(word)):
                word_pattern = word[:i] + '*' + word[i+1:]
                if word_pattern in self.word_map:
                    for _word in self.word_map[word_pattern]:
                        if _word not in visited:
                            self.dis[_word] = step    # get the distance to the begin word
                            queue.append((_word, step+1))
                            visited.append(_word)
        return 0
    
    def back_tracking(self, res, visited):
        if len(res) > self.min_step:
            return 
        
        word = res[0]
        # confirm the second word in the path
        if len(res) == self.min_step-1 and self.dis[word] == 1:
            self.results.append([self.beginWord] + res)
        
        for i in range(len(word)):
            word_pattern = word[:i] + '*' + word[i+1:]
            if word_pattern in self.word_map:
                for _word in self.word_map[word_pattern]:
                    if _word != word and _word not in visited:
                    	# 剪枝 
                        if _word not in self.dis or self.dis[_word] + len(res) > self.min_step:
                            continue
                        else:
                            visited.append(_word)
                            self.back_tracking([_word] + res, visited)
                            visited.remove(_word)
                    
    def findLadders(self, beginWord: str, endWord: str, wordList: List[str]) -> List[List[str]]:
        if not wordList or endWord not in wordList:
            return []
     
        self.word_map = {}
        for word in wordList:
            for i in range(len(word)):
                word_pattern = word[:i] + '*' + word[i+1:]
                if word_pattern not in self.word_map:
                    self.word_map[word_pattern] = [word]
                else:
                    self.word_map[word_pattern].append(word) 
        
        
        self.endWord = endWord
        self.beginWord = beginWord
        self.dis = {}
        self.dis[beginWord] = 0
        self.min_step = self.minladderLength(beginWord)
        self.results = []
        self.back_tracking([endWord], [endWord])
         
        return self.results
```


### 3. BackTracking
另一种比较简单的做法，从 beginWord 出发，逐一修改 beginWord 中的字符，将第一次出现在 wordList 的词维护一个map保存，按同样的方式遍历这些词语直到找到 endWord。 然后从 endWord 出发逆向 DFS，具体实现过程如下：

```python
from collections import defaultdict
from string import ascii_lowercase

class Solution:                   
    def findLadders(self, beginWord: str, endWord: str, wordList: List[str]) -> List[List[str]]:
        dictionary = set(wordList)
        result, cur, visited, found, trace = [], [beginWord], set([beginWord]), False, defaultdict(list)

        while cur and not found:
            for word in cur:
                visited.add(word)

            next = set()
            for word in cur:
                for i in range(len(word)):
                    for c in ascii_lowercase:
                        candidate = word[:i] + c + word[i + 1:]
                        if candidate not in visited and candidate in dictionary:
                            if candidate == endWord:
                                found = True
                            next.add(candidate)
                            trace[candidate].append(word)
            cur = next

        if found:
            self.backtrack(result, trace, [], endWord)

        return result

    def backtrack(self, result, trace, path, word):
        if not trace[word]:
            result.append([word] + path)
        else:
            for prev in trace[word]:
                self.backtrack(result, trace, [word] + path, prev)
```

**Note:** 这里dictionary = set(wordList)很重要，不然也会超时(Time Limit Exceeded)。set和lsit可以自由转换，在删除list中多个/海量重复元素时，可以先转换成set，然后再转回list并排序(set没有排序)，此种方法不仅方便且效率较高。
