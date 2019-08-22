---
title: LeetCode_Meeting Rooms II
date: 2019-08-22 22:00:45
categories: LeetCode
tags: 
  - hard
  - sort
---

## [Meeting Rooms II]()

给定一系列的会议时间间隔intervals，包括起始和结束时间[[s1,e1],[s2,e2],...]，找到所需的最小的会议室数量。
（区间重叠最多部分）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_253.png" width = "500" align=center/>
</div>

### 1. 排序

首先对所有区间进行标记，区分起始点和终止点，然后对所有时间节点进行排序（若时间相同保证结束点在开始点前面），再依次遍历每个点，遇到起始点+1，遇到终止点-1，并更新记录最大值。具体实现过程如下：

```python
def minMeetingRooms(intervals):
    if intervals is None or len(intervals) == 0:
        return 0

    time_points = []
    for inter in intervals:
        time_points.append((inter[0], True))
        time_points.append((inter[1], False))
    # 先按x[0]升序，x[0]想等时按照x[1]升序，其中end=False=0， start=True=1
    time_points.sort(key=lambda x: (x[0], x[1]))
   
    count, max_count = 0, 0
    for time_point in time_points:
        if time_point[1]:
            count += 1
        else:
            count -= 1
        max_count = max(max_count, count)
   
    return max_count
```


### 2.求区间
维护两个数组分别保存开始时间和结束时间并排序；然后再遍历开始时间数组，这时不断地更新当前的区间的起止时间；在遇到开始时间大于结束时间时，更新新的结束时间。具体实现过程入下：


```python
# [[10, 14], [12, 16], [12, 18]]   --->  (3, [12, 14])
# [[3, 5], [4, 10], [5, 7], [10, 14], [12, 16], [12, 18]]  --->  (3, [12, 14])

def minMeetingRooms(intervals):
    if intervals is None or len(intervals) == 0:
        return 0

    start_points, end_points = [], []
    for inter in intervals:
        start_points.append(inter[0])
        end_points.append(inter[1])

    start_points.sort()
    end_points.sort()

    count, endpos, result = 0, 0, [-1, -1]
    for i in range(len(intervals)):
        if start_points[i] < end_points[endpos]:
            count += 1
            result[0] = start_points[i]
            result[1] = end_points[endpos]
        else:
            endpos+= 1
   
    return count, result

```