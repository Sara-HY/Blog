---
title: LeetCode_Single Number II
date: 2019-03-14 18:40:44
categories: LeetCode
tags: 
  - medium
  - bit manipulation
---

## [Single Number II](https://leetcode.com/problems/single-number-ii/)

Given a non-empty array of integers, every element appears three times except for one, which appears exactly once. Find that single one.
（只出现一次的数字(其余出现三次)）

<!--more-->

**Note:** Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example:** 

<div align=center>
	<img src="/images/leetcode_137.png" width = "500" align=center/>
</div>

### 1. 按位操作
ones / twos / threes 表示将数组中所有整形数转为二进制后，每个位上1出现次数为1/2/3次的情况；

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        ones, twos, threes = 0, 0, 0
        
        for num in nums:
            twos |= ones & num
            ones ^= num
            threes = twos & ones
            # 当ones和twos中的某一位同时为1时表示二进制1出现3次，此时需要清零。
            ones &= ~threes
            twos &= ~threes
        
        return ones
```

### 2. 使用Python库Counter

```python
from collections import Counter

class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        nums_map = dict(Counter(nums))
        
        for num in nums_map:
            if nums_map[num] == 1:
                return num
```