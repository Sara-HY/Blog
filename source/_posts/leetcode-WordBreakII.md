---
title: LeetCode_Word Break II
date: 2019-03-14 21:48:44
categories: LeetCode
tags: 
  - hard
  - dynamic programming
  - back tracking
  - hash table
---

## [Word Break II](https://leetcode.com/problems/word-break-ii/)

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, add spaces in s to construct a sentence where each word is a valid dictionary word. Return all such possible sentences.
（字符串有效分词）

<!--more-->

**Note:** 
1. The same word in the dictionary may be reused multiple times in the segmentation.
2. You may assume the dictionary does not contain duplicate words.

**Example:** 

<div align=center>
	<img src="/images/leetcode_140.png" width = "500" align=center/>
</div>

### 1. 动态规划 + 回溯法
下面这种解法只使用了回溯，最终会导致 Time Limit Exceeded。

```python
# Time Limit Exceeded
# s = "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaabaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"
# wordDict = ["a","aa","aaa","aaaa","aaaaa","aaaaaa","aaaaaaa","aaaaaaaa","aaaaaaaaa","aaaaaaaaaa"]
class Solution:
    def backtracking(self, s, res, start):
        if s[start:] in self.wordDict:
            self.results.append(" ".join(res + [s[start:]]))
           
        for i in range(start+1, len(s)):
            if s[start:i] in self.wordDict:
                self.backtracking(s, res+[s[start:i]], i)
                
    
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
        if not s:
            return []
        
        self.results = []
        self.wordDict = wordDict
        self.backtracking(s, [], 0)
        
        return self.results
```

因此需要结合动态规划首先进行判断再回溯，最终具体解法如下：
```python
class Solution:
    def wordBreak_check(self, s):
        if s in self.wordDict:
            return True
        
        dp = [False for _ in range(len(s) +1)]
        dp[0] = [True]
        
        for i in range(1, len(s)+1):
            for j in range(i):
                if s[j:i] in self.wordDict and dp[j]:
                    dp[i] = True
            
        return dp[-1]
    
    def backtracking(self, s, res, start):
        if s[start:] in self.wordDict:
            self.results.append(" ".join(res + [s[start:]]))
           
        for i in range(start+1, len(s)):
            if s[start:i] in self.wordDict:
                self.backtracking(s, res+[s[start:i]], i)
                
    
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
        self.wordDict = wordDict
        if not s or not self.wordBreak_check(s):
            return []
    
        self.results = [] 
        self.backtracking(s, [], 0)
        
        return self.results
```

### 1. 哈希表 + 回溯法
这里维护了一个哈希表保存之前对字符串已经处理过的映射关系，例如memo['sanddog'] = 'sand dog'这样就避免了重复多次计算。不会Time Limit Exceeded，具体实现方法如下：

```python
class Solution:
    def helper(self, s: str, wordDict: [str], memo: dict) -> [str]:
        if s in memo:
            return memo[s]
        res =[]
        if not s:
            return res
        for word in wordDict:
            if not s.startswith(word):
                continue
            if len(s) == len(word):
                res.append(word)
            else:
                rest = self.helper(s[len(word):], wordDict, memo)
                for tmp in rest:
                    tmp = word + ' ' + tmp
                    res.append(tmp)
        memo[s] = res
        return res
    
    def wordBreak(self, s: str, wordDict: [str]) ->[str]:
        memo = {}
        return self.helper(s, wordDict, memo)
```