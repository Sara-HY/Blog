---
title: LeetCode_Best Time to Buy and Sell Stock IV
date: 2019-04-10 21:06:01
categories: LeetCode
tags: 
  - hard
  - array
  - dynamic programming
---

## [Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)

Say you have an array for which the ith element is the price of a given stock on day i. Design an algorithm to find the maximum profit. You may complete **at most k** transactions.
（股票收益）

<!--more-->

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

**Example:** 

<div align=center>
    <img src="/images/leetcode_188.png" width = "500" align=center/>
</div>

### 1. 动态规划
结合前几次的买卖股票的问题，这次的区别在于交易的次数至多 k 次。如此一来，我们一定可以根据前交易 k-1 次的交易来推导出再增加一交易的最大收入，具体实现过程如下：


```python
class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        n = len(prices)
        if n < 2:
            return 0

        # k足够大，能够赢取所有的收益
        if k >= n // 2: 
            return sum(i - j for i, j in zip(prices[1:], prices[:-1]) if i - j > 0)

        # 在n天内进行k次交易的最大收益值
        global_max = [[0] * n for _ in range(k+1)] 
        
        for i in range(1, k+1):
            # n天内的最大收益
            local_max = [0] * n 

            for j in range(1, n):
                profit = prices[j] - prices[j-1]
                # 1. 在j-1天进行i-1次的最大收益 + 第j-1天买入&第j天卖掉的收益
                # 2. 在j-1天进行i-1次的最大收益 + 第j天买入&第j天卖掉的收益(0)
                # 3. 前j-1天的最大收益 + 第j-1天买入&第j天卖掉的收益
                local_max[j] = max(global_max[i-1][j-1] + profit, global_max[i-1][j-1], local_max[j-1]+profit)
                # 1. 在j-1天进行i次的最大收益 
                # 2. 前j天的最大收益
                global_max[i][j] = max(global_max[i][j-1], local_max[j])
        
        return global_max[-1][-1]
```