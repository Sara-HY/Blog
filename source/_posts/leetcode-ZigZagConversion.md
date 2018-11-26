---
title: LeetCode_Zig Zag Conversion
date: 2018-11-26 14:49:30
categories: LeetCode
tags: 
  - medium
  - string
---

## [ZigZag Conversion](https://leetcode.com/problems/zigzag-conversion/)

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this:
```
P   A   H   N
A P L S I I G
Y   I   R
```
And then read line by line: "PAHNAPLSIIGYIR".
（字符串ZIGZAG之后按行输出）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_6.png" width = "500" align=center/>
</div>

### 规律
根据ZigZag的规律，当行数为 numRows 时：
  - ZigZag的第 i 行字符的序号为 \\(k \* (2 \* numRows - 2) + i \\) ；
  - ZigZag的非第一行和最后一行的第 i 行的偶数个字符的序号是 \\((k + 1) \* (2 \* numRows - 2) - i \\)；
其时间复杂度为 \\(O(n)\\)，具体实现过程如下：
```
class Solution:
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
       
        if numRows == 1:
            return s
        
        result = ""
        n = len(s)
        add = 2 * numRows - 2 
        
        for i in range(numRows):
            for j in range(0, n-i, add):
                result += s[i+j]
                if (i != 0 and i != numRows-1 and j+add-i<n):
                    result += s[j+add-i]
        return result
```

**注**：这里需要特别注意的是保证 \\(add = 2 * numRows - 2\\) 的有效性，因此需要单独考虑 numRows 为1时的情况。


### 变步长遍历字符串
这是一个十分巧妙的思路，仅仅只需要遍历一次字符串。题目的本质可以理解为将字符串分成 numRows 组，然后再连接起来。但是在遍历字符串时，需要根据 ZigZag 的形式来回的遍历，但实质也只遍历了一次。其时间复杂度为 \\(O(n)\\)，具体实现过程如下：
```
class Solution:
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        n = len(s)
        if numRows == 1 or numRows >= n:
            return s
        
        group_list = [""] * numRows

        index = 0
        step = 1
        for char in s:
            group_list[index] += char
            
            if index == 0:
                step = 1
            elif index == numRows - 1:
                step = -1
            index += step
           
        return "".join(group_list)

```

















