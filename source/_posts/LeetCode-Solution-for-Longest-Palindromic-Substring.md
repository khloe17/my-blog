---
title: LeetCode-Solution-for-Longest-Palindromic-Substring
date: 2025-02-06 21:31:54
categories: [LeetCode, Algorithm]
tags: [String]
---

# Question

Given a string s, return the longest palindromic substring in s.

## Explanation

Example 1:
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.

Example 2:
Input: s = "cbbd"
Output: "bb"

# Idea

A few methods to solve this problem:

1. Brute force (O(n\*\*3)): Check all possible substrings to see if they are palindromes.
2. Expand around center (O(n\*\*2)): Expand from each character and consider odd-length palindrome(single character center e.g. racecar) and even-length palindrome situations (double character center e.g. abba)
3. Dynamic programming

# Code

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        # edge case: if the string is empty or has one character
        if len(s) <= 1:
            return s

        # variable to store the start and end of the longest palindrome
        start, end = 0, 0

        # helper function to find the longest palindrome by expanding outward from a center point
        def expandAroundCenter(lef: int, right: int):
            while left >= 0 and right < len(s) and s[left] == s[right]:
                left -= 1
                right += 1
            # return the start and end indices of the longest palindrome
            return left + 1, right - 1 \ The characters at left and right are no longer equal or the indices are out of bounds. The longest palindrome ends just before this point

        for i in range(len(s)):
            # check for odd-length palindromes
            l1, r1 = expandAroundCenter(i, i)
            # check for even-length palindromes
            l2, r2 = expandAroundCenter(i, i + 1)

            # update the longest palindrome if needed
            if r1 - l1 > end - start:
                start, end = l1, r1

            if r2 - l2 > end - start:
                start, end = l2, r2

        # return the longest palindromic substring
        return s[start:end + 1]





```
