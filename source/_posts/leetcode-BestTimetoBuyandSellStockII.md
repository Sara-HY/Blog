---
title: LeetCode_Best Time to Buy and Sell Stock II
date: 2019-03-12 23:01:05
categories: LeetCode
tags: 
  - easy
  - array
  - greedy
---

## [BBest Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

Say you have an array for which the ith element is the price of a given stock on day i. Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).
（股票收益）

<!--more-->

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

**Example:** 

<div align=center>
	<img src="/images/leetcode_122.png" width = "500" align=center/>
</div>

### 1. 单重循环
题中的意思是指可以进行多次买入卖出的操作，这个过程实际上也就是在每次股价要降低前卖出，在每次股价要上升时买入，因此只需要计算每次上升的过程中的的差价即可。具体实现过程如下：

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if not prices:
            return 0
        
        max_profit = 0
        for i in range(1, len(prices)):
            if prices[i] > prices[i-1]:
                max_profit += prices[i] - prices[i-1]
        
        return max_profit
```