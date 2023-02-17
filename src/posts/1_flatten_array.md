---
title: 1 - Flatten Array
description: First Problem of 100 Python Problem Challenge
date: 2023-03-17
tags:
  - posts
layout: layouts/post.njk
---

What if the data is super nested?

```py
result = []
def flatten(nested_list):
    for elem in nested_list:
        if isinstance(elem,int): #[2,[[2,3],4]]
            result.append(elem)
        elif isinstance(elem[0],int):#[2,3]
            for item in elem:
                result.append(item)
        elif isinstance(elem,list):
            flatten(elem[0])
    return result


# nested = [[1], [[2, 3]], [[[4]]]]
nested = [[1,1],2,[1,1]]
print(nested)
answer = flatten(nested)
print(answer) # [1, 2, 3, 4]
```
