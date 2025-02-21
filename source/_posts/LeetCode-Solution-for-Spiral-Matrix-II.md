---
title: LeetCode-Solution-for-Spiral-Matrix II
date: 2025-02-13 18:53:56
categories: [LeetCode, Algorithm]
tags: [Array]
---

# Question

Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order.

## Explanation

Example 1:
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]

![Local image](./images/59_1.png "Spiral matrix generation explanation")

Example 2:
Input: n = 1
Output: [[1]]

# Idea

1. Initialize a n x n matrix filled with 0.
2. Set up the boundaries: top = 0, bottom = n - 1, left = 0, right = n - 1.
3. Start filling numbers from 1 to n^2:
   Left to Right: Fill top row, then increase top
   Top to Bottom: Fill rightmost column, then decrease right.
   Right to Left: Fill bottom row (if top <= bottom), then decrease bottom.
   Bottom to Top: Fill leftmost column (if left <= right), then increase left.
4. Repeat until we fill all numbers.

# Code

```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        matrix = [[0] * n for _ in range(n)] # initialize an n x n matrix

        top, bottom, left, right = 0, n - 1, 0, n - 1
        num  = 1 # start with 1

        while num <= n * n:
            # traverse from left to right
            for i in range(left, right + 1):
                matrix[top][i] = num
                num += 1
            top += 1 # move the top boundary down

            # traverse from top to bottom
            for i in range(top, bottom + 1):
                matrix[i][right] = num
                num += 1
            right -= 1

            # traverse from right to left
            if top <= bottom:
                for i in range(right, left - 1, -1):
                    matrix[bottom][i] = num
                    num += 1
                bottom -= 1 # move the bottom boundary up

            # traverse from bottom to top
            if left <= right:
                for i in range(bottom, top - 1, -1):
                    matrix[i][left] = num
                    num += 1
                left += 1 # move the left boundary right

        return matrix


```
