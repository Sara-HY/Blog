---
title: LeetCode_Sort Colors
date: 2019-02-21 17:42:37
categories: LeetCode
tags: 
  - medium
  - array
  - two pointers
  - sort
---

## [Sort Colors](https://leetcode.com/problems/sort-colors/)

Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue. Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.
(in-place 分组排序)

<!--more-->

**Note:** You are not suppose to use the library's sort function for this problem.

**Follow up:** A rather straight forward solution is a two-pass algorithm using counting sort. First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's. Could you come up with a one-pass algorithm using only constant space?

**Example:**
<div align=center>
	<img src="/images/leetcode_75.png" width = "500" align=center/>
</div>


### 1. 首尾指针

在一开始，两个指针是指向数组的头和尾的，可以看做是排好序的“0”序列的后一个数和“2”序列的前一个数。遍历数组当遇到“0”时，将其和“0”序列后面一个数交换，然后“0”序列的指针向后移。当遇到“2”时，将其和“2”序列前面一个数交换，然后将“2”序列的指针向前移。遇到“1”时，不做处理。这样，当我们遍历到2序列开头时，实际上我们已经排好序了，因为所有“0”都被交换到了前面，所有“2”都被交换到了后面。 (这里需要注意的是当遇到“2”时并交换数值之后，我们还不能确定换来的就是“0”“1”“2”，需要重新检测一次。) 其时间复杂度为O(N)，空间复杂度为O(1)。

```python
class Solution:
    def sortColors(self, nums: 'List[int]') -> 'None':
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        left, right, i = 0, n - 1, 0

        while i <= right:
            if nums[i] == 0:
                nums[i], nums[left] = nums[left], nums[i]
                left += 1
                i += 1 
            elif nums[i] == 2:
                nums[i], nums[right] = nums[right], nums[i]
                right -= 1
            else:
                i += 1
```

### 2. 遍历两次
根据题中的Follow Up, 我们可以在第一次遍历过程中分别记录“0”“1”“2”的个数，在第二次遍历过程中一次替换即可。

