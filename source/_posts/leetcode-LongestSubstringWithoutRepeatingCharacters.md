---
title: LeetCode_Longest Substring Without Repeating Characters
date: 2018-11-23 14:33:59
categories: LeetCode
tags: 
  - medium
  - string
  - hash table
  - dynamic programming
---

## [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Given a string, find the length of the longest substring without repeating characters.
（字符串中的最大不重复子串）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_3.png" width = "500" align=center/>
</div>


### 1. 暴力循环

对字符串进行两轮循环，并在循环的过程中判断两个指针之间的字符串是否包含了重复的字符。其时间复杂度为 \\(O(n^3)\\)。在测试过程中会 Time Limit Exceeded。

### 2. 移动窗口 / 动态规划

这道题是字符串中的很典型的 DP 问题。构建两个指针i和j，当指针j+1所指的元素在[i, j]中没有出现时，这时的字符串为[i, j+1]；当指针j+1所指的元素在[i, j]中有出现时，这时的字符串为[i+1, j]。另外，构建了一个字典来快速判断元素是否在子串中出现。其时间复杂度为 \\(O(2n)\\)。具体实现过程如下：

```
class Solution:
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        d = {}
        long = 0
        i = 0
        j = 0
        
        while(i < len(s) and j < len(s)):
            if (s[j] not in d) or (d[s[j]] == 0):
                d[s[j]] = 1
                j += 1
                long = max(long, j-i)
            else:
                d[s[i]] = 0
                i += 1 
        return long
```

上面那个方法需要对整个字符串遍历两次，另外一种思路就是在字典dict中保存的是字符最后一次出现的下一个元素。指针j来遍历整个字符串，指针i来维护[0, j]中所有字符中最后一次出现的下一个元素，于是[i, j]就是最大不重复子串。其时间复杂度为 \\(O(n)\\)。具体实现过程如下：

```
class Solution:
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        d = {}
        i = 0
        j = 0
        long = 0
        while j < len(s) :
            if s[j] in d and d[s[j]] > i:
                i = d[s[j]]
            else:
            	long = max(long, j - i + 1)
            d[s[j]] = j + 1
            j += 1
            
        return long
```

**注**： 测试的时候考虑字符串为空等临界条件。






