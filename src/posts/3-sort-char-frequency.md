---
title: Python Challenge - Sort Characters By Frequency
description: Sort a string based on character frequency.
date: 2023-03-18
tags:
  - posts
layout: layouts/post.njk
---

This is LeetCode problem [451. Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/description/)

The output string should order the characters by their frequency, most frequent first.

Input: s = "tree"
Output: "eert"

Input: s = "cccaaa"
Output: "aaaccc"

Input: s = "Aabb"
Output: "bbAa"

Strings are immutable so growing a string by concatenating characters takes O(n^2).

Read about it [here](https://stackoverflow.com/questions/37133547/time-complexity-of-string-concatenation-in-python)

But basically we want to avoid something like:

```python

word = ""
for i in range(m):
    word = char_value + word
return word
```

<br/>

And as [described here](https://stackoverflow.com/questions/34008010/is-the-time-complexity-of-iterative-string-append-actually-on2-or-on) use an array to work with characters of the string.

<br/>

```python
output = []
    # ... loop thing
    output.append('%20')
    # ...
    output.append(char)
# ...
return ''.join(output)
```

<br/>

Note that the join takes O(n) but is outside the loop.

<br/>

```python
class Solution:
    def frequencySort(self, s: str) -> str:
        #Note: create frequency dictionary
        frequency = {}
        for char in s:
            if char in frequency:
                frequency[char] = frequency[char] + 1
            else:
                frequency[char] = 1
        #Note: Each element in grouped duplicated based on frequency
        grouped = []
        for key in frequency.keys():
            grouped.append( key*frequency[key] )
        #Note: Sort by group length, descending
        def sortFunction(e):
            return len(e)
        grouped.sort(key=sortFunction,reverse=True)
        return "".join(grouped)
```

<br/>

Running the function should produce the following ouput:

<br/>

```python
s1 = "tree"
answer = Solution().frequencySort(s1)
print(answer) #eetr

s2 = "cccaaa"
answer = Solution().frequencySort(s2)
print(answer) #cccaaa

s3 = "Aabb"
answer = Solution().frequencySort(s3)
print(answer) #bbAa
```

<br/>
