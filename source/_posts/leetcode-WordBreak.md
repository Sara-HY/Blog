---
title: LeetCode_Word Break
date: 2019-03-14 21:11:32
categories: LeetCode
tags: 
  - medium
  - dynamic programming
---

## [Word Break](https://leetcode.com/problems/word-break/)

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.
（字符串是否可以有效分词）

<!--more-->

**Note:** 
1. The same word in the dictionary may be reused multiple times in the segmentation.
2. You may assume the dictionary does not contain duplicate words.

**Example:** 

<div align=center>
	<img src="/images/leetcode_139.png" width = "500" align=center/>
</div>

### 1. 动态规划
具体实现方法如下：

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        if s in wordDict:
            return True
        
        dp = [False for _ in range(len(s) +1)]
        dp[0] = [True]
        
        for i in range(1, len(s)+1):
            for j in range(i):
                if s[j:i] in wordDict and dp[j]:
                    dp[i] = True
            
        return dp[-1]
```