---
title: LeetCode_Minimum Window Substring
date: 2019-02-22 18:31:19
categories: LeetCode
tags: 
  - hard
  - hash table
  - two pointers
  - string
---

## [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).
（包含字符串的最小窗口）

<!--more-->

**Note:** 
1. If there is no such window in S that covers all characters in T, return the empty string "".
2. If there is such window, you are guaranteed that there will always be only one unique minimum window in S.

**Example:** 

<div align=center>
	<img src="/images/leetcode_76.png" width = "500" align=center/>
</div>

### 1. 哈希表 & 双指针

很直观，这题需要用到 HashMap 来存储目标字符串。用 left，right 两个指针指向 S，在遍历 S 的过程中，right 不断地右移来找到复合要求的字符串，也就是 required_char == 0 的时候，考虑向右移动 left，直到发现了当前的 S[left: right+1] 不符合要求的时候，重新向右移动 right。具体实现过程如下：

```python
import collections

class Solution:
    def minWindow(self, s: 'str', t: 'str') -> 'str':
        if not s or not t:
            return ""

        t_dict = collections.Counter(t)
        required_char = len(t_dict)

        len_s = len(s)
        re_len, re = len_s + 1, ""
        left, right = 0, 0

        while right < len_s:
            if s[right] not in t_dict:
                right += 1
                continue
            t_dict[s[right]] -= 1
            if t_dict[s[right]] == 0:
                required_char -= 1

            while required_char == 0:
                if right - left + 1 < re_len:
                    re = s[left: right + 1]
                    re_len = right - left + 1 

                if s[left] not in t_dict:
                    left += 1
                    continue
                
                t_dict[s[left]] += 1
                if t_dict[s[left]] == 1:
                    required_char += 1
                left += 1

            right += 1

        if re_len == len_s + 1:
            return ""
        return re
```