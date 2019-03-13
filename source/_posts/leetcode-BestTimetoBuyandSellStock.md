---
title: LeetCode_Best Time to Buy and Sell Stock
date: 2019-03-12 22:35:09
categories: LeetCode
tags: 
  - easy
  - array
  - dynamic programming
---

## [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

Say you have an array for which the ith element is the price of a given stock on day i. If you were only permitted to complete **at most one** transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit. Note that you cannot sell a stock before you buy one.
（股票收益）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_121.png" width = "500" align=center/>
</div>

### 1. 双重循环
类似于插入排序的方法，外层 i 从 [0,n-1） 循环，内层 j 从 [i+1, n） 循环，获取遍历过程中的最大值。


### 2. 单重循环 & 动态规划
只进行一次遍历，在遍历过程中发现价格小于买入的价格时，修改最低价表示买入；当收益大于最大收益时，修改最大收益值。（这里使用elif 是因为买入必须在卖掉之前。）具体实现过程如下：

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if not prices:
            return 0
        
        max_profit, min_price = 0, float('inf')
        
        for i in range(len(prices)):
            if prices[i] < min_price:
                min_price = prices[i]
            elif prices[i] - min_price > max_profit:
                max_profit = prices[i] - min_price
        
        return max_profit
```