---
title: LeetCode_Best Time to Buy and Sell Stock III
date: 2019-03-12 23:14:08
categories: LeetCode
tags: 
  - hard
  - array
  - dynamic programming
---

## [Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

Say you have an array for which the ith element is the price of a given stock on day i. Design an algorithm to find the maximum profit. You may complete **at most two** transactions. 
（股票收益）

<!--more-->

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

**Example:** 

<div align=center>
	<img src="/images/leetcode_123.png" width = "500" align=center/>
</div>

### 1. 动态规划
题中的意思是指可以进行至多两次买入卖出的操作。可以以 i 划分整个时间，根据Best Time to Buy and Sell Stock中最大只能买卖一次的算法计算[0,i]的最大收益以及[i,n]的最大收益。具体实现过程如下：

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if not prices:
            return 0
        
        n = len(prices)
        left = [0 for _ in range(n)]
        right = [0 for _ in range(n)]
        min_price, max_price = prices[0], prices[n-1]
        
        for i in range(1, n):
            left[i] = max(left[i-1], prices[i] - min_price)
            if prices[i] < min_price:
                min_price = prices[i]
            
            right[n-1-i] = max(right[n-i], max_price - prices[n-1-i])
            if prices[n-1-i] > max_price:
                max_price = prices[n-1-i]
        
        final_profit = 0
        for i in range(n):
            final_profit = max(final_profit, left[i] + right[i])
            
        return final_profit
```