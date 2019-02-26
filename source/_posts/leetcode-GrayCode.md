---
title: leetcode_Gray Code
date: 2019-02-25 22:49:34
categories: LeetCode
tags: 
  - medium
  - binary
  - back tracking
---

## [Gray Code](https://leetcode.com/problems/gray-code/)

The gray code is a binary numeral system where two successive values differ in only one bit. Given a non-negative integer n representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.
(n位格雷码)

<!--more-->

**Example:**

<div align=center>
	<img src="/images/leetcode_89.png" width = "500" align=center/>
</div>

### 1. 二进制码转换为格雷码
二进制转换为 Gray码：右移一位并与自身异或。
如 n=2 时，binary=[00, 01, 10, 11], 
	        gray=[00^00, 00^01, 01^10, 01^11]=[11, 01, 11, 10]，即[0, 1, 3, 2]。

```python
class Solution:
    def grayCode(self, n: int) -> List[int]:
        results = []
        for i in range(pow(2, n)):
            results.append((i >> 1) ^ i)
        
        return results
```

### 2. 格雷码的镜面排列
1. n=0时，gray=[0]
2. n=1时，add_gray=[0] + 2^0, gray=[0, 1]
3. n=2时，add_gray=[1, 0] + 2^1, gray=[0, 1, 3, 2]
...

```python
class Solution:
    def grayCode(self, n: int) -> List[int]:
        results = [0]
        for i in range(n):
            results += [x+2**i for x in reversed(results)]
        
        return results
```


