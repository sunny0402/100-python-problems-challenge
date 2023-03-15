---
title: Python Challenge -  Repeated Substring Pattern
description: Can a string be constructed from repeated substrings.
date: 2023-03-14
tags:
  - posts
layout: layouts/post.njk
---

Can a string be constructed from repeated substrings?

This is [LeetCode problem 459](https://leetcode.com/problems/repeated-substring-pattern/description/).

As move down the characters of a string determine whether can repeat those characters to form the string.

Solution:

```python
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:
        length = len(s)
        for idx in range(1,length):
            if idx > length / 2:
                return False
            substring = s[:idx]

            if len(s) % len(substring) == 0: #note: can we repeat substring to make s
                repeat_num = len(s) // len(substring)
                if substring*repeat_num == s:
                        return True
        return False
```
