---
title: LeetCode_Reverse Bits
date: 2019-04-16 20:30:21
categories: LeetCode
tags: 
  - easy
  - bit manipulation
---

## [Reverse Bits](https://leetcode.com/problems/reverse-bits/)

Reverse bits of a given 32 bits unsigned integer.
（翻转2进制无符号数表示）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_190.png" width = "500" align=center/>
</div>

### 1. 转换为字符串
将输入的数值用format函数转换为32位的二进制的形式，然后翻转后再转换为2进制即可。具体实现如下：

```python
class Solution:
    # @param n, an integer
    # @return an integer
    def reverseBits(self, n):
        string_n = '{:032b}'.format(n)
        return int(string_n[::-1], 2)
```

**Note:** 这里可以总结的是`format`函数可以转换进制并表示，这里的`b`表示二进制，`032`表示32位表示，不足的位置补0。


### 2. 位操作
按位操作，将数值的2进制表示从右向左逐渐加载`result`的后面。具体实现过程如下：

```python
class Solution:
    # @param n, an integer
    # @return an integer
    def reverseBits(self, n):
        result = 0
        for i in range(32):
            result <<= 1
            result |= (n&1)
            n >>= 1
        return result
```
