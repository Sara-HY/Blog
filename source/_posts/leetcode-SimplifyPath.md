---
title: LeetCode_Simplify Path
date: 2019-02-16 20:31:52
categories: LeetCode
tags: 
  - medium
  - string
  - stack
---

## [Simplify Path](https://leetcode.com/problems/simplify-path/)

Given an absolute path for a file (Unix-style), simplify it. Or in other words, convert it to the canonical path. In a UNIX-style file system, a period **.** refers to the current directory. Furthermore, a double period **..** moves the directory up a level. Note that the returned canonical path must always begin with a slash /, and there must be only a single slash / between two directory names. The last directory name (if it exists) **must not** end with a trailing /. Also, the canonical path must be the **shortest** string representing the absolute path.
（简化文件路径）

<!--more-->

**Example:**

<div align=center>
	<img src="/images/leetcode_71.png" width = "500" align=center/>
</div>

### 1. 堆栈

```python
class Solution:
    def simplifyPath(self, path: 'str') -> 'str':
        dirs = [x for x in path.split('/') if x and x != '.']

        results = []

        for dir in dirs:
            if dir == '..':
                results.pop() if results else None
            else:
                results.append(dir)

        return '/' + '/'.join(results)
```
