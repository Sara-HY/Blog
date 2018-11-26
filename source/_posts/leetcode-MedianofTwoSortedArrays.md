---
title: LeetCode_Median of Two Sorted Arrays
date: 2018-11-23 18:30:10
categories: LeetCode
tags: 
  - array
  - binary search
  - divide and conquer
---

## [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

There are two sorted arrays nums1 and nums2 of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be **O(log (m+n))**. You may assume nums1 and nums2 cannot be both empty.
（两个有序数组的中位数）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_4.png" width = "500" align=center/>
</div>

### 1. 分治法_1
我们可以将中位数简单的理解成将数组分成两个部分，一部分中的数值总是大于另一部分。因此，我们可以看做是找\\((m+n)\\)个数中的第\\((m+n)/2\\)数值的大小（需要单独考虑\\((m+n)\\)的奇偶性）。其时间复杂度为 \\(O(log(m+n))\\)。具体实现过程如下：
```
class Solution:
    def findKth(self, nums1, nums2, k):
        if not nums1:
            return nums2[k]
        if not nums2:
            return nums1[k]
        
        len1 = len(nums1)
        len2 = len(nums2)
        
        i, j = len1 // 2, len2 // 2
        
        if i + j < k:
            if nums1[i] > nums2[j]:
                return self.findKth(nums1, nums2[j+1:], k-j-1)
            else:
                return self.findKth(nums1[i+1: ], nums2, k-i-1)
        else:
            if nums1[i] > nums2[j]:
                return self.findKth(nums1[:i], nums2, k)
            else:
                return self.findKth(nums1, nums2[:j], k)
                
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        length = len(nums1) + len(nums2)
        
        if length % 2:
            return self.findKth(nums1, nums2, length//2)
        else:
            return (self.findKth(nums1, nums2, length//2) + self.findKth(nums1, nums2, length//2-1))/2
```

### 2. 分治法_2
与上面的思路相同，但是不同的是找第 \\(k\\) 个值时，并不是直接将两个数组混合一起找第 \\(k\\) 个，而是以比较短的数组 A 为基准，找到符合条件的 \\(i\\)，使得 \\(A[i]\\) 和 \\(B[k-i]\\) 刚好满足其中一个是第\\(k\\)个数。其时间复杂度为 \\(O(log(min(m, n)))\\)。具体实现过程如下：
```
def findKth(self, nums1, nums2, k):
        len1 = len(nums1)
        len2 = len(nums2)
        
        if len1 > len2:
            len1, len2, nums1, nums2 = len2, len1, nums2, nums1
        if not nums1:
            return nums2[k]
        if k == len1 + len2 - 1:
            return max(nums1[-1], nums2[-1])
        
        i = len1 // 2
        j = k - i
        
        if nums1[i] > nums2[j]:
            # Assume it is O(1) to get A[:i] and B[j:]. In python, it's not but in cpp it is.
            return self.findKth(nums1[:i], nums2[j:], i)
        else:
            return self.findKth(nums1[i:], nums2[:j], j)
```




















