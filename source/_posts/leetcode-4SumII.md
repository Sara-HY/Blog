---
title: LeetCode_4SumII
date: 2018-12-06 12:12:13
categories: LeetCode
tags: 
  - medium
  - binary search
  - hash table
---

## [4SumII](https://leetcode.com/problems/4sum-ii/)

Given four lists A, B, C, D of integer values, compute how many tuples (i, j, k, l) there are such that A[i] + B[j] + C[k] + D[l] is zero.
To make problem a bit easier, all A, B, C, D have same length of N where 0 ≤ N ≤ 500. All integers are in the range of -2^28 to 2^28 - 1 and the result is guaranteed to be at most 2^31 - 1.
（寻找4个数组中四个数的和为0的组合个数）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_454.png" width = "500" align=center/>
</div>

### 1. 两次双重循环
将其转换为两次双重循环的问题，第一次查找数组 A 和数组 B 中两个数的和保存在 Dict。第二次查找数组 C 和数组 D 中两个数的和的相反数书否在 Dict中。其时间复杂度为 \\(O(n^2)\\)。
```python
class Solution:
    def fourSumCount(self, A, B, C, D):
        """
        :type A: List[int]
        :type B: List[int]
        :type C: List[int]
        :type D: List[int]
        :rtype: int
        """
        n = len(A)
        
        dict = {}
        for i in range(n):
            for j in range(n):
                sum =  A[i] + B[j]
                if sum not in dict:
                    dict[sum] = 1
                else:
                    dict[sum] += 1
        
        result = 0
        for i in range(n):
            for j in range(n):
                sum = C[i] + D[j]
                if -sum in dict:
                    result += dict[-sum]
                
        return result 
```

### 1. 两次双重循环2
将上述过程中的解法中的通过 index索引改为 python中的 **`in`** 遍历。
```python
class Solution:
    def fourSumCount(self, A, B, C, D):
        """
        :type A: List[int]
        :type B: List[int]
        :type C: List[int]
        :type D: List[int]
        :rtype: int
        """

        dict = {}
        for a in A:
            for b in B:
                if a + b not in dict:
                    dict[a + b] = 1
                else:
                    dict[a + b] += 1
        
        result = 0
        for c in C:
            for d in D:
                if -c-d in dict:
                    result += dict[-c-d]
                
        return result
```
