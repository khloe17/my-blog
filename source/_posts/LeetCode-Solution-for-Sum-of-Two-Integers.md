---
title: LeetCode-Solution-for-Sum-of-Two-Integers
date: 2025-01-17 16:34:30
categories: [LeetCode, Algorithm]
tags: Bit Manipulation
---

# Question

Given two integers a and b, return the sum of the two integers without using the operators + and -.

## Explanation

Example 1:
Input: a = 1, b = 2
Output: 3

Example 2:
Input: a = 2, b = 3
Output: 5

# Idea: Bitwise operators (XOR + AND + <<)

1. Perform addition without carrying: Use XOR to get sum without carry (不进位情况)
   a ^ b = 01 ^ 10 = 11 (3 in decimal)
2. Detect where a carry is needed: Use AND to get carry (获得进位)
   a & b = 01 & 10 = 00 (no carry)
3. Left shift (<<): Move the carry to the left by one bit to add it in the next place value

Tips:

1. Exclusive OR (XOR):
   1 XOR 1 = 0
   1 XOR 0 = 1
   0 XOR 1 = 1
   0 XOR 0 = 0

2. Operations about negative numbers:

1) MASKing: Use result & MASK to keep only 32 bits.
2) Check for Negative: If result > MAX, it’s negative.
3) Convert to Signed: Use ~(result ^ MASK) to handle two’s complement conversion.

# Code

```python
class Solution:
    def getSum(self, a: int, b: int) -> int:
        # define constants for 32-bit integer representation
        MASK = 0xFFFFFFFF # all 1s for 32-bit integer
        MAX = 0x7FFFFFFF # maximum positive integer is 32 bits

        while b != 0:
            # calculate the sum without carry
            temp = (a ^ b) & MASK
            # calculate carry
            b = ((a & b) << 1) & MASK
            # update a to the sum
            a = temp

        return a if a <= MAX else ~(a ^ MASK)

```
