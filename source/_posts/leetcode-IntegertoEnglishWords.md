---
title: leetcode_Integer to English Words
date: 2019-06-30 21:41:50
categories: LeetCode
tags: 
  - hard
  - math
  - string
  - hash table
---

## [Integer to English Words](https://leetcode.com/problems/integer-to-english-words/)

Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than 2^31 - 1.
（读数值）

<!--more-->

**Example:** 

<div align=center>
	<img src="/images/leetcode_273.png" width = "500" align=center/>
</div>

### 1. 哈希表

```python
class Solution:       
    def numberToWords(self, num: int) -> str:
        if num == 0:
            return "Zero"
        
        digits = ["Zero", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"]
        tens = ["Zero", "Ten", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"]
    
        if num >= 1000000000:
            if num % 1000000000:
                return self.numberToWords(num // 1000000000) + " Billion " +  self.numberToWords(num % 1000000000)
            else:
                return self.numberToWords(num // 1000000000) + " Billion"
        elif num >= 1000000:
            if num % 1000000:
                return self.numberToWords(num // 1000000) + " Million " +  self.numberToWords(num % 1000000)
            else:
                return self.numberToWords(num // 1000000) + " Million"
        elif num >= 1000:
            if num % 1000:
                return self.numberToWords(num // 1000) + " Thousand " +  self.numberToWords(num % 1000)
            else:
                return self.numberToWords(num // 1000) + " Thousand" 
        elif num >= 100:
            if num % 100:
                return self.numberToWords(num // 100) + " Hundred " +  self.numberToWords(num % 100)
            else:
                return self.numberToWords(num // 100) + " Hundred"
        elif num >= 20:
            if num % 10:
                return tens[num // 10] + ' ' +self.numberToWords(num % 10)
            else:
                return tens[num // 10]
        elif num >= 1:
            return digits[num]
        else:
            return ''
```


另一种更简洁的方法如下：

```python
num_mapping = {
    1: "One",
    2: "Two",
    3: "Three",
    4: "Four",
    5: "Five",
    6: "Six",
    7: "Seven",
    8: "Eight",
    9: "Nine",
    10: "Ten",
    11: "Eleven",
    12: "Twelve",
    13: "Thirteen",
    14: "Fourteen",
    15: "Fifteen",
    16: "Sixteen",
    17: "Seventeen",
    18: "Eighteen",
    19: "Nineteen"
}

prefixes = [
    (1000000000, "Billion"),
    (1000000, "Million"),
    (1000, "Thousand"),
    (100, "Hundred"),
    (90, "Ninety"),
    (80, "Eighty"),
    (70, "Seventy"),
    (60, "Sixty"),
    (50, "Fifty"),
    (40, "Forty"),
    (30, "Thirty"),
    (20, "Twenty")
]

class Solution:
    def numberToWords(self, num: int) -> str:
        if num in num_mapping:
            return num_mapping[num]
        elif num == 0:
            return "Zero"
        
        words = []
        for size, text in prefixes:
            size_count = num // size
            num = num % size
            if size_count:
                if size >= 100:
                    words.append(self.numberToWords(size_count))
                words.append(text)
                
        if num in num_mapping:
            words.append(num_mapping[num])
        
        return " ".join(words)
```