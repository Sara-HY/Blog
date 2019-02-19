---
title: LeetCode_Text Justification
date: 2019-02-19 14:46:55
categories: LeetCode
tags: 
  - hard
  - string
---

## [Text Justification](https://leetcode.com/problems/text-justification/)

（文本左右对齐）

<!--more-->

**Note:**
1. A word is defined as a character sequence consisting of non-space characters only.
2. Each word's length is guaranteed to be greater than 0 and not exceed maxWidth.
3. The input array words contains at least one word.

**Example:**

<div align=center>
	<img src="/images/leetcode_68.png" width = "500" align=center/>
</div>


### 字符串遍历
具体考虑分析需要分为以下几步：
1. 计算每行最多显示单词的数量，记录起始单词位置（结束指针单词不包含在内），这里要注意，单词与单词之间的都要求有空格，所以除了开始的单词，每个单词的长度还要加1 
2. 计算显示每句话需要的空格的数量 
3. 计算每句话中单词之间需要均匀填充的空格数量。这里要注意最后一行不需要进行均匀填充，不能均匀填充的空格数量要记录下来，优先分给左边的单词间空格 
4. 按照之前计算好的空格数量将单词连接成语句。 
5. 要考虑到最后一句是在最右端填充所有的空格

```python
class Solution(object):
    def fullJustify(self, words, maxWidth):
        """
        :type words: List[str]
        :type maxWidth: int
        :rtype: List[str]
        """
        ans = []
        i = 0
        while i < len(words):
            size = 0
            begin = i

            # 确定每行的单词数
            while i < len(words):
                newsize = len(words[i]) if size == 0 else size + len(words[i]) + 1
                if newsize <= maxWidth: 
                    size = newsize
                    i += 1
                else:
                    break

            # 计算需要的剩余的空格数
            spaceCount = maxWidth - size

            # 计算每个单词需要的分配的单词数
            if i - 1 - begin > 0 and i < len(words):
            	# 不是最后一行
                everyCount = spaceCount // (i - 1 - begin)
                spaceCount %= (i - 1 - begin)
            else:
            	# 最后一行
                everyCount = 0

            # 根据空格数重新构建输出
            j = begin
            s = ''
            while j < i:
                if j > begin:
                    s += ' ' * (everyCount + 1)
                    # 无法均匀分配的空格优先分配给左边
                    if spaceCount > 0 and i < len(words):
                        s += ' '
                        spaceCount -= 1
                s += words[j]
                j += 1
            s += ' ' * spaceCount
            
            ans.append(s)
        return ans
```