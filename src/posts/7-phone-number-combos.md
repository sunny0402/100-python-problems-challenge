---
title: Python Challenge - Letter Combinations of a Phone Number
description: Find all letter combinations given an input number.
date: 2023-03-24
tags:
  - posts
layout: layouts/post.njk
---

Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]

Each digit on the phone maps to several characters.

<br/>

```python
self.map = {'2':['a','b','c'],
        '3':['d','e','f'],
        '4': ['g','h','i'],
        '5': ['j','k','l'],
        '6': ['m','n','o'],
        '7': ['p','q','r','s'],
        '8': ['t','u','v'],
        '9': ['w','x','y','z']}
```

<br/>

LeetCode problem [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/).

We'll use backtracking to generate all possible combinations. For combinations order does not matter, meaning ["a","d"] is the same as ["d","a"], therefore only return one.

Backtracing Template:

```python
if isCombination():
    result.append()
    return

for next_candidate in list_of_candidates:
    append(next_candidate)
    backtrack(next_candidate)
    remove(next_candidate)
```

<br/>

Solution:

```python
class Solution:
    def __init__(self):
        self.result = []
        self.temp = []
        self.map = {'2':['a','b','c'],
               '3':['d','e','f'],
               '4': ['g','h','i'],
               '5': ['j','k','l'],
               '6': ['m','n','o'],
               '7': ['p','q','r','s'],
               '8': ['t','u','v'],
               '9': ['w','x','y','z']}

    def backtrack(self,index,input_nums,length):
        if len(self.temp) == length:
            self.result.append(self.temp[:])
            return

        current_digit = input_nums[index]
        for char in self.map[current_digit]: #Note: 2 : ['d','e','f'|
            self.temp.append(char)
            self.backtrack(index+1,input_nums,length)
            self.temp.pop(-1)

    def letterCombinations(self, digits:str):
        nums = [num for num in digits]
        num_digits = len(nums)
        if num_digits == 0:
            return []
        self.backtrack(0,nums,num_digits)


        return ["".join(combo) for combo in self.result]


answer = Solution().letterCombinations("23")
print(answer)
```

<br/>
