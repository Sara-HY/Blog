---
title: LeetCode_Insert Interval
date: 2019-01-12 14:05:50
categories: LeetCode
tags: 
  - hard
  - array
  - sort
---

## [Insert Interval](https://leetcode.com/problems/insert-interval/)

Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary). You may assume that the intervals were initially sorted according to their start times.
（插入间隔区间）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_57.png" width = "500" align=center/>
</div>

### 1. 遍历间隔区间
直接遍历间隔区间数组，并在遇到交叉的情况下时不断更新新插入的间隔区间的起止位置。具体实现过程如下：

```python
# Definition for an interval.
# class Interval:
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution:
    def insert(self, intervals, newInterval):
        """
        :type intervals: List[Interval]
        :type newInterval: Interval
        :rtype: List[Interval]
        """
        
        if len(intervals) == 0:
            return [newInterval]
        
        result = []
        
        insert_new = False
        for interval in intervals:
            if interval.end < newInterval.start:
                result.append(interval)
            elif interval.start > newInterval.end:
                if not insert_new:
                    result.append(newInterval)
                    insert_new = True
                result.append(interval)
            else:
                 newInterval = Interval(min(interval.start, newInterval.start), max(interval.end, newInterval.end))
        
        if not insert_new:
            result.append(newInterval)
        
        return result
```

### 2. 合并间隔区间
借用前一道题目的方法，把待插入的间隔区间和数组合并，然后合并交叉的区间。具体实现方法如下：

```python
# Definition for an interval.
# class Interval:
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution:
    def insert(self, intervals, newInterval):
        """
        :type intervals: List[Interval]
        :type newInterval: Interval
        :rtype: List[Interval]
        """
        
        if len(intervals) == 0:
            return [newInterval]
        
        intervals.append(newInterval)
        intervals.sort(key = lambda x: x.start)
        
        result = []
        for interval in intervals:
            if not result or interval.start > result[-1].end:
                result.append(interval)
            else:
                result[-1].start = min(result[-1].start, interval.start)
                result[-1].end = max(result[-1].end, interval.end)
                
        return result 
```

