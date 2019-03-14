---
title: LeetCode_Candy
date: 2019-03-14 17:57:31
categories: LeetCode
tags: 
  - hard
  - greedy
---

## [Candy](https://leetcode.com/problems/candy/)

There are N children standing in a line. Each child is assigned a rating value. You are giving candies to these children subjected to the following requirements:
1. Each child must have at least one candy.
2. Children with a higher rating get more candies than their neighbors.

What is the minimum candies you must give?
（分糖问题）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_135.png" width = "500" align=center/>
</div>

### 1. 贪心算法 (两次遍历)

根据题意要求按权重分糖，每个人至少有一个糖，有较高权重的必须比相邻的人有更多的糖。第一遍从左向右遍历，如果右边的权重大，等加一个糖果，这样保证了一个方向上高权重的糖果多。然后再从右向左遍历一遍，如果相邻两个左边的等级高，而左边的糖果又少的话，则左边糖果数为右边糖果数加一。时间复杂度为O(n)，空间复杂度为O(n)。具体实现过程如下：

```python
class Solution:
    def candy(self, ratings: List[int]) -> int:
        n = len(ratings)
        nums = [1 for _ in range(n)]
                
        for i in range(1, n):
            if ratings[i] > ratings[i-1]:
                nums[i] = nums[i-1] + 1
        
        for i in range(n-2, -1, -1):
            if ratings[i] > ratings[i+1]:
                nums[i] = max(nums[i+1]+1, nums[i])
        
        return sum(nums)
```

