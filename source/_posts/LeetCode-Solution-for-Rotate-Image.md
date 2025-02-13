---
title: LeetCode-Solution-for-Rotate-Image
date: 2025-02-09 14:32:15
categories: [LeetCode, Algorithm]
tags: Array
---

# Question

You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

## Explanation

n x n 的矩阵整体顺时针旋转 90 度，返回旋转后的矩阵

input:
matrix = [
[1, 2, 3],
[4, 5, 6],
[7, 8, 9]
]

output:
matrix = [
[7, 4, 1],
[8, 5, 2],
[9, 6, 3]
]

![Local image](./images/48_1.png "Rotate Image")

# Idea: Transpose + Reverse

1. Transpose the matrix: swap matrix[i][j] with matrix[j][i] for i < j.
2. Reverse each row.

# Code

```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)

        # transpose the matrix
        for i in range(n):
            for j in range(i + 1, n): \ j 从 (i+1) 开始是为了避免出现重复交换的情形
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

        # reverse each row of the matrix
        for i in range(n):
            matrix[i].reverse()
```
