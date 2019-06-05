---
title: LeetCode_Kth Largest Element in an Array
date: 2019-06-05 12:42:11
categories: LeetCode
tags: 
  - medium
  - divide and conquer
  - heap
---

## [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.
(数组定位第k大的元素)

<!--more-->

**Note:**
You may assume k is always valid, 1 ≤ k ≤ array's length.


**Example:**
<div align=center>
	<img src="/images/leetcode_45.png" width = "500" align=center/>
</div>


### 1. 堆

```python
import heapq

class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        heapq.heapify(nums)
        nlarge = heapq.nlargest(k, nums)
        return nlarge[-1]
```