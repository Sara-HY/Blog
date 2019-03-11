---
title: LeetCode_Pascal's Triangle II
date: 2019-03-11 11:03:46
categories: LeetCode
tags: 
  - easy
  - array
---

## [Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii/)

Given a non-negative index k where k ≤ 33, return the k_th index row of the Pascal's triangle. Note that the row index starts from 0.
(第k行杨辉三角)

<!--more-->


**Example:**

<div align=center>
	<img src="/images/leetcode_119.png" width = "500" align=center/>
</div>

### 1. 逐层生成
维护两个数组 result 和 result_before 表示当前层和前一层的结果，空间复杂度为 O(k). 具体实现过程如下：

```python
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        if rowIndex == 0:
            return [1]
        if rowIndex == 1:
            return [1, 1]
        
        result = [1, 1]
        for i in range(1, rowIndex):
            result_before = result
            result = [1, 1]
            for j in range(1, i+1):
                result.insert(j, result_before[j] + result_before[j-1])
            
        return result
```


### 2. 直接生成
根据杨辉三角的生成过程来维护一个数组，空间复杂度为 O(k). 具体实现过程如下：

```python
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        result = [1 for i in range(rowIndex + 1)]
        
        for i in range(2, rowIndex + 1):
            aux = result[0]
            for j in range(1, i):
                result[j], aux = result[j]+aux, result[j]
        
        return result
```


