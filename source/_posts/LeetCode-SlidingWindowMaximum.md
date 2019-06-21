---
title: LeetCode_Sliding Window Maximum
date: 2019-06-21 15:36:09
categories: LeetCode
tags: 
  - hard
  - heap
  - sliding window
---

## [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.
（寻找大小为 k 的滑动窗口中的最大值）

<!--more-->

**Example:** 
<div align=center>
    <img src="/images/leetcode_239.png" width = "500" align=center/>
</div>

### 1.常规思路
遍历数组，每次计算最大值，时间复杂度为O(N\*K), 实际操作中会 TLE.


### 2. 最大堆

堆分为最小堆和最大堆，是一种完全二叉树的结构，最小（大）堆的每个节点均不大（小）于为其孩子节点的值。

```python
import heapq

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        if not nums:
            return []

        heap, results = [], []
        for i, n in enumerate(nums):
            while heap and heap[0][1] + k <= i:
                heapq.heappop(heap)
            # 默认为最小堆，并根据push的第一个值排序，因此push (-n, i)
            heapq.heappush(heap, (-n, i))
            if i >= k-1:
                results.append(-heap[0][0])
        
        return results
```

### 3. 双端队列
双端队列类似于一个list，但是可以对两段都进行加入或删除操作。

使用双端队列，队列元素降序排序，队首元素为所求最大值。滑动窗口右移，每次窗口右移的时候需要判断当前的最大值是否在有效范围，若不在，则需要将其从队列中删除。若出现的元素比队尾（最小元素）大，此时移除比起小的数。时间复杂度为 O(n)，空间复杂度为 O(k)，具体实现过程如下：

```python
from collections import deque
    
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        if not nums:
            return []

        q = deque()
        results = []

        for i in range(len(nums)):
            while q and q[0] + k <= i:
                q.popleft()
            while q and nums[i] >= nums[q[-1]]:
                q.pop()
            q.append(i)
            if i >= k-1:
                results.append(nums[q[0]])           
        
        return results
```

**应用**：构造哈夫曼树，任务调度算法

