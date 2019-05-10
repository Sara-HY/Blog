---
title: Bash Script
date: 2019-05-10 21:47:22
categories: Note
tags:
  - bash
---

Linux 终端指令总结。

<!-- more --> 

### 1. 词频统计

**Example:** 

<div align=center>
	<img src="/images/leetcode_192.png" width = "500" align=center/>
</div>

* tr : -s，连续的字符（空格）缩减为1个；字符替换（空格 -> 换行）。
* uniq -c: 计算相同的行的数目
* sort -r: 降序排序
* awk: 从标准输入中选择字段输出


```bash
cat words.txt | tr -s ' ' '\n' | sort | uniq -c | sort -r | awk '{print $2, $1}'
```


### 2. 输出第 N 行

**Example:** 

<div align=center>
	<img src="/images/leetcode_192.png" width = "500" align=center/>
</div>

* sed : -n，只打印匹配的行


```bash
sed -n 10p file.txt
```




