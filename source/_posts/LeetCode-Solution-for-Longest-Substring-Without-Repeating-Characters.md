---
title: LeetCode-Solution-for-Longest-Substring-Without-Repeating-Characters
date: 2025-02-14 11:17:51
categories: [LeetCode, Algorithm]
tags: [String]
---

# Question

Given a string s, find the length of the longest substring without repeating characters.

## Explanation

Example 1:
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

Example 2:
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

# Idea: Sliding window

1. Expand the right pointer to add new characters.
2. If a duplicate appears, move the left pointer forward to remove duplicates.
3. Maintain a set of unique characters for quick lookup.

# Code

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        seen = set() # store unique characters
        l = 0 # left pointer
        max_length = 0 # store max length

        for r in range(len(s)):
            while s[r] in seen: # if duplicate found, move left pointer
                seen.remove(s[l])
                l += 1

            seen.add(s[r]) # add unique character
            max_length = max(max_length, r - l + 1)

        return max_length



```
