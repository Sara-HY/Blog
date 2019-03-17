---
title: LeetCode_Reverse Words in a String
date: 2019-03-17 21:41:28
categories: LeetCode
tags: 
  - medium
  - string
---

## [Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)

Given an input string, reverse the string word by word.
（翻转字符串中的词语）

<!--more-->


**Note:**
1. A word is defined as a sequence of non-space characters.
2. Input string may contain leading or trailing spaces. However, your reversed string should not contain leading or trailing spaces.
3. You need to reduce multiple spaces between two words to a single space in the reversed string.


**Example:** 

<div align=center>
	<img src="/images/leetcode_151.png" width = "500" align=center/>
</div>


### 1. 字符串函数
使用 `split join [::-1]` 等常用的字符串换处理函数，具体实现过程如下：

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        return " ".join(word for word in s.split(' ')[::-1] if word)
```








