---
title: Python Challenge -  Kth Smallest Element in a BST
description: Find a specific node in tree.
date: 2023-03-14
tags:
  - posts
layout: layouts/post.njk
---

This is [LeetCode problem 230](https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/).

InOrder traversal and add values to array. Return the element at index k - 1.

```python
class Solution:
    def __init__(self):
        self.tree = []
    def kthSmallest(self, root, k) -> int:
        self._inOrder(root)
        return self.tree[k-1]


    def _inOrder(self,curr_node):
        if curr_node == None:
            return
        else:
            self._inOrder(curr_node.left)
            self.tree.append(curr_node.val)
            self._inOrder(curr_node.right)
```
