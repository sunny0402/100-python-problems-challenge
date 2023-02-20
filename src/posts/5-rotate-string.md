---
title: Python Challenge - Rotate String
description: Can two strings be made equal after rotation.
date: 2023-03-19
tags:
  - posts
layout: layouts/post.njk
---

LeetCode problem [796. Rotate String](https://leetcode.com/problems/rotate-string/description/).

Input: s = "abcde", goal = "cdeab"
Output: true

Input: s = "abcde", goal = "abced"
Output: false

So can we shift the characters in s to make goal?

We shift by moving the leftmost character to the end.

<br/>

```python
class Solution:
    def rotateString(self, s: str, goal: str) -> bool:
        if (len(s)!= len(goal)):
            return False
        if (s == goal):
            return True

        length = len(s)
        # Note: range(length -1 ) as above check if s == goal
        for idx in range(length - 1 ):
            temp = s[1+idx:] + s[:idx+1]
            if(temp == goal):
                return True

answer = Solution().rotateString("abcde","cdeab")
print(answer) # True
```

<br/>
<br/>
