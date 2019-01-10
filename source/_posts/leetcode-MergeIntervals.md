---
title: LeetCode_Merge Intervals
date: 2019-01-10 21:39:48
categories: LeetCode
tags: 
  - medium
  - array
  - sort
---

## [Merge Intervals](https://leetcode.com/problems/merge-intervals/)

Given a collection of intervals, merge all overlapping intervals.
(合并间隔区间)

<!--more-->

**Example:**
<div align=center>
	<img src="/images/leetcode_56.png" width = "500" align=center/>
</div>


### 1. 贪心算法

类似于教室安排问题，根据每个间隔区间的 start 排序，然后遍历所有的间隔区间：
1. 当前间隔区间的 start 位置大于之前所有合并的区间的 end 时，加入新的间隔区间；
2. 更新合并区间的 end 为之前合并区间的 end 和当前间隔区间 end 的最大值。

```python
class Solution:
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        
        intervals.sort(key=lambda x: x.start)
        
        result = []
        for interval in intervals:
            if not result or result[-1].end < interval.start:
                result.append(interval)
            else:
                result[-1].end = max(result[-1].end, interval.end)
                
        return result
```