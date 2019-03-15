---
title: LeetCode_Max Points on a Line
date: 2019-03-15 20:27:00
categories: LeetCode
tags: 
  - hard
  - hash table
  - math
---

## [Max Points on a Line](https://leetcode.com/problems/max-points-on-a-line/)

Given n points on a 2D plane, find the maximum number of points that lie on the same straight line.
（坐标系中共线最多的点数）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_149.png" width = "500" align=center/>
</div>

### 1. 哈希表 + 穷举
对每个点都计算一下该点和其他点连线的斜率，这样对于这个点来说，相同斜率的直线有多少条，就意味着有多少个点在同一条直线上。用哈希表，以斜率为key，记录有多少重复直线。但是通过斜率来判断共线需要用到除法，而用double表示的双精度小数在有的系统里不一定准确，为了更加精确无误的计算共线，我们应当避免除法，而使用约分之后的分数表示（记录分子分母）。具体实现过程如下：

```python
# Definition for a point.
# class Point(object):
#     def __init__(self, a=0, b=0):
#         self.x = a
#         self.y = b

from collections import defaultdict
class Solution(object):
    def maxPoints(self, points):
        """
        :type points: List[Point]
        :rtype: int
        """
        # 最大公约数
        def gcd(a, b):
            if b == 0:
                return a
            else:
                return gcd(b, a % b)
            
        result = 0
        for i in range(len(points)):
            k_map = defaultdict(int)
            duplicate_point = 1
            for j in range(i+1, len(points)):
                if points[i].x == points[j].x and points[i].y == points[j].y:
                    duplicate_point += 1
                    continue
                dx = points[j].x - points[i].x
                dy = points[j].y - points[i].y
                d = gcd(dx, dy)
                k_map[(dx/d, dy/d)] += 1
            result = max(result, duplicate_point)
            
            for k in k_map:
                result = max(result, k_map[k] + duplicate_point)
    
        return result
```
