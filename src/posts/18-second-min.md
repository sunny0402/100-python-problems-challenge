---
title: Python Challenge - Second Minimum Node In a Binary Tree
description: In a special binary tree find the second minimum node.
date: 2023-03-14
tags:
  - posts
layout: layouts/post.njk
---

This is [LeetCode problem 671](https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/description/).

For this binary tree all nodes follow: root.val = min(root.left.val, root.right.val).

In the set formed by all nodes need to find the second minimum.

Traverse inOrder and add nodes to the unique_nodes set.

Convert set to list and find second minimum.

Solution:

```python

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def __init__(self):
        self.unique_nodes = set()
    def findSecondMinimumValue(self, root):
        self.inOrder(root)
        node_list = list(self.unique_nodes)
        length = len(node_list)
        if length > 1:
            min = node_list[0]
            second_min =  node_list[1]
            if min > second_min:
                tmp = min
                min = second_min
                second_min = tmp
            for idx in range(2,length):
                if node_list[idx] < min:
                    min = node_list[idx]
                if  node_list[idx] < second_min:
                    second_min = node_list[idx]
            return second_min
        else:
            return -1

    def inOrder(self,curr_node):
        if curr_node == None:
            return
        self.inOrder(curr_node.left)
        if curr_node.val:
            self.unique_nodes.add(curr_node.val)
        self.inOrder(curr_node.right)

```

To test the code:

```python
from BST import TreeNode, myBST
# Note: create BST
treeA = myBST()
values = [5,3,6,2,4,1]
for val in values:
    treeA.my_insert(val)
root_node = treeA.root
print(str(root_node))

obj = Solution()
answer = obj.findSecondMinimumValue(root_node)
print(answer)

```

Output:

```python

 ┌─6
5
 |  ┌─4
 └─3
    └─2
       └─1

2

```
