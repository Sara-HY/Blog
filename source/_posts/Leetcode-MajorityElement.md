---
title: Leetcode_Majority Element
date: 2019-04-07 15:16:32
categories: LeetCode
tags: 
  - easy
  - array
  - divide and conquer 
  - bit manipulation
  - hash map
---

## [Majority Element](https://leetcode.com/problems/majority-element/)

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times. You may assume that the array is non-empty and the majority element always exist in the array.
(众数（次数大于n/2）)

<!--more-->

**Example:**

<div align=center>
	<img src="/images/leetcode_169.png" width = "500" align=center/>
</div>

### 1. 哈希表
构建一个哈希表来保存数组，统计每个元素的个数。也就是实现函数`collections.Counter(nums)`的功能。具体实现过程如下：

```python
from collections import defaultdict, Counter

class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        num_map = defaultdict(int)
        max_num, max_count = None, 0
        for num in nums:
            num_map[num] += 1
            if num_map[num] > max_count:
                max_num, max_count = num, num_map[num]
        
        return max_num
        # counts = Counter(nums)
        # return max(counts.keys(), key=counts.get)
```

### 2. 排序
由于此处的众数的定义为出现频次超过 n/2 的元素，因此先将数组进行排序，然后第 n/2 个元素一点就是“众数”。具体实现过程如下:

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        nums.sort()
        return nums[len(nums) // 2]
```
