---
title: LeetCode-Solution-for-Reverse-Words-in-a-String
date: 2025-02-07 06:58:44
categories: [LeetCode, Algorithm]
tags: [String]
---

# Question

Given an input string s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

## Explanation

Multiple spaces are reduced to a single space.
Reverse the words: "a good example" → "example good a".

Example 1:
Input: s = "the sky is blue"
Output: "blue is sky the"

Example 2:
Input: s = " hello world "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.

Example 3:
Input: s = "a good example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.

# Idea

Approach 1: Split and reverse

1. Trim leading and trailing spaces
2. Split the string into words using split(), which automatically removes extra spaces
3. Reverse the list of words
4. Join the reversed words into a single string

Approach 2: Two pointer

1. Remove leading and trailing spaces
2. Reverse the entire string
3. Reverse each word back to its correct form
4. Reduce multiple spaces to single spaces while rebuilding the final string

Tips:

1. The strip() method removes any leading, and trailing whitespaces.
2. The reverse() method reverses the elements of the list in-place and it modify the original list without creating a new list.

   a = [1, 2, 3, 4, 5]

   # Reverse the list in-place

   a.reverse()

3. The join() method takes all items in an iterable and joins them into one string.

   input:
   myTuple = ("Apple", "Banana", "Orange")
   x = "#".join(myTuple)
   print(x)

   output:
   Apple#Banana#Orange

4. Different method for reversing a list in python

1) Using reverse() method
2) Using List Slicing
   e.g.
   a = [1, 2, 3, 4, 5]

   # Create a new list that is a reversed list using slicing

   rev = a[::-1]

3. Using the reversed()

   Python’s built-in reversed() function is another way to reverse the list. However, reversed() returns an iterator, so it needs to be converted back into a list.
   e.g.
   a = [1, 2, 3, 4, 5]

   # Use reversed() to create an iterator and convert it back to a list

   rev = list(reversed(a))

4. Using List Comprehension
   e.g.
   a = [1, 2, 3, 4, 5]

   # Use list comprehension to create

   # a reversed version of the list

   rev = [a[i] for i in range(len(a) - 1, -1, -1)]

# Code

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        # trim spaces
        s = s.strip()
        s = s.split()
        # reverse entire string
        s.reverse()
        s = " ".join(s)
        return s

        # return " ".join(s.strip().split()[::-1])

```

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        """
        remove space->change to string with single space->convert string to list->reverse the entire list->reverse each word in the list->convert list back to string

        change process:
        "  hello   world  " -> "hello world" -> ['h', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd'] -> "dlrow olleh" -> "world hello"

        """
        def trim_spaces(s):
            return " ".join(s.split()) # manually remove spaces

        def reverse(l, r, arr):
            while l < r:
                arr[l], arr[r] = arr[r], arr[l]
                l += 1
                r -= 1

        # convert string to list to mutate it
        s = list(trim_spaces(s))
        n = len(s)

        # reverse the entire list
        reverse(0, n - 1, s)

        # reverse each word
        start = 0
        for end in range(n + 1): # traverse the string (including last position n)
            if end == n or s[end] == ' ': # reach the end of string or find a space
                reverse(start, end - 1, s)
                start = end + 1 # move start to next word

        return "".join(s)




```
