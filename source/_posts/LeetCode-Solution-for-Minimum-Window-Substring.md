---
title: LeetCode-Solution-for-Minimum-Window-Substring
date: 2025-02-16 21:42:44
categories: [LeetCode, Algorithm]
tags: [String]
---

# Question

Given two strings s and t of lengths m and n respectively, return the minimum window substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

## Explanation

Example 1:
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

Example 2:
Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.

Example 3:
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.

# Idea: Sliding window

1. We expand the right pointer to include characters until we have all of `t`.
2. Once all characters are included, we shrink the left pointer to minimize the window.
3. Keep track of the smallest valid window.

Tips:
A window is valid when it contains all the characters of `t` in the required frequency.

How do we track validity?
We use a formed variable that keeps track of how many unique characters in t are fully matched in the current window.

# Code

```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if not s or not t:
            return ""

        # frequency count of characters in t
        t_count = Counter(t)
        window_count = {}

        required = len(t_count) # unique characters in t that need to be in window
        formed = 0 # track how many unique characters meet the required frequency. It helps track when we have a valid substring, so that we can try to shrink the window length.
        l, r = 0, 0
        min_length = float('inf')
        start_index = 0 # start index of the minimum window

        # expand the right pointer
        while r < len(s):
            char = s[r]
            window_count[char] = window_count.get(char, 0) + 1

            # if character count matches the t_count, increase formed
            if char in t_count and window_count[char] == t_count[char]:
                formed += 1

            # contract the left pointer to minimize the window
            while l <= r and formed == required:
                # update minimum window size
                if (r - l + 1) < min_length:
                    min_length = r - l + 1
                    start_index = l

                # remove the leftmost character
                window_count[s[l]] -= 1
                if s[l] in t_count and window_count[s[l]] < t_count[s[l]]:
                    formed -= 1 # a required character is now missing

                l += 1 # move left pointer forward

            r += 1 # expand right pointer

        # return the smallest valid window
        return s[start_index:start_index + min_length] if min_length != float('inf') else ""

```
