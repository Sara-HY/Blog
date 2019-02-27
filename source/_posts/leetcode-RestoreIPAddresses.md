---
title: LeetCode_Restore IP Addresses
date: 2019-02-27 01:10:07
categories: LeetCode
tags: 
  - medium
  - string
  - back tracking
---

## [Restore IP Addresses](https://leetcode.com/problems/restore-ip-addresses/)

Given a string containing only digits, restore it by returning all possible valid IP address combinations.
（IP地址规则化）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_93.png" width = "500" align=center/>
</div>

### 1. 回溯法 / DFS
很自然的使用回溯法来解决这个问题。其中，需要考虑到的问题是：
1. ip地址为4段，每段在[0,255]区间内；
2. 每段可以是0，但是其长度大于1时，不能以0开头。
具体实现过程如下：

```python
class Solution:
    def dfs(self, string, part, count):
        re = ".".join(part)
        if count == 4 and not string and re not in self.results:
            self.results.append(re)
        
        for j in range(len(string)):
            # count = 4 才满足ip的4段地址，新划分的string[:j+1]不为空，且在0-255之间
            if count <= 3 and string[:j+1] and int(string[:j+1]) <= 255 \
            # string[:j+1]长度为1 或 string[:j+1]长度大于1但不能以0开头
            and (j+1 < 2 or (j+1 >= 2 and string[0] != '0')):
                    self.dfs(string[j+1:], part + [string[:j+1]], count + 1)

        # for i in range(1, 4):
        #     if i <= len(string):
        #         if i == 1:
        #             self.dfs(string[i:], part + [string[:i]], count + 1)
        #         if i==2 and string[0] != '0':
        #             self.dfs(string[i:], part + [string[:i]], count + 1)
        #         if i==3 and string[0] != '0' and int(string[:3]) <= 255 :
        #             self.dfs(string[i:], part + [string[:i]], count + 1)
    
    def restoreIpAddresses(self, s: str) -> List[str]:
        if not s or len(s) > 12:
            return []
        self.results = []
        self.dfs(s, [], 0)
        
        return self.results
```