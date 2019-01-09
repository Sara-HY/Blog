---
title: LeetCode_Jump Game II
date: 2019-01-09 11:14:52
categories: LeetCode
tags: 
  - hard
  - array
  - dynamic programming
  - greedy
---

## [Jump Game II](https://leetcode.com/problems/jump-game-ii/)

Given an array of non-negative integers, you are initially positioned at the first index of the array. Each element in the array represents your maximum jump length at that position. Your goal is to reach the last index in the minimum number of jumps.
(跳棋游戏II)

<!--more-->

**Note:**
 You can assume that you can always reach the last index.

**Example:**
<div align=center>
	<img src="/images/leetcode_45.png" width = "500" align=center/>
</div>


### 1. 动态规划
从后向前遍历数组，根据 i+1 ~ nums[i]+i 需要跳的步数来得到当前需要跳的最小步数。具体实现如下：
**Note:** 特别需要注意的是在 nums 数组中为 0 的情况，需要单独考虑，否则上述的数组子集为空。

```python
class Solution:
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        jumps = [0 for _ in range(n)]

        for i in range(n-2, -1, -1):
            if nums[i] == 0:
                jumps[i] = n + 1 
            elif nums[i] + i >= n-1:
                jumps[i] = jumps[n-1] + 1 
            else:
                jumps[i] = min(jumps[i+1: i + nums[i] + 1]) + 1
       
        return jumps[0]
```

### 2. 贪心算法
题目中说明了所有测试数据都有解，而且不需要知道具体的是如何到达最后一格的。可以通过贪心的思想从左向右遍历，每次都可获得到目前为止可以到达的最远的位置 curr_max_index；在遍历过程中，若当前的位置 i 超过了上一次跳动得到的最远的的位置 last_max_index ，则增加跳动的步数。具体实现过程如下：

```python
class Solution:
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        step = 0
        last_max_index = 0
        curr_max_index = 0

        for i in range(len(nums)):
            if (i > last_max_index):
                step += 1
                last_max_index = curr_max_index
            curr_max_index = max(curr_max_index, nums[i] + i)

        return step
```