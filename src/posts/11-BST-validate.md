---
title: Python Challenge - Validate Binary Search Tree
description: Validate a binary search tree.
date: 2023-03-27
tags:
  - posts
layout: layouts/post.njk
---

This is [LeetCode problem 98](https://leetcode.com/problems/validate-binary-search-tree/description/).

<br/>

One way to solve this problem would be traverse the BST in-order and save the nodes to an array.
If the array is sorted then the BST is valid.

Another approach is propagate a set of constraints on each node in the tree.

For example the root node's left child must be greater than the minimum and less than the root node.
If we go left again. So root.left.left. Then the node must be again greater than the minimum and less than node before it.

Solution:

<br/>

```python
import sys
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def _validator(self, curr_node ,min= -sys.maxsize, max=sys.maxsize):
        if curr_node == None:
            return True
        else:
            if (curr_node.val > min and \
                curr_node.val < max and \
                self._validator(curr_node.left,min, curr_node.val) and \
                self._validator(curr_node.right,curr_node.val,max)):
                return True
            else:
                return False

    def isValidBST(self, root: TreeNode) -> bool:
        return self._validator(root)

```
