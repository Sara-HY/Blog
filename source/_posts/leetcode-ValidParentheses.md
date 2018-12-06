---
title: LeetCode_Valid Parentheses
date: 2018-12-06 15:44:13
categories: LeetCode
tags: 
  - easy
  - string
  - stack
---

## [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
（判断有效的括号对）

<!--more-->

An input string is valid if:
 - Open brackets must be closed by the same type of brackets.
 - Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example:** 

<div align=center>
	<img src="/images/leetcode_20.png" width = "500" align=center/>
</div>

### 1. 栈匹配
括号的匹配问题是一个很直观的栈的应用问题。具体实现过程如下：

```python
class Solution:
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        
        stack = []
        mapping = {')': '(', ']': '[', '}': '{'}
        
        for ch in s:
            if ch in mapping:
                top = stack.pop() if stack else '#'
                if top != mapping[ch]:
                    return False
            else:
                stack.append(ch)
                
        return not stack
```

### 2. 栈匹配
后来看别人的解答过程中有一种更直观简单的栈匹配过程。具体实现过程如下：

```python
class Solution:
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        for c in s:
            if c == '[':
                stack.append(']')
            elif c == '{':
                stack.append('}')
            elif c == '(':
                stack.append(')')
            elif not stack or c != stack.pop():
                return False
        return not stack
```