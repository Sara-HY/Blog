---
title: Algorithm_Closest Pair of Points
date: 2019-06-30 15:27:59
categories: Algorithm
tags: 
  - divide and conquer
---

## Closest Pair of Points（平面最近点对）

<!--more-->
给定平面上n个点，找其中的一对点，使得在n个点的所有点对中，该点对的距离最小。

### 1. 暴力轮循

直接计算每两个点之间的距离，然后就可以确定距离最小的两个点。其时间复杂度为 O(n\*2)


### 2. 分治法
基本思路是将点集合平均分为两份，分别计算两个子集合中的最近点对。此方法重点在于分治算法的合并过程，即最近点对分别存在于两个集合中。其时间复杂度是 O(nlogn) ，具体算法步骤如下：
1. 对所有点从小到大排序，以 x 为第一关键词，y 为第二关键字；
2. 将所有点按 x = mid 坐标分成左右两部分；
3. 递归求解左右两部分中的最近距离，并取最小值min_d = min{min_left，min_right}；
4. 以 x = mid 划分 x = mid - min_d 和  x = mid + min_d 的区域，则若最近点对分别存在于两个集合中，必须在此范围内；
	1）其中对于在 [mid - min_d, mid] 的点 p(x_p, y_p)，不需要与所有 [mid, mid + min_d] 的点计算距离，而是 x in [mid, mid + min_d], y in [y_p - min_d, y_p + min_d] 范围内的点计算即可。
主要时间复杂度是排序的时间复杂度，即 O(nlogn)，具体实现过程如下：

```python
import math

class Point(object):
    """docstring for Point"""
    def __init__(self, x, y):
        self.x = x
        self.y = y

def point_distance(p, q):
    return math.sqrt(pow(p.x-q.x, 2) + pow(p.y-q.y, 2))

def candidatePoint(p, points, min_d, med_x):
    for q in points:
        if q.x < med_x - min_d:
            continue
        if q.x > med_x + min_d:
            break
        if q.y >= p.y-min_d and q.y <= p.y+min_d:
            yield q

def combine(points, n, min_d, med_x):
    final_min = min_d

    for p in points[:n//2]:
        if p.x < med_x - min_d:
            continue
        for q in candidatePoint(p, points[n//2:], min_d, med_x):
            final_min = min(point_distance(p, q), final_min)
           
    return final_min

def divide(points):
    n = len(points)
    if n <= 1:
        return float('inf')
    elif n == 2:
        return point_distance(points[0], points[1])
    else:
        points=sorted(points, key=lambda x:([x.x, x.y]))
        min_left = divide(points[:n//2])
        min_right = divide(points[n//2:])

        med_x = (points[n//2].x + points[-n//2-1].x)/2
        min_d = min(min_left, min_right)

    return combine(points, n, min_d, med_x)
```
