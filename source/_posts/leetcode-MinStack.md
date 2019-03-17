---
title: LeetCode_Min Stack
date: 2019-03-17 23:26:38
categories: LeetCode
tags: 
  - easy
  - stack
  - design
---

## [Min Stack](https://leetcode.com/problems/min-stack/)

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.
  - push(x) -- Push element x onto stack.
  - pop() -- Removes the element on top of the stack.
  - top() -- Get the top element.
  - getMin() -- Retrieve the minimum element in the stack.

（设计一个堆栈类，并可以O(1)定位到最小值）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_155.png" width = "500" align=center/>
</div>


### 1. 牺牲空间复杂度来实现时间复杂度
为了能够快速在动态出栈，入栈的过程中得到当前堆栈的最小值，我们需要维护一个与当前栈相同大小的“最小栈”，并在入栈的时候更新一致，具体实现过程如下：

```python
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack = []
        self.min_ele = []

    def push(self, x: int) -> None:
        if not self.stack:   
            self.stack.append(x)
            self.min_ele.append(x)
        else:
            min_ele = min(self.min_ele[-1], x)
            self.stack.append(x)
            self.min_ele.append(min_ele)

    def pop(self) -> None:
        self.stack.pop()
        self.min_ele.pop()

    def top(self) -> int:
        if not self.stack:
            return None
        else:
            return self.stack[-1]

    def getMin(self) -> int:
        if not self.stack:
            return None
        else:
            return self.min_ele[-1]


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```