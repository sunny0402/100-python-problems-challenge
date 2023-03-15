---
title: Python Challenge -  Subarray Sum Equals K
description: Number of subarrays which total the target.
date: 2023-03-14
tags:
  - posts
layout: layouts/post.njk
---

A solution that is too slow. n^2 time.

Calculate whether the current cumulative sum totals the target.

Cumulative sum is calculated for all subarrays.

```python

    def subarraySum(self, nums: int, k: int):
        n = len(nums)
        if(n==1):
            if k == nums[0]:
                return 1
            else:
                return 0

        num_sub_arr_equal_k = 0
        sum = [None]*(n+1)
        sum[0] = 0


        for start_index in range(n):
            curr_sum = 0
            for end_index in range(start_index,n):
                curr_sum = curr_sum + nums[end_index]
                if curr_sum == k:
                    num_sub_arr_equal_k += 1

        return num_sub_arr_equal_k


```

Solution using a hash map to keep track of a "prefix" sum.

1. Calculate the cumulative sum.
2. If prefix sum update count.
3. Add sum to hash map.

Solution:

```python
class Solution:
    def subarraySum(self, nums: int, k: int):
        map = {0:1}
        sum = 0
        count = 0
        for elem in nums:
            sum = sum + elem
            prefix = sum - k
            if prefix in map:
                count = count + map[prefix]

            if sum in map:
                map[sum] = map[sum] + 1
            else:
                map[sum] = 1

        return count
```
