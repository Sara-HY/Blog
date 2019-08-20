---
title: Algorithm_Knapsack Problem
date: 2019-08-10 09:51:21
categories: Algorithm
tags: 
  - knapsack
  - back_tracking
  - greedy
  - dynamic programming
---

## [Knapsack Problem](https://zh.wikipedia.org/wiki/%E8%83%8C%E5%8C%85%E9%97%AE%E9%A2%98)

背包问题

<!--more-->

背包问题（Knapsack problem）是一种组合优化的 NP 完全问题。问题可以描述为：给定一组物品，每种物品都有自己的重量和价格，在限定的总重量内，我们如何选择才能使得物品的总价格最高。

### 1. 背包问题

这个问题是指每个物体的可以拆分，即可以得到单位重量的价值，最终要求选择后的结果使得物品的总价格最高，这种问题最后背包一定会放满，使用贪心算法。具体实现过程如下:

```python
weights = [3, 4, 8, 5]
values = [7, 4, 3, 8]
C = 10

n = len(weights)

value_per_weights = [(values[i]/weights[i], weights[i]) for i in range(n)]
value_per_weights.sort(key=lambda x: x[0], reverse=True)

results = [0] * n
for i in range(n):
    if value_per_weights[i][1] > C:
        break
    results[i] = 1
    C -= value_per_weights[i][1]

if i < n:
    results[i] = C / value_per_weights[i][1]

for value_per_weight, result in zip(value_per_weights, results):
    print(value_per_weight[1], result)
```


### 2. 01背包问题

01背包问题是指每个物体都有且只有一个（即选或不选），最终要求选择后的结果使得物品的总价格最高，这种问题最后背包不一定会放满，使用动态规划算法。具体实现过程如下：

f[n][C] 表示容量 C 是否可以放置前 i 个物品。

f[i][j] = max( f[i-1][j-weights[i]] + values[i] if j>=weights[i],  f[i-1][j])

```python
weights = [3, 4, 8, 5]
values = [7, 4, 3, 8]
C = 10

n = len(weights)
dp = [[0] * (C+1) for _ in range(n+1)]

for i in range(1, n+1):
    for j in range(C+1):
        dp[i][j] = max(dp[i][j], dp[i-1][j])
        if weights[i-1] <= j:
            dp[i][j] = max(dp[i][j], dp[i-1][j-weights[i-1]]+values[i-1])

return dp[n][C]
```

### 3. 非01背包问题

非01背包问题是指每个物体都有很多个(无限个)，最终要求选择后的结果使得物品的总价格最高。具体实现过程如下：

```python
weights = [3, 4, 8, 5]
values = [7, 4, 3, 8]
C = 10

n = len(weights)
dp = [[0] * (C+1) for _ in range(n+1)]

for i in range(1, n+1):
    for j in range(C+1):
        k = 0
        while k*weights[i-1] <= j:
            dp[i][j] = max(dp[i][j], dp[i-1][j-k*weights[i-1]]+k*values[i-1])
            k += 1

return max(map(max, dp))

```

### 4. 变种之选硬币问题

给定一些物品数组和一个目标值，问有多少种可以组成目标的组合数，比如给定物品数组 [2,3,6,7] 和目标值 7 （2种可能）。可以考虑使用动态规划：
dp[n][C] 表示从前i中里面组成 C 的组合数，则
dp[n][C] = dp[n-1][C] + dp[n-1][C-values[n-1]\* 1] + dp[n-1][C-values[n-1]\* 2] + ...


```python
values = [2, 3, 6, 7]
C = 7

n = len(values)
dp = [[0] * (C+1) for _ in range(n+1)]

dp[0][0] = 1
for i in range(1, n+1):
    for j in range(C+1):
        k = 0
        while k*values[i-1] <= j:
            dp[i][j] += dp[i - 1][j - k * values[i - 1]];
            k += 1

return dp[n][C]

```





