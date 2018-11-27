---
title: LeetCode_Add Two Numbers
date: 2018-11-23 11:59:43
categories: LeetCode
tags: 
  - medium
  - linked list
  - math
---

## [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list. You may assume the two numbers do not contain any leading zero, except the number 0 itself.
（字符串/链表数值加法）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_2.png" width = "500" align=center/>
</div>

这道题是一个很典型的字符串 String 变数字 Number 例子，不过这里使用了**链表**的概念来表示组成数值的每个数字。

### 1. 转换为数值计算

很直观的，我们可以将每一个链表转化为一个真实的数值，计算两者的和之后再将其转换为链表。其时间复杂度为 \\(O(m + n)\\)。

```python
class Solution:
    def list2num(self, l):
        result = 0
        j = 0
        while l != None:
            num =  10 ** j * l.val
            result += num
            l = l.next
            j += 1 
        return result
    
    def num2list(self, num):
        if num == 0:
            return ListNode(0)
        l = ListNode(0)
        p = l
        while num != 0:
            a = num % 10
            num = num // 10
            new_l = ListNode(a)
            p.next = new_l
            p = p.next 
        return l.next
        
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        left = self.list2num(l1)
        right = self.list2num(l2)
        return self.num2list(left + right)
```

### 2. 加法器

我们可以将其看做一个加法器的过程，链表的从头到尾也就是加法器的从个位到最高位的过程，其中需要考虑到每一步加法计算的**进位**。其时间复杂度为 \\(O(max(m + n))\\)。

```python
class Solution:    
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
       
        l = None
        l3 = None
        a = 0
        
        while l1 or l2 or a:
            if l1:
                a += l1.val
                l1 = l1.next
            if l2:
                a +=l2.val
                l2 = l2.next
            if l3:
                l3.next = ListNode(a % 10)
                l3 = l3.next
            else:
                l3 = ListNode(a % 10)
                l = l3
            
            a = a // 10
        
        return l
```

**注**：“/”“//”在python中的作用不同。“/”表示浮点数除法，结果为浮点数；“//”结果为整除向下取整。