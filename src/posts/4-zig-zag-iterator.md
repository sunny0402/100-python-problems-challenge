---
title: Python Challenge - Zig Zag Iterator
description: Return element from two vectors alternatively.
date: 2023-02-18
tags:
  - posts
layout: layouts/post.njk
---

This is LeetCode problem [281. Zigzag Iterator](https://leetcode.com/problems/zigzag-iterator/description/).

Return values from the first vector then the second and so forth.

Input: v1 = [1,2], v2 = [3,4,5,6]
Output: [1,3,2,4,5,6]

Apply the same approach as the iterator problem to [flatten an array](https://100-python-problems-challenge.netlify.app/posts/1-flatten_array/).

Iterators have a next() and hasNext() method.

```python
def next(self) -> int:
    if self.hasNext():
        self.position += 1
        return self.result[self.position]

def hasNext(self) -> bool:
    next = self.position + 1
    if next <  self.result_length:
        return True
    else:
        return False
```

</br>
</br>

Use a couple pointers as in merge sort to merge element into a common result array.

<br/>

```python
class ZigzagIterator:
    def __init__(self, v1, v2):
        self.len1 = len(v1)
        self.len2 = len(v2)
        self.position = -1
        self.result = []
        self.result_length = 0
        self.populateIterator(v1,v2)

    def populateIterator(self,v1,v2):
        p1,p2 = 0,0
        while p1 < self.len1 and p2 < self.len2:
            self.result.append(v1[p1])
            p1+=1
            self.result.append(v2[p2])
            p2+=1
        while p1 < self.len1:
            self.result.append(v1[p1])
            p1 +=1
        while p2 < self.len2:
            self.result.append(v2[p2])
            p2+=1
        self.result_length = len(self.result)


    def next(self) -> int:
        if self.hasNext():
            self.position += 1
            return self.result[self.position]

    def hasNext(self) -> bool:
        next = self.position + 1
        if next <  self.result_length:
            return True
        else:
            return False
```

<br/>
The output:
<br/>

```python
#Test
v1 = [1,2]
v2 = [3,4,5,6]
i, v = ZigzagIterator(v1, v2), []
while i.hasNext():
    v.append(i.next())
print(v) #[1, 3, 2, 4, 5, 6]
```

<br/>
Generalizing the solution for k vectors would a good next step!
<br/>
