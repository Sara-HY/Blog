---
title: LeetCode_Valid Number
date: 2019-01-15 14:25:07
categories: LeetCode
tags: 
  - hard
  - math
  - string
---

## [Valid Number](https://leetcode.com/problems/valid-number/)

Validate if a given string can be interpreted as a decimal number.
（字符串是否为有效数字）

<!--more-->

**Note:** It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one. However, here is a list of characters that can be in a valid decimal number:

  - Numbers 0-9
  - Exponent - "e"
  - Positive/negative sign - "+"/"-"
  - Decimal point - "."

Of course, the context of these characters also matters in the input.

**Example:** 

<div align=center>
	<img src="/images/leetcode_65.png" width = "500" align=center/>
</div>

### 1. 有限状态机（Deterministic Finite Automaton, DFA）

所谓“确定有穷状态”，必然需要我们自己动手构造出所有状态来，如下所示：

0 初始无输入或者只有space的状态
1 输入了数字之后的状态
2 前面无数字，只输入了dot的状态
3 输入了+/-状态
4 前面有数字和有dot的状态
5 'e' or 'E'输入后的状态
6 输入e之后输入+/-的状态
7 输入e后输入数字的状态
8 前面有有效数输入之后，输入space的状态

<div align=center>
	<img src="/images/leetcode_65_2.png" width = "500" align=center/>
</div>

```python
class Solution:
    def isNumber(self, s):
        """
        :type s: str
        :rtype: bool
        """
        # 0invalid, 1space, 2sign, 3digit, 4dot, 5exponent, 6num_inputs
        INVALID, SPACE, SIGN, DIGIT, DOT, EXPONENT = 0, 1, 2, 3, 4, 5

        transitionTable=[[-1,  0,  3,  1,  2, -1],    #0 no input or just spaces 
                         [-1,  8, -1,  1,  4,  5],    #1 input is digits 
                         [-1, -1, -1,  4, -1, -1],    #2 no digits in front just Dot 
                         [-1, -1, -1,  1,  2, -1],    #3 sign 
                         [-1,  8, -1,  4, -1,  5],    #4 digits and dot in front 
                         [-1, -1,  6,  7, -1, -1],    #5 input 'e' or 'E' 
                         [-1, -1, -1,  7, -1, -1],    #6 after 'e' input sign 
                         [-1,  8, -1,  7, -1, -1],    #7 after 'e' input digits 
                         [-1,  8, -1, -1, -1, -1]]    #8 after valid input input space
        state = 0
        for c in s:
            inputtype = INVALID
            if c == ' ': 
                inputtype = SPACE
            elif c == '-' or c == '+': 
                inputtype = SIGN
            elif c.isdigit(): 
                inputtype = DIGIT
            elif c == '.': 
                inputtype = DOT
            elif c.lower() == 'e': 
                inputtype = EXPONENT
            state = transitionTable[state][inputtype]
            if state == -1: 
                return False

        return state == 1 or state == 4 or state == 7 or state == 8
```

### 2. 正则表达式
考察正则表达式的书写：
1. 前后的空格 “(\\s\*)”
2. 整个数字的符号 “[+-]?”
3. 纯小数或者带小数 ((\\.[0-9]+)|([0-9]+(\\.[0-9]\*)?))，这部分可以单独出现，也可以是科学计数法的前部分。
4. 科学计数法，(e[+-]?[0-9]+)?
（**\***表示匹配0至多次，**+**表示匹配1至多次，**?**表示匹配0至1次。）

```python
import re 

class Solution:
    def isNumber(self, s):
        """
        :type s: str
        :rtype: bool
        """
        pattern = "(\\s*)[+-]?((\\.[0-9]+)|([0-9]+(\\.[0-9]*)?))(e[+-]?[0-9]+)?(\\s*)"
        
        return bool(re.fullmatch(pattern, s))
```

### 3. 搞笑版
直接调用 python 的类型转换函数`float()`，出现异常则不是有效的数字。

```python
class Solution:
    def isNumber(self, s):
		"""
        :type s: str
        :rtype: bool
        """
        try:
            float(s)
        except:
            return False

        return True
```
