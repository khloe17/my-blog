---
title: LeetCode-Solution-for-Spiral-Matrix
date: 2025-02-09 15:02:30
categories: [LeetCode, Algorithm]
tags: Array
---

# Question

Given an m x n matrix, return all elements of the matrix in spiral order.

## Explanation

Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]

![Local image](./images/54_1.png "Spiral Matrix")

# Idea

1. Initialize boundaries to represent the outer boundaries of the matrix.
2. Traverse in four directions (right, down, left, up), adding elements to the result in each direction.
3. After completing a pass in each direction, adjust the boundaries inward.
   更新逻辑： 每次遍历完一圈后，向内收缩边界以进入下一层的螺旋：
   完成顶部行的遍历后，将 top 增加 1，收缩上边界。
   完成右侧列的遍历后，将 right 减少 1，收缩右边界。
   完成底部行的遍历后，将 bottom 减少 1，收缩下边界。
   完成左侧列的遍历后，将 left 增加 1，收缩左边界。
4. Repeat the process until all elements are added to the result.

Tips:
Edge Case Walkthrough
Example 3: 1×4 Matrix (Single Row)

1 2 3 4

First traversal: 1 → 2 → 3 → 4 (left to right).
Now, top = 1, bottom = 0 (no more rows left).
Without if top <= bottom, the code might try to traverse bottom to top, which does not exist.
if top <= bottom prevents unnecessary operations.

# Code

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:

        result = []
        if not matrix:
            return result

        # initialize boundaries index
        top, bottom = 0, len(matrix) - 1
        left, right = 0, len(matrix[0]) - 1

        while top <= bottom and left <= right: \ 使用and逻辑的原因：只有在 top <= bottom 且 left <= right 时，我们才有一个有效的矩形区域（即还有行和列未被遍历），可以继续进行螺旋遍历。
            # traverse from left to right along the top row
            for i in range(left, right + 1):
                result.append(matrix[top][i])
            top += 1 # move the top boundary down

            # traverse from top to bottom along the right column
            for i in range(top, bottom + 1):
                result.append(matrix[i][right])
            right -= 1 # move the right boundary left

            # traverse from right to left along the bottom row
            if top <= bottom: \ 为了处理不对称的情况，避免遍历已经不在范围内的行或列，导致重复添加元素或访问超出矩阵范围的元素
                for i in range(right, left - 1, -1):
                    result.append(matrix[bottom][i])
                bottom -= 1

            # traverse from bottom to top along the left column
            if left <= right:
                for i in range(bottom, top - 1, -1):
                    result.append(matrix[i][left])
                left += 1

        return result



```
