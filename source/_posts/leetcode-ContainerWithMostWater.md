---
title: LeetCode_Container With Most Water
date: 2018-11-28 11:20:13
categories: LeetCode
tags: 
  - medium
  - array
  - pointer
---

## [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.
（求最大矩形面积）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_11.png" width = "500" align=center/>
</div>


### 1. 暴力轮循
双层循环遍历得到所有可能的矩形的面积。很显然，该算法会 Time Limit Exceeded。其时间复杂度为 \\(O(n^2)\\)。具体实现过程如下：

```python
class Solution:
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        area = 0
        n = len(height)
        for j in range(n):
            for i in range(j):
                height_min = min(height[i], height[j])
                area = max(area, height_min*(j-i))
                
        return area
```

### 2. 头尾指针
在数组的收尾分别维护一个指针，过程中将高度较低的指针向中间移动。其时间复杂度为 \\(O(n)\\)。具体实现过程如下：

```python
class Solution:
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        area = 0
        p_left = 0
        p_right = len(height) - 1
        
        while p_left < p_right:
            area = max(area, min(height[p_left], height[p_right]) * (p_right - p_left))
            if height[p_left] < height[p_right]:
                p_left += 1
            else:
                p_right -= 1
                
        return area
```