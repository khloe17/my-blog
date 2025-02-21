---
title: LeetCode-Solution-for-Permutation-in-String
date: 2025-02-14 17:16:06
tags:
---

# Question

Given two strings s1 and s2, return true if s2 contains a
permutation of s1, or false otherwise.

In other words, return true if one of s1's permutations is the substring of s2.

## Explanation

Example 1:
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").

Example 2:
Input: s1 = "ab", s2 = "eidboaoo"
Output: false

# Idea

1. The length of the substring to check is len(s1).
2. Instead of generating all substrings, we can slide a window of size len(s1) across s2 and compare character frequencies.
3. Sliding window technique efficiently updates the character frequency count in O(n) time.

# Code

```python
from collections import Counter

class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        if len(s1) > len(s2):
            return False  # If s1 is longer than s2, it's impossible to find a permutation

        # Step 1: Frequency counts for s1 and the first window in s2
        s1_count = Counter(s1)
        s2_count = Counter(s2[:len(s1)])  # Initial window of s2

        # Step 2: Slide the window across s2
        l = 0  # Left pointer
        for r in range(len(s1), len(s2)):
            if s1_count == s2_count:
                return True  # Found a permutation

            # Remove the leftmost character of the window
            s2_count[s2[l]] -= 1
            if s2_count[s2[l]] == 0:
                del s2_count[s2[l]]  # Remove the character if its count becomes zero
            l += 1  # Move the left pointer

            # Add the new character at the right end
            s2_count[s2[r]] += 1

        # Final check for the last window
        return s1_count == s2_count


```
