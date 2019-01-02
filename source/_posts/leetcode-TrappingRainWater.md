---
title: LeetCode_Trapping Rain Water
date: 2018-12-26 11:00:07
categories: LeetCode
tags: 
  - hard
  - array
  - two pointers
  - stack
---

## [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.
（收集雨水）

<!--more-->

**Example:**

<div align=center>
	<img src="/images/leetcode_42.png" width = "500" align=center/>
</div>

根据这个例子我们发现途中的蓝色的方块为6个，即最多蓄水位6。

### 两个指针
蓄水实质上是找从左到右或者从右到左高度下降的地方：
设定左右指针 left 和 right，max_left, max_right 分别记录从左到右和从右到左的最大值。
1. 假设 max_left <= max_right，这时我们从左边向右边看，蓄水值为 max_left - height[left]，更新左指针；
2. 在 max_left > max_right，这时我们从右边向左边看，蓄水值为 max_right - height[right]，更新右指针；

最终在 left 和 right 指针相遇时，退出循环，返回所有位置存储水的总量。具体实现过程如下：

```python
class Solution:
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        if not height:
            return 0
       
        result = 0

        max_left, max_right = 0, 0
        left, right = 0, len(height)-1
        while left < right:
            max_left = max(height[left], max_left)
            max_right = max(height[right], max_right)
            
            if max_left <= max_right:
                result += (max_left - height[left])
                left += 1
            else:
                result += (max_right - height[right])
                right -= 1
                
        return result
```