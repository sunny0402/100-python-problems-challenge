---
title: Python Challenge - Symmetric Binary Tree?
description: Validate the binary tree is a mirror of itself.
date: 2023-03-02
tags:
  - posts
layout: layouts/post.njk
---

This is [LeetCode problem 100](https://leetcode.com/problems/symmetric-tree/description/).

Symmetric means mirror image. So right is left and left is right. Notice which children nodes are passed into the recursive calls. Again we compare the left and right subtree, starting at their roots.

```python
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        # Note: left subtree equals right subtree
        return self._compareSubtrees(root.left,root.right)

    def _compareSubtrees(self, root_left: TreeNode, root_right: TreeNode):
        if root_left == None and root_right == None:
            return True

        # Note: already checked if both are None
        # so here catch if one is None and other is not
        if root_left == None or root_right == None:
            return False

        if root_left.val != root_right.val:
                return False
        # Note: root_left.left == root_right.right
        # and root_left.right == root_right.left
        return (root_left.val == root_right.val) and \
                self._compareSubtrees(root_left.left, root_right.right) and \
                self._compareSubtrees(root_left.right,root_right.left)
```
