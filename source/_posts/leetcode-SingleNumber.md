---
title: LeetCode_Single Number
date: 2019-03-14 18:27:42
categories: LeetCode
tags: 
  - easy
  - hash table
  - bit manipulation
---

## [Single Number](https://leetcode.com/problems/single-number/)

Given a non-empty array of integers, every element appears twice except for one. Find that single one.
（只出现一次的数字）

<!--more-->

**Note:** Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example:** 

<div align=center>
	<img src="/images/leetcode_136.png" width = "500" align=center/>
</div>

### 1. 哈希表
使用哈希表保存数组，时间复杂度为O(n)，空间复杂度为O(n)。具体实现过程如下：

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        num_dict = {}
         
        for num in nums:
            if num not in num_dict:
                num_dict[num] = 1
            else:  
                 num_dict[num] += 1
        
        for key in num_dict:
            if num_dict[key] == 1:
                return key
```

### 2. 按位异或
题中要求使用时间复杂度为O(n)，空间复杂度为O(1)。在遍历数组的过程中使用按位异或的方法，最终会保留下只存在一次的数字。具体实现过程如下：

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        result = 0
        for num in nums:
            result ^=  num
        return result
```

