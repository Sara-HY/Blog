---
title: LeetCode_Validate Stack Sequences
date: 2019-08-20 15:02:29
categories: LeetCode
tags: 
  - medium
  - stack
---

## [Validate Stack Sequences](https://leetcode.com/problems/validate-stack-sequences/)

Given two sequences **pushed** and **popped** with distinct values, return true if and only if this could have been the result of a sequence of push and pop operations on an initially empty stack.
（判断有效的栈压入、压出序列）

**Note:**
1. 0 <= pushed.length == popped.length <= 1000
2. 0 <= pushed[i], popped[i] < 1000
3. pushed is a permutation of popped.
4. pushed and popped have distinct values.

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_946.png" width = "500" align=center/>
</div>


### 1. 模拟栈
构建一个新的栈来模拟栈压入、压出的过程，直到最后栈为空时表示是有效的序列。时间复杂度为O(n)，空间复杂度为O(n)。具体实现过程如下：

```python
class Solution:
    def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
        temp_stack = []
        while pushed:
            top = pushed.pop(0)
            temp_stack.append(top)
            while temp_stack and popped and popped[0] == temp_stack[-1]:
                popped.pop(0)
                temp_stack.pop()
        return not temp_stack
```