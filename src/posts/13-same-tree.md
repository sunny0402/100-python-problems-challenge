---
title: Python Challenge - Same Tree?
description: Confirm that two binary trees are the same.
date: 2023-03-02
tags:
  - posts
layout: layouts/post.njk
---

This is [LeetCode problem 100](https://leetcode.com/problems/same-tree/description/).

This is how my binary search tree class look like, notice the repr function.

```python
# Definition for a binary tree node.
import sys
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# Note: https://stackoverflow.com/questions/62406562/how-to-print-a-binary-search-tree-in-python
    def __repr__(self):
        lines = []
        if self.right:
            found = False
            for line in repr(self.right).split("\n"):
                if line[0] != " ":
                    found = True
                    line = " ┌─" + line
                elif found:
                    line = " | " + line
                else:
                    line = "   " + line
                lines.append(line)
        lines.append(str(self.val))
        if self.left:
            found = False
            for line in repr(self.left).split("\n"):
                if line[0] != " ":
                    found = True
                    line = " └─" + line
                elif found:
                    line = "   " + line
                else:
                    line = " | " + line
                lines.append(line)
        return "\n".join(lines)

class myBST:
    def __init__(self):
        self.root = None

    def my_insert(self,value):
        if self.root == None:
            self.root = TreeNode(value)
            return
        self._recursive_insert(value,self.root)

    def _recursive_insert(self,value,curr_node: TreeNode):
        if value < curr_node.val:
            if curr_node.left == None:
                curr_node.left = TreeNode(value) #Note: insert
            elif curr_node.left is not None:
                self._recursive_insert(value,curr_node.left) #Note: traverse left

        elif value > curr_node.val:
            if curr_node.right == None:
                curr_node.right = TreeNode(value) #Note: insert
            elif curr_node.right is not None:
                self._recursive_insert(value, curr_node.right)
        else:
            print("Node already in tree")

    # Note: InOrder traversal
    def _inOrderTraverse(self,curr_node: TreeNode):
        if curr_node is None:
            return

        self._inOrderTraverse(curr_node.left)
        print(curr_node.val)
        self._inOrderTraverse(curr_node.right)



    # Note: Validate BST
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

We just have to compare node values in left and right subtree.

<br/>

```python

from BST import TreeNode, myBST
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:

    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if p == None and q == None:
            return True
        # Note: we already checked if both are none, so here only one will be none
        if p == None or q == None:
             return False

        if p.val != q.val:
            return False

        if p.val == q.val:
            return self.isSameTree(p.left,q.left) and self.isSameTree(p.right,q.right)


treeA = myBST()
nodes_a = [10,5,7,3,15,12,20]
for val in nodes_a:
    treeA.my_insert(val)

root_node_A = treeA.root

print(str(root_node_A))

print("*"*20)

treeB = myBST()
nodes_b = [10,5,7,3,15,12,22]
for val in nodes_b:
    treeB.my_insert(val)

root_node_B = treeB.root

print(str(root_node_B))



obj = Solution()
isSame = obj.isSameTree(root_node_A, root_node_B)
print(isSame)
```
