---
title: LeetCode_Count and Say
date: 2018-12-24 18:15:52
categories: LeetCode
tags: 
  - easy
  - string
---

## [Count and Say](https://leetcode.com/problems/count-and-say/)

读字符串

<!--more-->

这个题目 LeetCode 给的解释和实例 really 让人难以理解。简单来说是这样的：
1. n = 1时，返回‘1’
2. n = 2时，由于 n-1 为1，且其对应的字符串为‘1’，读作 one 1， 则输出 ‘11’
3. n = 3时，由于 n-1 为2，且其对应的字符串为‘11’，读作 two 1， 则输出 ‘21’
3. n时，对n-1的对应的字符串读取的过程进行输出。

这很明显是一个递归的问题，先得到n-1对应的字符串，然后遍历字符串得到相应的读法并输出。具体实现过程如下：

### 1. 递归
```python
class Solution:
    def countAndSay(self, n):
        """
        :type n: int
        :rtype: str
        """
        if n == 1:
            return '1'

        last_string = self.countAndSay(n-1)

        match_char = last_string[0]
        match_count = 0

        result_string = ''

        for char in last_string:
            if char == match_char:
                match_count += 1
            else:
                result_string += str(match_count) + match_char
                match_char = char
                match_count = 1
        
        result_string += str(match_count) + match_char
        return result_string
```