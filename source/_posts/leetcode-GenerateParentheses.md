---
title: LeetCode_Generate Parentheses
date: 2018-12-07 16:33:33
categories: LeetCode
tags: 
  - medium
  - string
  - backtracking
---

## [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.
（n 对括号所有组合形式）

<!--more-->

**Example:** 
For example, given n = 3, a solution set is:

<div align=center>
	<img src="/images/leetcode_22.png" width = "500" align=center/>
</div>


### 1. 递归 & 深度优先搜索
这个题目是一个很直观的括号对序列的问题，问题的实质就是在每次添加新的括号时： **任何位置的之前的 NUM_( >= NUM_)**。

```python
class Solution:
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        result = []
        
        def generateParenthesis(left_remain, right_remain, s):
            if left_remain == 0 and right_remain == 0:
                result.append(s)
            if left_remain > 0:
                generateParenthesis(left_remain-1, right_remain, s + '(')
            if right_remain > 0 and left_remain < right_remain:
                generateParenthesis(left_remain, right_remain-1, s + ')')
            
        generateParenthesis(n, n, '')
        
        return result
```

### 2. 动态规划
经过观察发现如下：
  - n==0, result = ['']
  - n==1, result = [
  	() = ( + result_0 + ) + result_0
  ]
  - n==2, result = [
  ()() = ( + result_0 + ) + result_1()
  (()) = ( + result_1() + ) + result_0
  ]
  - n==3, result = [
  ()()() = ( + result_0 + ) + result_2_1()()
  ()(()) = ( + result_0 + ) + result_2_2(())
  (())() = ( + result_1() + ) + result_1()
  (()()) = ( + result_2_1()() + ) + result_0
  ((())) = ( + result_2_2(()) + ) + result_0
  ]
因此我们可以得出如下结论：
  - dp[n] = [( + x + ) + y for x in dp[j] for y in dp[i - j - 1]] , j in range(i)。

```python
class Solution:
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        dp = [[] for i in range(n+1)]

        dp[0].append('')
        for i in range(n + 1):
        	for j in range(i):
        		 dp[i] += ['(' + x + ')' + y for x in dp[j] for y in dp[i - j - 1]]
            
        return dp[n]    
        
```