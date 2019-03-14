---
title: LeetCode_Gas Station
date: 2019-03-14 15:52:22
categories: LeetCode
tags: 
  - medium
  - greedy
---

## [Gas Station](https://leetcode.com/problems/gas-station/)

There are N gas stations along a circular route, where the amount of gas at station i is gas[i]. You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations. Return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1.
（加油站问题）

<!--more-->

**Note:**
1. If there exists a solution, it is guaranteed to be unique.
2. Both input arrays are non-empty and have the same length.
3. Each element in the input arrays is a non-negative integer.

**Example:** 

<div align=center>
	<img src="/images/leetcode_134.png" width = "500" align=center/>
</div>

### 1. 贪心算法
这是一道很直接的贪心的题目，题中要求在一个环形的轨道中选择一个出发点，使得在路途中的经历耗油、加油可以成功的会到出发点。起点 start 将路径分为前后两段，前段总的余量为负，即油不够用，要想有解，那么后段油量应该为正，此时才可能有解，我们要做的就是找到这个分割点作为起点，然后再验证一下；反之，如果前段就为正了，那么显然可以直接选择前面的点为起点；如果整段加起来都是负的，那么无解。具体实现过程如下：

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        total, remain, start = 0, 0, 0
        
        for i in range(len(gas)):
            remain += gas[i] - cost[i]
            total += gas[i] - cost[i]
            if remain < 0:
                start = i + 1
                remain = 0

        if total < 0:
            return -1
        return start
```
