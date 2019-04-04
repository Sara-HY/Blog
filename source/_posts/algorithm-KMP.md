---
title: Algorithm_KMP
date: 2019-04-03 17:14:38
categories: Algorithm
tags: 
  - string
---

## [KMP](https://zh.wikipedia.org/wiki/%E5%85%8B%E5%8A%AA%E6%96%AF-%E8%8E%AB%E9%87%8C%E6%96%AF-%E6%99%AE%E6%8B%89%E7%89%B9%E7%AE%97%E6%B3%95)（Knuth-Morris-Pratt 字符串子串位置）

<!--more-->

在字符串 **S** 内查找子串 **T** 出现的位置，如果我们不考虑使用 KMP 算法，使用简单的轮循，具体实现过程如下：

### 1. 暴力轮循
```python
s = 'bbc abcbab abcdabcdabde'
t = 'abcdabd'

m, n = len(s), len(t)
i, j = 0, 0

while i < m and j < n:
    if s[i] == t[j]:
        i += 1
        j += 1
    else:
        i = i - j + 1
        j = 0

if j == n:
    return i - j
else:
    return -1
```

### 2. KMP 

KMP 算法的主要 trick 就是在于：若当前的 **S** 中的字符串序列与 **T** 不匹配，则它会记录下一个匹配可能从哪里开始（因为我们已经遍历了前面的字符），从而避免重新检查先前匹配的字符。

**Example:** 

如 `S = BBC ABCDAB ABCDABCDABDE` ，`T= ABCDABD`，则在外层循环扫描到 S中的 "A" 时，：

```
'BBC ABCDAB ABCDABCDABDE'
'    ABCDABD'                # 此时不匹配，我们可以直接从下一个 "A" 开始
'BBC ABCDAB ABCDABCDABDE'
'        ABCDABD'            # 此时不匹配，我们可以直接从下一个 "A" 开始
'BBC ABCDAB ABCDABCDABDE'
'           ABCDABD'         # 此时不匹配，我们可以直接从下一个 "A" 开始
'BBC ABCDAB ABCDABCDABDE'
'               ABCDABD'     # 此时不匹配，我们可以直接从下一个 "A" 开始
```

而这个算法的关键就在于我们如何记录不匹配时重新从哪里开始继续扫描，实质上是计算当前匹配了的字符串 **T[:j]**前缀后缀最长公共元素长度，上一个例子第一次中 **T[:j]** 为 'ABCDAB'：
```
'ABCDAB' 的前缀为 [A, AB, ABC, ABCD, ABCDA]
'ABCDAB' 的后缀为 [B, AB, DAB, CDAB, BCDAB]
```
前缀后缀最长公共元素长度为2。我们可以求出 **T** 相应子串的前缀后缀最长公共元素长度为
```
A B C D A B D
0 0 0 0 1 2 0
```
由于是否匹配在于第一个不匹配的元素，于是 Next 数组为
```
 A B C D A B D
-1 0 0 0 0 1 2
```

最终 KMP 具体实现过程如下：

```python
def get_next(t, n):
    Next = [0 for _ in range(n)]
    Next[0] = -1
    j, k = 0, -1
    while j < n - 1:
        if k == -1 or t[j] == t[k]:
            j += 1
            k += 1
            Next[j] = k
        else:
            k = Next[k]
    return Next

s = 'bbc abcbab abcdabcdabde'
t = 'abcdabd'
m, n = len(s), len(t)
i, j = 0, 0

Next = get_next(t, n)

while i < m and j < n:
    if j==-1 or s[i] == t[j]:
        i += 1
        j += 1
    else:
        j = Next[j]

if j == n:
    return i - j
else:
    return -1
```




### 3. KMP 变种 
**问题描述**：给定字符串，不断将首字母移动到末尾并记录所得的字符串，则不同的字符串有多少个。

**解析**：如果字符串中有循环的话，于是问题转化为求字符串中的循环节。假设字符串长度了n，利用 KMP 的 Next 数组求出的循环节长度为 Next[n] (**注意：这里是n**)，那么我们去掉循环部分得到的答案为 answer。

这里还需要注意的是当 n % answer == 0的时候答案是 answer，否则答案是 n 。比如 'abab'答案是2，'aabbaaa' 这个样例答案是7。

具体实现过程如下：

```python
def get_next(t, n):
    Next = [0 for _ in range(n + 1)]
    Next[0] = -1
    j, k = 0, -1
    while j < n:
        if k == -1 or t[j] == t[k]:
            j += 1
            k += 1
            Next[j] = k
        else:
            k = Next[k]
    return Next

t = 'abab'
n = len(t)
Next = get_next(t, n)
answer = n - Next[n]

if n % answer == 0:
    print(answer)
else:
    print(n)
```


