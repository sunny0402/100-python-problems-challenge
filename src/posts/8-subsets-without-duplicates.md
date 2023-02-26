---
title: Python Challenge - Subsets without duplicates
description: Given an integer array with duplicates, find all unqiue subsets.
date: 2023-03-24
tags:
  - posts
layout: layouts/post.njk
---

This builds on a previous [subsets problem](https://100-python-problems-challenge.netlify.app/posts/6-subsets/).

Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]

Only difference in solution is sort the input integer array. And check if such subset already exists in the result.

This is [LeetCode problem 90](https://leetcode.com/problems/subsets-ii/description/).

Solution:

```python
class Solution:
    def __init__(self):
        self.result = []
        self.temp = []

    def subsetsWithDup(self, nums):
        sorted_nums = sorted(nums)
        self.nums = sorted_nums
        self.length = len(self.nums)

        self.backtrack(0)
        return self.result

    def backtrack(self,index):
        if index == self.length:
            # Test
            if(self.temp not in self.result):
                self.result.append(self.temp[:])
            return

        self.temp.append(self.nums[index])
        # Note: depth first search of possible subsets
        self.backtrack(index+1)
        if self.temp:
            self.temp.pop(-1)

        self.backtrack(index+1)


test  = [1,2,2]
answer = Solution().subsetsWithDup(test) #[[],[1],[1,2],[1,2,2],[2],[2,2]]
print(answer)
```
