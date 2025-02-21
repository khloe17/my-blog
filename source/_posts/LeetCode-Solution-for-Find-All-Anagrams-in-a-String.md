---
title: LeetCode-Solution-for-Find-All-Anagrams-in-a-String
date: 2025-02-14 14:34:51
categories: [LeetCode, Algorithm]
tags: [String]
---

# Question

Given two strings s and p, return an array of all the start indices of p's anagrams in s. You may return the answer in any order.

## Explanation

An anagram is a rearrangement of characters.
The order of letters doesn’t matter, but the frequency of each letter must be the same.

Example 1:
Input: s = "cbaebabacd", p = "abc"
Output: [0,6]
Explanation:
The anagrams of "abc" in "cbaebabacd" are:
"cba" at index 0
"bac" at index 6

Example 2:
Input: s = "abab", p = "ab"
Output: [0,1,2]
Explanation:
The anagrams of "ab" in "abab" are:
"ab" at index 0
"ba" at index 1
"ab" at index 2

# Idea: Sliding window

1. The string `p` has a fixed length.
2. Instead of generating all substrings, we can slide a window of length `len(p)` across `s`.
3. We can check if the character frequency of the current window matches `p`.

# Code

```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        if len(p) > len(s):
            return [] # edge case: if p is longer than s, no anagrams possible

        p_count = Counter(p)
        s_count = Counter(s[:len(p)-1]) # initialize with the first possible word with length of word p

        result = []
        l = 0

        for r in range(len(p)-1, len(s)):
            s_ count[s[r]] += 1 # add new character to window

            # check if window matches p_count
            if s_count == p_count:
                result.append(l) # find an anagram

            # remove the leftmost character to slide window
            s_count[s[l]] -= 1
            if s_count[s[l]] == 0:
                del s_count[s[l]] # remove char from hashmap if count is 0
            l += 1 # move window forward

        return result



```
