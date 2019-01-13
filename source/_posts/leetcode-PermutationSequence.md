---
title: LeetCode_Permutation Sequence
date: 2019-01-13 15:48:55
categories: LeetCode
tags: 
  - medium
  - math
  - back tracking
---

## [Permutation Sequence](https://leetcode.com/problems/permutation-sequence/)

The set [1,2,3,...,n] contains a total of n! unique permutations. By listing and labeling all of the permutations in order, we get the following sequence for n = 3: "123", "132", "213", "231", "312", "321". Given n and k, return the k_th permutation sequence.
(排列组合结果的第 K 项)

<!--more-->

**Note:**
1. Given n will be between 1 and 9 inclusive.
2. Given k will be between 1 and n! inclusive.


**Example:**
<div align=center>
	<img src="/images/leetcode_60.png" width = "500" align=center/>
</div>


### 1. 找规律

在n=4，k=9时，
1. 最高位可以取{1, 2, 3, 4}，而每个数重复3!=6次。所以第 k=9 个排列的 s[0] 为{1, 2, 3, 4}中的第 9/6+1=2 个数字，即s[0]=2；
2. 同样地，对于以 **2** 开头的6个数字而言，k=9是其中的第 k'=9%(3!)=3 个。而剩下的数字{1, 3, 4}的重复周期为 2!=2次。所以 s[1] 为{1, 3, 4} 中的第k'/(2!)+1=2个，即 s[1]=3；
3. 以此类推，对于以 **23** 开头的2个数字而言，k=9是其中的第k''=k'%(2!)=1 个。剩下的数字{1, 4}的重复周期为 1!=1次。所以 s[2]=1；
4. 对于以 **231** 开头的一个数字而言，k=9是其中的第k'''=k''/(1!)+1=1 个。所以s[3]=4。

综上所述，按照顺序寻找 n 的全排列中的第 k 个，也是就是不断地对 (n-1)! 取商和余数的过程。这里使用 k-1 来判断是为了方便处理边界条件。具体实现方法如下：

```python
class Solution:
    def getPermutation(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: str
        """
        nums = [str(i) for i in range(1, n+1)]
        result = ''

        k -= 1
        for i in range(n):
            rank, k = divmod(k, math.factorial(n-i-1))
            result += nums[rank]
            # nums.remove(nums[rank])
            nums.pop(rank)

        return result
```








