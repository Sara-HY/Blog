---
title: LeetCode_Merge Sorted Array
date: 2019-02-25 21:51:03
categories: LeetCode
tags: 
  - easy
  - array
  - two pointers
---

## [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.
(合并有序数组)

<!--more-->

**Note:**
1. The number of elements initialized in nums1 and nums2 are m and n respectively.
2. You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.

**Example:**

<div align=center>
	<img src="/images/leetcode_88.png" width = "500" align=center/>
</div>

### 1. 反向插入
由于最终的数组的长度是已知的，我们可以直接从最后一个位置向前遍历，寻找最大值。具体实现过程如下：

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        index = m + n - 1
        while index >= 0:
            if m > 0 and n > 0:
                if nums1[m-1] > nums2[n-1]:
                    nums1[index] = nums1[m-1]
                    m -= 1
                else:
                    nums1[index] = nums2[n-1]
                    n -= 1
                index -= 1
            elif n > 0:
                nums1[: index+1] = nums2[: index+1]
                break
            else:
                break
```