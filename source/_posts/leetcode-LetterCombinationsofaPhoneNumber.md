---
title: LeetCode_Letter Combinations of a Phone Number
date: 2018-11-30 20:28:46
categories: LeetCode
tags: 
  - medium
  - string
  - back tracking
---

## [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.
（根据九宫格键盘将数字映射到字符）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_17.png" width = "500" align=center/>
</div>

### 1. map / hash_table 进行索引
这个问题很直观就是建立一个map进行索引。在提交过程中，发现如果考虑了`digits == ''`的情况，时间大幅度降低。说明在这种测试情况下，多考虑一些极端情况，直接返回结果，会使得整体的测试时间减少很多。

```python
class Solution:
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        
        dict = {
            '2': ['a', 'b', 'c'],
            '3': ['d', 'e', 'f'],
            '4': ['g', 'h', 'i'],
            '5': ['j', 'k', 'l'],
            '6': ['m', 'n', 'o'],
            '7': ['p', 'q', 'r', 's'],
            '8': ['t', 'u', 'v'],
            '9': ['w', 'x', 'y', 'z']
        }
        
        result = []
        for ch in digits:
            letter = dict[ch]
            if len(result) == 0:
                result = letter
            else:
                new_result = []
                for a in result:
                    for b in letter:
                        new_result.append(a + b)
                result = new_result
                
        return result 
```