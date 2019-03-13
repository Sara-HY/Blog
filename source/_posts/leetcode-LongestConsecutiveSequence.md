---
title: LeetCode_Longest Consecutive Sequence
date: 2019-03-13 20:34:47
categories: LeetCode
tags: 
  - hard
  - array
  - union find
---

## [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

Given an unsorted array of integers, find the length of the longest consecutive elements sequence. Your algorithm should run in O(n) complexity.
（时间复杂度为O(n)，乱序数组中找到最长连续的数列）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_128.png" width = "500" align=center/>
</div>

### 1. 哈希
使用 **set** 对数组进行hash，这样可以实现遍历数组时迅速定位，具体实现过程如下： 

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        s = set(nums)
        
        res = 0
        for i in range(len(nums)):
            if nums[i]-1 not in s:
                j = nums[i]
                while j in s:
                    j += 1
                res = max(res, j - nums[i])
        
        return res
```


### 2. 并查集

并查集是一种常用的解决**联通性**问题的一种数据结构。首先对数组中的每个数字建立 数->index 的映射，在映射过程中维护并查集将连续的数字的根节点合并，最终判断根节点最多的那一个也就是联通子图中的最大个数。具体实现方法如下：

```python
class Solution:
    def find(self, i):
        if self.parent[i] != -1:
            return self.find(self.parent[i])
        return i
    
    def union(self, i, j):
        root_i = self.find(i)
        root_j = self.find(j)
        self.parent[root_i] = root_j
    
    def longestConsecutive(self, nums: List[int]) -> int:
        n = len(nums)
        self.parent = [-1 for _ in range(n)]
        
        nums_map = {}
        for i in range(n):
            if nums[i] in nums_map:
                continue
    
            nums_map[nums[i]] = i
            if nums[i]-1 in nums_map:        
                self.union(i, nums_map[nums[i]-1])
            if nums[i]+1 in nums_map:
                self.union(i, nums_map[nums[i]+1])
        
        max_length = 0
        count = [0 for i in range(n)]
        for i in range(n):
            count[self.find(i)] += 1
            max_length = max(count[self.find(i)], max_length)
        
        return max_length
```
