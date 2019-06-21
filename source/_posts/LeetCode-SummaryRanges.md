---
title: LeetCode_Summary Ranges
date: 2019-06-21 14:22:04
categories: LeetCode
tags: 
  - medium
  - array
---

## [Summary Ranges](https://leetcode.com/problems/summary-ranges/)

Given a sorted integer array without duplicates, return the summary of its ranges.
（将数组中连续的范围合并）

<!--more-->

**Example:** 
<div align=center>
	<img src="/images/leetcode_228.png" width = "500" align=center/>
</div>

### 1. 设置标志位 left

具体实现过程如下：

```python
class Solution:
    def summaryRanges(self, nums: List[int]) -> List[str]:
        n = len(nums)
        if not n:
            return []
        
        results = []
        left = -1
        for i in range(n-1):
            if nums[i] == nums[i+1] - 1:
                if left == -1:
                    left = i
            else:
                if left == -1:
                    results.append(str(nums[i]))
                else:
                    results.append("%s->%s"%(str(nums[left]), str(nums[i])))
                    left = -1
        if left == -1:
            results.append(str(nums[n-1]))
        else:
            results.append("%s->%s"%(str(nums[left]), str(nums[n-1])))
                    
        return results
```

### 2. 直接统计range
在遍历数组的过程中不断地更新统计中range的右界，具体实现过程如下：

```python
def summaryRanges(self, nums):
    ranges = []
    for n in nums:
        if not ranges or n > ranges[-1][-1] + 1:
            ranges += [],
        ranges[-1][1:] = n,
    return ['->'.join(map(str, r)) for r in ranges]
```