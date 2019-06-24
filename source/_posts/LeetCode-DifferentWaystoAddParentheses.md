---
title: LeetCode_Different Ways to Add Parentheses
date: 2019-06-24 09:31:04
categories: LeetCode
tags: 
  - medium
  - divide and conquer
---

## [Different Ways to Add Parentheses](https://leetcode.com/problems/different-ways-to-add-parentheses/)

Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are +, - and \*.
（不同的加括号方式使得运算结果不一致）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_241.png" width = "500" align=center/>
</div>

### 1. 分治法
这道题比较直观的是使用分治法分别解决符号的左边和右边的计算结果。其中需要单独考虑的是当字符串中不存在符号时，应该直接返回该字符串的表示的数值。其中，也可以在开始实现使用 `isdigit()` 判断。具体实现过程如下：

```python
class Solution:
    def diffWaysToCompute(self, input: str) -> List[int]:
        if len(input) == 1:
            return [int(input)]
        # if input.isdigit():
        #     return [int(input)]

        results = []
        for i, c in enumerate(input):
            if c in '+-*':
                for a in self.diffWaysToCompute(input[:i]):
                    for b in self.diffWaysToCompute(input[i+1:]):
                        if c == '+':
                            results.append(a+b) 
                        elif c == '-':
                            results.append(a-b)
                        else:
                            results.append(a*b)
        # 当字符串中不存在符号时，应该直接返回该字符串的表示的数值
        if not results:
            return [int(input)]
        return results
```