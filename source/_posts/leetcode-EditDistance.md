---
title: LeetCode_Edit Distance
date: 2019-02-19 17:31:37
categories: LeetCode
tags: 
  - hard
  - string
  - dynamic programming
---

## [Edit Distance](https://leetcode.com/problems/edit-distance/)

Given two words word1 and word2, find the minimum number of operations required to convert word1 to word2.
（计算编辑距离）

<!--more-->

You have the following 3 operations permitted on a word:
1. Insert a character
2. Delete a character
3. Replace a character

**Example:**

<div align=center>
	<img src="/images/leetcode_72.png" width = "500" align=center/>
</div>


### 动态规划 时间复杂度 O(n^2) 空间间复杂度 O(n^2)
很明显的动态规划的题目，问题就在于需要分类讨论。具体的讨论情况在code的注释部分有详细解释。

```python
class Solution:
    def minDistance(self, word1: 'str', word2: 'str') -> 'int':
        len1 = len(word1)
        len2 = len(word2)
        
        # Create a table to store results of subproblems 
        dp = [[0 for _ in range(len1 + 1)] for _ in range(len2 + 1)]
        
        for i in range(len2 + 1):
            for j in range(len1 + 1):
            	# word1 is empty, insert all chars
                if i == 0:
                    dp[i][j] = j
                # word2 is empty, remove all chars
                elif j == 0:
                    dp[i][j] = i
                # last chars are same
                elif word2[i-1] == word1[j-1]:
                    dp[i][j] = dp[i-1][j-1]
                # last chars are different, min(insert, remove, replace)
                else:
                    dp[i][j] = 1 + min(dp[i][j-1], dp[i-1][j], dp[i-1][j-1])
                
        # return dp[len2][len1]
        return dp[-1][-1]
```

### 动态规划 时间复杂度 O(n^2) 空间间复杂度 O(n^2)

```python
class Solution:
    def minDistance(self, word1: 'str', word2: 'str') -> 'int':
        len1 = len(word1)
        len2 = len(word2)
        
        # Create a table to store results of subproblems 
        dp = [0 for _ in range(len2 + 1)] 
 
        for j in range(len2 + 1):
            dp[j] = j

        for i in range(1, len1 + 1):
            prev = i
            for j in range(1, len2 + 1):
                if word1[i-1] == word2[j-1]:
                    cur = dp[j-1]
                else:
                    cur = min(dp[j-1], dp[j], prev) + 1
                dp[j-1] = prev
                prev = cur  
            dp[len2] = prev
            
        return dp[len2]
```
