---
title: Python Challenge - Binary Tree Level Order Traversal
description: Use breadth first search to traverse a binary tree.
date: 2023-02-28
tags:
  - posts
layout: layouts/post.njk
---

This is [LeetCode problem 102](https://leetcode.com/problems/binary-tree-level-order-traversal/description/).

<br/>

You are given the root node of a binary tree and need to traverse the tree in level order. Return an array for each level of the tree.

For each level will pop from the front of queue and push to the end. The length of the queue at each level of the tree will be determined by the number of children nodes. So as we remove a node from the queue we add it's children.

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
        self.result = []
        self.my_q = []

    def levelOrder(self, root: TreeNode):
        #Note: the root node has reference to all other nodes in tree
        self.my_q.append(root)

        # Note: while queue not empty
        while self.my_q:
            level = []
            length_q = len(self.my_q)
            # Note; at each level the length of q is different
            for index in range(length_q):
                node = self.my_q.pop(0)
                if node:
                    level.append(node.val)
                    if node.left:
                        self.my_q.append(node.left)
                    if node.right:
                        self.my_q.append(node.right)

            #Note: add the level to the result
            if level:
                self.result.append(level)

        return self.result



# Note: test
tree = myBST()

tree.my_insert(10)
tree.my_insert(5)
tree.my_insert(7)
tree.my_insert(3)

tree.my_insert(15)
tree.my_insert(12)
tree.my_insert(20)

root_node = tree.root

obj = Solution()
obj.levelOrder(root_node)
result = obj.result

print(result)

```
