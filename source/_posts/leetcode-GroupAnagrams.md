---
title: LeetCode_Group Anagrams
date: 2019-01-09 14:48:18
categories: LeetCode
tags: 
  - medium
  - string
  - hash table
---

## [Group Anagrams](https://leetcode.com/problems/group-anagrams/)

Given an array of strings, group anagrams together.
(将使用相同字符构成的不同排列的单词合并)

<!--more-->

**Note:** 
1. All inputs will be in lowercase.
2. The order of your output does not matter.


**Example:**
<div align=center>
	<img src="/images/leetcode_49.png" width = "500" align=center/>
</div>


### 1. 哈希表 / Dict 
遍历数组中的每一个单词，将每个单词根据所组成的字符排序从而得到哈希表的key。具体实现过程如下：

```python
class Solution:
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        
        word_map = {}
        for word in strs:
            items = list(word)
            items.sort()
            items = ''.join(items)
            if items not in word_map:
                word_map[items] = [word]
            else:
                word_map[items].append(word)

        result = []
        for key in word_map:
            result.append(word_map[key])

        return result
```
