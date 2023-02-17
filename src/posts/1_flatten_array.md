---
title: Python Flatten Nested Array
description: First Problem of 100 Python Problem Challenge!
date: 2023-03-17
tags:
  - posts
layout: layouts/post.njk
---

First problem of the 100 Python Problems challenge. Let's do this.

What if the data is super nested?

```python
nested = [ [0], [1,2], 3,4, [5,[[6,7]] ] ]
```

To unpack this array let's use recursion. Using the buil-in method **isinstance** we check whether the nested element is another list or an integer.

The trick is to put the recursive call inside a for loop. The for loop iterates over the nested elements and checks if those are lists or integers.

And we only append elements which are integers to the result.

```python
result = []
def flatten(nested_list):
    if isinstance(nested_list,list):
        for elem in nested_list:
            flatten(elem)
    elif isinstance(nested_list,int):
        result.append(nested_list)

    return result


nested = [ [0], [1,2], 3,4, [5,[[6,7]] ] ]
print(nested) # [[0], [1, 2], 3, 4, [5, [[6, 7]]]]
answer = flatten(nested)
print(answer) #[0, 1, 2, 3, 4, 5, 6, 7]
```

Using the same approach we can solve LeetCode problem [341. Flatten Nested List Iterator](https://leetcode.com/problems/flatten-nested-list-iterator/description/).

We are given a NestedInteger class which has three methods. We do not need to implement it, but need to figure out how use isInteger(), getInteger(), and getList().

```python
# """
# This is the interface that allows for creating nested lists.
# You should not implement it, or speculate about its implementation
# """
#class NestedInteger:
#    def isInteger(self) -> bool:
#        """
#        @return True if this NestedInteger holds a single integer, rather than a nested list.
#        """
#
#    def getInteger(self) -> int:
#        """
#        @return the single integer that this NestedInteger holds, if it holds a single integer
#        Return None if this NestedInteger holds a nested list
#        """
#
#    def getList(self) -> [NestedInteger]:
#        """
#        @return the nested list that this NestedInteger holds, if it holds a nested list
#        Return None if this NestedInteger holds a single integer
#        """
```

<br/>
We need flatten a nested list and create an iterator to iterate over the result.
<br/>
<br/>
So our solution class NestedIterator will have a flatten() method, which is immediately called by the constructor. And two helper methods to see if there is a next item and to return the next item.

```python
class NestedIterator:
    def __init__(self, nestedList):
        self.iterator_idx = -1
        self.result = []
        self.flatten(nestedList)

    def flatten(self,nested_list):
        for elem in nested_list:
            if elem.isInteger():
                self.result.append(elem.getInteger())
            else:
                self.flatten(elem.getList())


    def next(self) -> int:
        self.iterator_idx = self.iterator_idx + 1
        return self.result[self.iterator_idx]


    def hasNext(self) -> bool:
        next = self.iterator_idx + 1
        if next < len(self.result):
            return True
        else:
            return False
```
