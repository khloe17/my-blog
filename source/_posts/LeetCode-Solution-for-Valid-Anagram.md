---
title: LeetCode-Solution-for-Valid-Anagram
date: 2025-01-14 13:28:17
categories: [LeetCode, Algorithm]
tags: [Hash Table]
---

# Question

Given two strings s and t, return true if t is an anagram of s, and false otherwise.

## Explanation

Examples of Anagrams:
"listen" → "silent"
"evil" → "vile"
"cinema" → "iceman"

Key Characteristics of Anagrams:
They must use all the original letters exactly once.
The rearranged letters form a valid word or phrase in the same language.
Case and spacing are usually ignored, but some contexts may consider them.

Non-Examples (Not Anagrams):
"hello" → "olehl" (Not a valid word, so it's not an anagram.)

# Idea

Approach 1: Sort both strings
Sorting rearranges the characters in a consistent order, so if `s` and `t` are anagrams, their sorted versions will match.

Approach 2: Use a frequency counter
Count the occurrences of each character in `s` and `t`. If the frequency counts match, the strings are anagrams.

Approach 3: Manual character counting

1. Use an array of size 26 to count character frequencies.
2. Increment for characters in `s` and decrement for characters in `t`.
3. If the array contains all zeros, the string are anagrams.

Example for approach 3:
s = "anagram"
t = "nagaram"
count after s = [3, 0, 0, 0, 0, 0, ..., 1, ..., 1, 1, 0]
count after t = [0, 0, 0, 0, 0, 0, ..., 0, ..., 0, 0, 0]

Tips:

1. The all() function returns:

True if all elements in the iterable (like a list, tuple, or generator) are True.
False if any element is False.

2. The ord() function in Python is used to convert a character into its corresponding Unicode code point (integer value).

Example 1: Basic Characters
print(ord('a')) # Output: 97
print(ord('A')) # Output: 65
print(ord('z')) # Output: 122
print(ord('0')) # Output: 48
print(ord('$')) # Output: 36

Example 2: Spaces and Special Characters
print(ord(' ')) # Output: 32 (space character)
print(ord('\n')) # Output: 10 (newline character)

# Code

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return sorted(s) == sorted(t)

```

```python
import collections.Counter
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return Counter(s) == Counter(t)

```

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        count = [0] * 26 # for lowercase English letters

        for char in s:
            count[ord(char) - ord("a")]] += 1
        for char in t:
            count[ord(char) - ord("a")]] -= 1

        return all(c == 0 for c in count)

```
