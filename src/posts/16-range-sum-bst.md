---
title: Python Challenge - Find Range Sum of BST
description: Given a range find the sum of all nodes in that range.
date: 2023-03-05
tags:
  - posts
layout: layouts/post.njk
---

This is [LeetCode problem 938](https://leetcode.com/problems/range-sum-of-bst/description/).

```python
from BST import TreeNode, myBST
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def __init__(self):
        self.sum = 0

    def rangeSumBST(self, root: TreeNode, low: int, high: int) -> int:
        if root == None:
            return
        if high < root.val:
            self._calculateSum(root.left,low,high)
        elif low > root.val:
            self._calculateSum(root.right,low,high)
        else:
            self._calculateSum(root,low,high)

        return self.sum

    def _calculateSum(self,curr_node: TreeNode, low: int, high: int) -> int:
        if curr_node == None:
            return

        # if curr_node.val > high or curr_node.val < low:
        #     return

        if curr_node.val in range(low,high+1):
            self.sum += curr_node.val

        if curr_node.val < low:
            self._calculateSum(curr_node.right,low,high)
        elif curr_node.val > high:
            self._calculateSum(curr_node.left,low,high)
        else:
            self._calculateSum(curr_node.left,low,high)
            self._calculateSum(curr_node.right,low,high)


# Note: create BST
treeA = myBST()
values = [10,5,15,3,7,18]
for val in values:
    treeA.my_insert(val)
root_node = treeA.root

print(str(root_node))


# Note: test function
low = 7
high = 15
obj = Solution()
obj.rangeSumBST(root_node,low,high)
sum = obj.sum #Note: 10 + 15 + 7 = 32
print(sum)
```
