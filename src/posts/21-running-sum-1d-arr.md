---
title: Python Challenge -  Running Sum of 1d Array
description: Calculate the cumulative sum.
date: 2023-03-14
tags:
  - posts
layout: layouts/post.njk
---

This is [LeetCode problem 1480](https://leetcode.com/problems/running-sum-of-1d-array/description/).

Solution:

```python
class Solution:
    def runningSum(self, nums):
        n = len(nums)
        sum = [nums[0]]
        for idx in range(1,n):
            sum.append(sum[idx - 1] + nums[idx])

        return sum
```
