---
title: Python Challenge - Remove Duplicates
description: Remove duplicate characters from a string.
date: 2023-03-18
tags:
  - posts
layout: layouts/post.njk
---

To remove duplicate characters from a string we can use a Python dictionary.

Look up in a Python dictionary is fast because it basically serves as a hash table. Sp look up is O(1).

And duplicate keys are not allowed. Or more accurately the the key will be overwritten if you add it more than once.

So to remove duplicate characters we iterate over the string add unique characters to the dictionary.

```python
# Using hash table/dictionary
def removeDuplicate(a_string):
    dictionary = {}
    length = len(a_string)
    for idx in range(length):
        if ( a_string[idx] not in dictionary):
            dictionary[a_string[idx]] = True
    result = dictionary.keys()
    return "".join(result)

print(removeDuplicate('qwe')) #'qwe'
print(removeDuplicate('qqwwee')) #'qwe'
print(removeDuplicate('qweeqweeqqww')) #'qwe'
```

We can apply a similar technique to a tricky problem LeetCode problem [316. Remove Duplicate Letters](https://leetcode.com/problems/remove-duplicate-letters/description/).

The hard part here is that the resulting string must be in the smallest lexicographical order.

Basically, letters that appear earlier in the alphabet must be at the start of the string.

Input: s = "bcabc"
Output: "abc"

Input: s = "cbacdcbc"
Output: "acdb"

So our function will preserver the order the character appear in, but remove duplicates and make sure in smallest lexicographical order.

The hard part is the while loop.

```python
        while (my_stack and ((my_stack[-1] > char) and \
                                      (idx < last_index[my_stack[-1]]) ) ):
```

We pop from the stack when:

- the character at the top of stack is larger than current character
- AND the character at the top of the stack occurs later in the string

If the character occurs later we can add it to the stack later, thus smallest lexicographical order.

```python
class Solution:
    def removeDuplicateLetters(self, s: str) -> str:
        last_index = {}
        for i,c in enumerate(s):
            last_index[c] = i
        my_stack = []
        for idx,char in enumerate(s):
            if char not in my_stack:
                # Note: last char > current chart or last char occurs later, thus can add later
                while (my_stack and ((my_stack[-1] > char) and \
                                      (idx < last_index[my_stack[-1]]) ) ):
                    my_stack.pop()
                #Note: after done as much removing from stack as possible add the char
                my_stack.append(char)

        return "".join(my_stack)

# Test
answer = Solution().removeDuplicateLetters("cbacdcbc")
print(answer)
```
