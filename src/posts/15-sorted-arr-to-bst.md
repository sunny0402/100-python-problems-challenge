---
title: Python Challenge - Sorted Array to BST
description: Given an array with elements in ascending order, return a height-balanced BST.
date: 2023-03-04
tags:
  - posts
layout: layouts/post.njk
---

This is [LeetCode problem 108](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/).

```python
from BST import TreeNode, myBST
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
      def sortedArrayToBST(self, nums) -> TreeNode:
        def _makeBST(left_idx, right_idx):
            if left_idx > right_idx:
                return

            mid = (left_idx + right_idx)//2

            new_node = TreeNode(nums[mid])

            new_node.left = _makeBST(left_idx,mid -1 )

            new_node.right = _makeBST(mid+1,right_idx)

            return new_node

        return _makeBST(0,len(nums) -1)



obj = Solution()
nums = [-10,-3,0,5,9]
heightBalancedBST = obj.sortedArrayToBST(nums)
root_node = heightBalancedBST

print(str(root_node))
```

Output:

```python
    ┌─9
 ┌─5
0
 |  ┌─-3
 └─-10
```
