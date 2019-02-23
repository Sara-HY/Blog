---
title: LeetCode_Largest Rectangle in Histogram
date: 2019-02-23 16:51:00
categories: LeetCode
tags: 
  - hard
  - array
  - stack
---

## [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.
（在条形图中取最大矩形面积）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_83.png" width = "500" align=center/>
</div>

### 1. 堆栈
维护一个栈来存储升序序列，当遇到当前 height 小于栈顶 height 时，考虑计算。以栈顶的高度为高，栈顶 index 到 i-1 为宽的矩形。其中在pop过程中栈顶为空时，则需要将其维护为 “-1”，因为当 stack 为空时，说明数组中的最小值（所有高度中的最小值已经pop出来了，因此前面的所有都可以算作面积）。其时间复杂度为O(n)，空间复杂度为O(n)。具体实现过程如下：

**Note:**
1. 在 heights 尾部增加一个 “0” 是为了防止在数组尾部的最后一个升序序列没有计算，如[3, 4, 1, 3, 5, 7]。
2. stack 存储的是 index 是为了方便计算矩形的 width。


```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        stack = []
        result = 0
        heights.append(0)
        for i, height in enumerate(heights):
            while len(stack) > 0 and height < heights[stack[-1]]:
                top = stack.pop()
                if len(stack) == 0:
                    start = -1
                else:
                    start = stack[-1]
                result = max(result, heights[top] * (i-1-start))
            stack.append(i)
        
        return result
```