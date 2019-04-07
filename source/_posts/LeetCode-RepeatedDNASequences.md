---
title: LeetCode_Repeated DNA Sequences
date: 2019-04-07 22:52:11
categories: LeetCode
tags: 
  - medium
  - hash table
  - bit manipulation
---

## [Repeated DNA Sequences](https://leetcode.com/problems/repeated-dna-sequences/)

All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA. Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.
（找出字符串中长度为10的重复出现的子串）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_187.png" width = "500" align=center/>
</div>

### 1. 哈希表

遍历字符串，记录每个长度为10的子串出现的次数，具体实现过程如下:

```python
from collections import defaultdict

class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        substring_dict = defaultdict(int)
        
        for i in range(len(s) - 9):
            substring_dict[s[i:i+10]] += 1
            
        return [string for string in substring_dict if substring_dict[string] > 1]
```