---
title: Python Challenge - Two Sum with BST Input
description: Find if two elements in BST sum to the target.
date: 2023-03-05
tags:
  - posts
layout: layouts/post.njk
---

This is [LeetCode problem 653](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/description/).

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
        self.nodes_visited = set()
        self. q = []

    def findTarget(self, root: TreeNode, k: int) -> bool:
        self.q.append(root)
        while self.q:
            curr_node = self.q.pop(0)
            if curr_node:
                if k - curr_node.val in self.nodes_visited:
                    return True
                else:
                    self.nodes_visited.add(curr_node.val)

                self.q.append(curr_node.left)
                self.q.append(curr_node.right)
        return False


# Note: create BST
treeA = myBST()
values = [5,3,6,2,4,7]
for val in values:
    treeA.my_insert(val)
root_node = treeA.root

print(str(root_node))

# Note: test function
k = 9
obj = Solution()
exists = obj.findTarget(root_node,k)
print(exists)

k = 28
obj = Solution()
exists = obj.findTarget(root_node,k)
print(exists)

```

<br/>
<br/>

```python
    ┌─7
 ┌─6
5
 |  ┌─4
 └─3
    └─2
True
False
```
