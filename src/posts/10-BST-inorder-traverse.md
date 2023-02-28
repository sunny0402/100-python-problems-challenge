---
title: Python Challenge - Binary Tree Inorder Traversal
description: Traverse Binary Tree Inorder
date: 2023-03-27
tags:
  - posts
layout: layouts/post.njk
---

This is [LeetCode problem 94](https://leetcode.com/problems/binary-tree-inorder-traversal/description/).

<br/>

```python
class Solution:
    def __init__(self):
        self.inOrderArray = []

    def inorderTraversal(self, root):
        self._inOrder(root)
        return self.inOrderArray

    def _inOrder(self, curr_node):
        if curr_node == None:
            return
        else:
            if curr_node.left:
                self._inOrder(curr_node.left)
            self.inOrderArray.append(curr_node.val)
            if curr_node.right:
                self._inOrder(curr_node.right)

    # Note: or simply
    # def _inOrder(self, curr_node):
    #     if curr_node == None:
    #         return

    #     self._inOrder(curr_node.left)
    #     self.inOrderArray.append(curr_node.val)
    #     self._inOrder(curr_node.right)
```
