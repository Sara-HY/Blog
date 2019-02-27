---
title: LeetCode_Unique Binary Search Trees
date: 2019-02-27 16:44:58
categories: LeetCode
tags: 
  - medium
  - tree
  - dynamic programming
---

## [Unique Binary Search Trees](https://leetcode.com/problems/unique-binary-search-trees/)

Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1 ... n.
（有效二叉查找(排序)树个数）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_96.png" width = "500" align=center/>
</div>

### 1. 动态规划
这道题实质上是 **卡塔兰数** 的一个实例。具体递推过程如下：

```c++
                           1                    n = 1
        
                        2      1                n = 2
                       /        \
                   	  1          2

            1          3     3      2      1    n = 3
              \       /     /      / \      \
               3     2     1      1   3      2
              /     /       \                 \
            2      1         2                 3
```
1. n=0 时，dp[0] = 1
2. n=1 时，dp[1] = 1
3. n=2 时，dp[2] = dp[0]\*dp[1] + dp[1]\*dp[0] （以1为根 + 以2为根）
4. n>=2 时，dp[n] = dp[0]\*dp[n-1] + dp[1]\*dp[n-2] + ... + dp[n-1]\*dp[0] 

```python
class Solution:
    def numTrees(self, n: int) -> int:
        dp = [0 for _ in range(n+1)]
        dp[0], dp[1] = 1, 1
        
        for i in range(2, n+1):
            for j in range(i):
                dp[i] += dp[j] * dp[i-j-1]
        
        return dp[n]
```

