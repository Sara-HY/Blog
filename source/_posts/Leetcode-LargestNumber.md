---
title: LeetCode_Largest Number
date: 2019-04-07 21:29:11
categories: LeetCode
tags: 
  - medium
  - sort
---

## [Largest Number](https://leetcode.com/problems/largest-number/)

Given a list of non negative integers, arrange them such that they form the largest number.
（字符串拼接在一起为最大数）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_179.png" width = "500" align=center/>
</div>


### 1. sort & key

看到这个题目最直观的想法是将这些数字首先按照最高位排序，然后是第二高位，依次排序下去。由于每个数字长度不确定，如何进行排序也不是很明确。因此看到了题目给的解法是重载了`sort`函数的参数`key`的类中的`__le__`函数。（因为sort默认的是升序排列，所以只需要重载`__le__`即可）

具体实现过程如下：

```python
class LargeNumKey(str):
    def __lt__(x, y):
        return x+y > y+x

class Solution:
    def largestNumber(self, nums: List[int]) -> str:
        largest_num = "".join(sorted(map(str, nums), key=LargeNumKey))
        
        return '0' if largest_num[0] == '0' else largest_num
``` 