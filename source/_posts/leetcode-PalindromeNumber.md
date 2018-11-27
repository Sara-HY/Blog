---
title: LeetCode_Palindrome Number
date: 2018-11-26 21:56:36
categories: LeetCode
tags: 
  - easy
  - math
---

## [Palindrome Number](https://leetcode.com/problems/palindrome-number/)

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.
（判断数字是否是回文序列）

<!--more-->

**Example:**

<div align=center>
	<img src="/images/leetcode_9.png" width = "500" align=center/>
</div>


### 字符串翻转

```
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        string  = str(x)
        
        return string == string[::-1]
```