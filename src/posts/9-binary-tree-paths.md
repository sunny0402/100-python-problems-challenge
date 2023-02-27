---
title: Python Challenge - Binary Search Tree Paths
description: Generate all paths from root to leaf.
date: 2023-03-26
tags:
  - posts
layout: layouts/post.njk
---

This is [LeetCode problem 257](https://leetcode.com/problems/binary-tree-paths/description/).

The goal is to generate all paths from the root node to a leaf.

We're provided a TreeNode class:

<br/>

```python

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

<br/>

If you want to test your code you can extend the class to create binary search tree.

Check out this great video to learn more about the [Python code for BSTs](https://www.youtube.com/watch?v=f5dU3xoE6ms&list=PLEJyjB1oGzx3iTZvOVedkT8nZ2cG105U7&index=5).

This is the GitHub repo associated with the YouTube video.[Link](https://github.com/bfaure/Python3_Data_Structures)

<br/>

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

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

    def _inOrderTraverse(self,curr_node: TreeNode):
        if curr_node is None:
            return

        self._inOrderTraverse(curr_node.left)
        print(curr_node.val)
        self._inOrderTraverse(curr_node.right)
```

<br/>

Finally the solution is a list of string paths:

<br/>

```python
['10->5->3', '10->5->7', '10->15->12', '10->15->20']
```

<br/>

Solution:

<br/>

```python

class Solution:
    def __init__(self):
        self.all_paths = []

    def _allPaths(self, curr_node, current_path):
        if curr_node:
            if current_path:
                current_path += '->' + str(curr_node.val)
            else:
                current_path = str(curr_node.val)

            #Note: if leaf node
            if not curr_node.left and not curr_node.right:
                self.all_paths.append(current_path)
                return

            else: #Note extend path
                self._allPaths(curr_node.left,current_path)
                self._allPaths(curr_node.right,current_path)



    def binaryTreePaths(self, root:TreeNode):
        self._allPaths(root,"")
        print(self.all_paths)
        return self.all_paths
```

And this is how to test your solution locally provided you create the BST class as described above.

<br/>

```python
if __name__ == "__main__":
    tree = myBST()

    tree.my_insert(10)

    tree.my_insert(5)
    tree.my_insert(7)
    tree.my_insert(3)

    tree.my_insert(15)
    tree.my_insert(12)
    tree.my_insert(20)

    root_node = tree.root

    Solution().binaryTreePaths(root_node)
```

<br/>
<br/>
