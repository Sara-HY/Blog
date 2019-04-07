---
title: LeetCode_Dungeon Game
date: 2019-04-07 17:43:22
categories: LeetCode
tags: 
  - hard
  - binary search
  - dynamic programming
---

## [Dungeon Game](https://leetcode.com/problems/dungeon-game/)

The demons had captured the princess (P) and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of M x N rooms laid out in a 2D grid. Our valiant knight (K) was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.
（勇士解救公主需要的最低能量）

<!--more-->

In order to reach the princess as quickly as possible, the knight decides to move **only rightward or downward** in each step. Write a function to determine the knight's minimum initial health so that he is able to rescue the princess.

**Example:** 

For example, given the dungeon below, the initial health of the knight must be at least 7 if he follows the optimal path `RIGHT-> RIGHT -> DOWN -> DOWN`.


<div align=center>
	<img src="/images/leetcode_174.png" width = "300" align=center/>
</div>


### 1. 动态规划
为了保证勇士能够顺利到达公主的位置，所以每个位置的最低能量值都是1。从矩阵的右下角出发不断往回回溯，需要每个方格需要的最小能量值。具体的动态规划递推表达式如下：

```python
class Solution:
    def calculateMinimumHP(self, dungeon: List[List[int]]) -> int:
        m, n = len(dungeon), len(dungeon[0])
        dp = [[0]* (n) for _ in range(m)]
        
        for i in range(m-1, -1, -1):
            for j in range(n-1, -1, -1):
                if i == m-1 and j == n-1:
                    dp[i][j] = max(1, 1 - dungeon[i][j])
                elif i == m-1:
                    dp[i][j] = max(1, dp[i][j+1] - dungeon[i][j])
                elif j == n-1:
                    dp[i][j] = max(1, dp[i+1][j] - dungeon[i][j])
                else:
                    dp[i][j] = max(1, min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j])
    
        return dp[0][0]
```