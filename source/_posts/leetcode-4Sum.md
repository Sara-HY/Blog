---
title: LeetCode_4Sum
date: 2018-12-04 18:56:06
categories: LeetCode
tags: 
  - medium
  - array
  - hash table
  - two pointers
---

## [4Sum](hhttps://leetcode.com/problems/4sum/)

Given an array nums of n integers and an integer target, are there elements a, b, c, and d in nums such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.
（寻找数组中四个数的和为target的一个组合）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_18.png" width = "500" align=center/>
</div>

### 1. 四个指针
可以将这个题理解为与之前的 3Sum 类似，但是这里要有三重循环，其时间复杂度为 \\(O(n^3)\\)。
```python
class Solution:
    def fourSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        
        result = []
        n = len(nums)
        if n < 4:
            return result
        
        nums.sort()
        for i in range(n):
            for j in range(i-2):
                k = j + 1
                l = i - 1
                while k < l:
                    sum = nums[i] + nums[k] + nums[l] + nums[j]
                    if sum == target:
                        if [nums[j], nums[k], nums[l], nums[i]] not in result:
                            result.append([nums[j], nums[k], nums[l], nums[i]])
                        k+=1
                        l-=1
                    elif sum > target:
                        l-=1
                    else:
                        k+=1
        
        return result
```

### 2. 两次 2Sum + Dict
换一种思路，以空间换时间。我们可以将其转换为两次 2Sum 的过程。第一次 2Sum 遍历数组中所有的两个数的和，并将索引在 dict 中保存。第二次 2Sum 来判断数组中的和与 Dict 是否满足要求 Target。其时间复杂度为 \\(O(n^2)\\)。 
```python
class Solution:
    def fourSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        
        result = []
        n = len(nums)
        if n < 4:
            return result
        
        nums.sort()   
     
        dict = {}
        for i in range(n):
            for j in range(i):
                sum = nums[i] + nums[j]
                if sum not in dict:
                    dict[sum] = [[j, i]]
                else:
                    dict[sum].append([j, i])
        
        for i in range(n):
            for j in range(i):
                sum = target - nums[i] - nums[j]
                if sum in dict:
                    for list in dict[sum]:
                        if list[0] > i and [nums[j],nums[i], nums[list[0]], nums[list[1]]] not in result:
                            result.append([nums[j],nums[i],nums[list[0]],nums[list[1]]])

        return result
```

### 3. 递归 N-sum
这个是在提交之后看到的别人的解法，将 N-sum 的问题递归的向下传递为 N-1, N-2 等等的问题，最终归结为 2Sum 的问题。 

```python
class Solution:
    def fourSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        def findNsum(l, r, target, N, result, results):
            if r-l+1<N or N<2 or nums[l]*N > target or nums[r]*N < target:
                return
            if N == 2:
                while l < r:
                    sum = nums[l] + nums[r]
                    if sum == target:
                        results.append(result + [nums[l], nums[r]])
                        l += 1
                        while l < r and nums[l] == nums[l-1]:
                            l+=1
                    elif sum < target:
                        l += 1
                    else:
                        r -= 1
            else:
                for i in range(l, r+1):
                    if i == l or (i > l and nums[i-1] != nums[i]):
                        findNsum(i+1, r, target-nums[i], N-1, result+[nums[i]], results)
            
        nums.sort()
        results = []
        findNsum(0, len(nums)-1, target, 4, [], results)
        
        return results 
```























