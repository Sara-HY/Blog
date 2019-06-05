---
title: LeetCode_House Robber II
date: 2019-06-05 11:42:03
categories: LeetCode
tags: 
  - medium
  - dynamic programming
---

## [House Robber II](https://leetcode.com/problems/house-robber-ii/)

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.
（圆环数组中不相邻数组成的和最大）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_213.png" width = "500" align=center/>
</div>


### 1. 动态规划
这道题是之前那道 House Robber 的拓展，但是现在房子排成了一个圆圈，则如果抢了第一家，就不能抢最后一家，因为首尾相连了，所以第一家和最后一家只能抢其中的一家，或者都不抢，那我们这里变通一下，如果我们把第一家和最后一家分别去掉，各算一遍能抢的最大值，然后比较两个值取其中较大的一个即为所求。那我们只需参考之前的 House Robber 中的解题方法，然后调用两边取较大值，具体实现过程如下：

```python
class Solution:
    def rob_list(self, nums):
        before_before, before = 0, 0
        for i in range(0, len(nums)):
            temp = before
            before = max(before_before + nums[i], before)
            before_before = temp
            
        return max(before_before, before)
    
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]
        
        left_max = self.rob_list(nums[1:])
        right_max = self.rob_list(nums[:-1])
                
        return max(left_max, right_max)
```