---
title: LeetCode_Valid Palindrome
date: 2019-03-13 15:12:56
categories: LeetCode
tags: 
  - easy
  - string
  - two pointers
---

## [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.
（回文字符串）
<!--more-->

**Note:** For the purpose of this problem, we define empty string as valid palindrome.

**Example:** 

<div align=center>
	<img src="/images/leetcode_125.png" width = "500" align=center/>
</div>

### 1. 双指针
两个指针分别指向字符串的首尾，查到符合要求的字符时就判断两者是否相同。具体实现过程如下：

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        if not s:
            return True
        
        n = len(s)
        i, j = 0, n-1
        
        s = s.lower()
        while i<j:
            # 需要注意保证i，j的有效性
            while i<n and not s[i].isalnum():
                i+=1
            while j>=0 and not s[j].isalnum():
                j-=1
            if i<=j and s[i] != s[j]:
                return False
            i+=1
            j-=1
                
        return True
```



