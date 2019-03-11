---
title: LeetCode_Pascal's Triangle
date: 2019-03-11 10:32:00
categories: LeetCode
tags: 
  - easy
  - array
---

## [Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/)

Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.
(杨辉三角)

<!--more-->


**Example:**

<div align=center>
	<img src="/images/leetcode_118.png" width = "500" align=center/>
</div>

### 1. 逐层生成
根据杨辉三角的规律，组成生成杨辉三角，具体实现过程如下：

```python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        if numRows == 0:
            return []
        
        results = []
        for i in range(numRows):
            if i == 0:
                results.append([1])
            else:
                list = [1]
                for j in range(i-1):
                    list.append(results[i-1][j] + results[i-1][j+1])
                list.append(1)
                results.append(list)
            
        return results
```