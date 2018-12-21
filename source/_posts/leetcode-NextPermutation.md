---
title: LeetCode_Next Permutation
date: 2018-12-21 10:13:55
categories: LeetCode
tags: 
  - medium
  - array
---

## [Next Permutation](https://leetcode.com/problems/next-permutation/)

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers. If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order). The replacement must be in-place and use only constant extra memory.
（从小到大全排列的下一个）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_31.png" width = "500" align=center/>
</div>

### 1. 后向遍历
整体的思路就是从后向前遍历：
1. 当遇到第一个数值大于其前面的数值，记录下这个数值，如 [1, 3, 5, 4, 2], 则此时的 i 为2。
2. 将数组中从i到最后的部分倒序，即变为 [1, 3, 2, 4, 5]。
3. 再次遍历从i到最后的部分，找到第一个大于 nums[i-1]（此处为3） 的值并交换即可，即为 [1, 4, 2, 3, 5]。

```python
class Solution:
    def nextPermutation(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        
        n = len(nums)
        if n == 0:
            return
        for i in range(n-1, -1, -1):
            if i == 0:
                nums.reverse()
                return 
            if nums[i] > nums[i-1]:
                break
        
        j, k = i, n-1
        while j < k:
            nums[j], nums[k] = nums[k], nums[j]
            j += 1
            k -= 1
      
        for j in range(i, n):
            if nums[j] > nums[i-1]:
                nums[i-1], nums[j] = nums[j], nums[i-1]
                break
            
        return
```


## 2. 后向遍历
另一种思路与上述一致，只是交换步骤2和步骤3的顺序。即先找到位置i，并同时找到后续数组中最小的值j，交换值后再倒序。