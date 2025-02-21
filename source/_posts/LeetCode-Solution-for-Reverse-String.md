---
title: LeetCode-Solution-for-Reverse-String
date: 2025-02-06 21:17:06
categories: [LeetCode, Algorithm]
tags: [String]
---

# Question

Write a function that reverses a string. The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.

## Explanation

Example 1:
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]

Example 2:
Input: s = ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]

# Idea: Two pointers

1. Initialize two pointers:
   left starting at index 0 (beginning).
   right starting at index n - 1 (end).

2. While left < right:
   Swap s[left] and s[right].
   Move left forward (left += 1).
   Move right backward (right -= 1).

# Code

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        left, right = 0, len(s) - 1
        while left < right:
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1

```
