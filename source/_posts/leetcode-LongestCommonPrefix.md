---
title: LeetCode_Longest Common Prefix
date: 2018-11-29 10:37:25
categories: LeetCode
tags: 
  - easy
  - string
---

## [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

Write a function to find the longest common prefix string amongst an array of strings. If there is no common prefix, return an empty string "". 
（寻找最长公共前缀序列）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_14.png" width = "500" align=center/>
</div>

### 1. 二分查找
将数组二分，分别查找其最长公共前缀序列，然后查找结果的最长公共前缀序列。具体实现过程如下：
```python
class Solution:
    def commonPrefixof2(self, str1, str2):
        result = ""
        n = min(len(str1), len(str2))
        for i in range(n):
            if str1[i] == str2[i]:
                result += str2[i]
            else:
                break
        return result    
        
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        result = '' 
        n = len(strs)
        
        if n == 0:
            return ""
        elif n == 1:
            return strs[0]
        elif n == 2:
            return self.commonPrefixof2(strs[0], strs[1])
        else: 
            result1 = self.longestCommonPrefix(strs[:n//2])
            result2 = self.longestCommonPrefix(strs[n//2:])
            return self.commonPrefixof2(result1, result2)
```

### 2. Zip函数 & Set
zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。具体实现过程如下：
```python
class Solution:
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """ 
        if not strs:
            return ""
        
        for i, word in enumerate(zip(*strs)):
            if len(set(word)) > 1:
                return strs[0][:i]

        return min(strs)
```


### 3. 字符子串组成Set
```python
class Solution:
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        n = len(strs)
        if n == 0:
            return ''
        elif n == 1:
            return strs[0]
        length = min([len(s) for s in strs])
        
        while length > 0:
            substrings = [s[:length] for s in strs]
            if len(set(substrings)) == 1:
                return substrings[0]
            length -= 1
        return ''
```