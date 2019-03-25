---
title: LeetCode_Compare Version Numbers
date: 2019-03-25 18:20:12
categories: LeetCode
tags: 
  - medium
  - string
---

## [Compare Version Numbers](https://leetcode.com/problems/compare-version-numbers/)

Compare two version numbers version1 and version2. If `version1 > version2` return 1; if `version1 < version2` return -1; otherwise return 0. You may assume that the version strings are non-empty and contain only digits and the . character. The . character does not represent a decimal point and is used to separate number sequences. 

For instance, 2.5 is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision. You may assume the default revision number for each level of a version number to be 0. For example, version number 3.4 has a revision number of 3 and 4 for its first and second level revision number. Its third and fourth level revision number are both 0.
（比较'.'分开的数值大小）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_165.png" width = "500" align=center/>
</div>

### 1. 字符串处理


```python
class Solution(object):
    def compareVersion(self, version1, version2):
        """
        :type version1: str
        :type version2: str
        :rtype: int
        """
        data1 = version1.split('.')
        data2 = version2.split('.')
        
        m, n = len(data1), len(data2)
        
        
        for i in range(min(m, n)):
            if int(data1[i]) > int(data2[i]):
                return 1
            elif int(data1[i]) < int(data2[i]):
                return -1
        
        if m == n:
            return 0
        if m > n:
            num = int(''.join(data1[n:]))
            if num:
                return 1
            else:
                return 0
        if m < n:
            num = int(''.join(data2[m:]))
            if num:
                return -1
            else:
                return 0   
```