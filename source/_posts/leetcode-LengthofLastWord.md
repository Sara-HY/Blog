---
title: LeetCode_Length of Last Word
date: 2019-01-13 15:15:22
categories: LeetCode
tags: 
  - easy
  - string
---

## [Length of Last Word](https://leetcode.com/problems/length-of-last-word/)

Given a string s consists of upper/lower-case alphabets and empty space characters “ ”, return the length of last word in the string. If the last word does not exist, return 0.
（字符串最后一个单词的长度）

<!--more-->

**Note:**
A word is defined as a character sequence consists of non-space characters only.

**Example:**
<div align=center>
	<img src="/images/leetcode_58.png" width = "500" align=center/>
</div>


### 1. 字符串处理
本题考查`python`中基本的字符串处理函数，比较简单。具体实现方法如下：
（其中之所以需要使用 `strip()` 是因为当字符串为 “a ” 时，最后一个单词应该是 "a"）

```python
class Solution:
    def lengthOfLastWord(self, s):
        """
        :type s: str
        :rtype: int
        """
        result = 0

        words = s.strip().split(' ')

        if len(words) == 0:
	        return 0
        else:
	        return len(words[-1])
```