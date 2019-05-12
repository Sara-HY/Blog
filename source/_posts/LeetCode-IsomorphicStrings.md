---
title: LeetCode_Isomorphic Strings
date: 2019-05-12 14:39:04
categories: LeetCode
tags: 
  - easy
  - hash table
---

## [Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings/)

Given two strings s and t, determine if they are isomorphic. Two strings are isomorphic if the characters in s can be replaced to get t. All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.
（判断是否为同构字符串）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_205.png" width = "500" align=center/>
</div>


### 1. 哈希表
用哈希表保存相同字符的index。具体实现过程如下：

```python
from collections import defaultdict 

class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        if not s:
            return True
        
        map_s, map_t = defaultdict(list), defaultdict(list)
        
        for i in range(len(s)):
            map_s[s[i]].append(i)
            map_t[t[i]].append(i)
            
            if map_s[s[i]] != map_t[t[i]]:
                return False

        return True
```


### 2. zip & 集合
首先判断组成两个字符串的字符的数目是否相同，然后使用 `zip` 函数判断字符串相同位置的字符组合是否相同。具体实现过程如下：

```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        if(len(set(zip(s,t)))==len(set(s))==len(set(t))): 
        	return True
        else: 
        	return False
```