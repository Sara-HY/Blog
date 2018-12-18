---
title: LeetCode_Substring with Concatenation of All Words
date: 2018-12-18 18:21:13
categories: LeetCode
tags: 
  - hard
  - string
  - hash table
  - two pointers
---

## [Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)

You are given a string **s**, and a list of words **words**, that are all of the same length. Find all starting indices of substring(s) in s that is a concatenation of each word in words exactly once and without any intervening characters.
（找到字符串中所有的子串，其为字符串数组全排列形成）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_30.png" width = "500" align=center/>
</div>


### 1. 定长取字符串子串
这道题我们不应该想着将所有字符串数组中的字符串的排列组合，这将是一个 \\(O(n!)\\)算法；而应该从另一个角度出发，遍历字符串。

由于数组中的字符串的长度 sub_length 是一致的，组合后的字符串的总长 whole_length 也可以确定，因此我们遍历字符串时每次都取出长度为 whole_length 的子串，然后将其分为子串长度均为 sub_length  的子串集合，判断这个子串集合和题中的 **words** 是否一致，这里的判断就借用了dict / hash map 实现。

**Note**：
 1. 边界条件 s, words都为空时需要单独考虑，否则后面的计算没有意义。
 2. 边界条件 i。遍历字符串时应该让 i 取到 len(s) - whole_length + 1，若为 len(s) - whole_length 时， 最后一个 sub 将无法取到。 
 3. 字符串切分为等长的字符子串：subs = re.findall('.{'+str(sub_length)+'}', sub)

```python
import re
class Solution:
    def findSubstring(self, s, words):
        """
        :type s: str
        :type words: List[str]
        :rtype: List[int]
        """
        
        if len(words) == 0 or s == '':
            return []
        
        dict = {}
        for word in words:
            if word in dict:
                dict[word] += 1
            else:
                dict[word] = 1
        
        sub_length = len(words[0])
        whole_length = len(words) * sub_length
        
        result = []
        for i in range(len(s) - whole_length + 1):
            sub = s[i:i + whole_length]
            subs = re.findall('.{'+str(sub_length)+'}', sub)
    
            d = {}
            flag = 1
            for word in subs:
                if word not in dict:
                    flag = 0
                    break
                if word in d:
                    d[word] += 1
                else:
                    d[word] = 1
            if flag == 1:
                for item in d:
                    if d[item] != dict[item]:
                        flag = 0
                        break
            if flag == 1:
                result.append(i)
            
        return result 
```