---
title: LeetCode-Solution-for-Invert-Binary-Tree
date: 2024-12-14 20:03:51
categories: [LeetCode, Algorithm]
tags: [Tree]
---

# Question

Given the root of a binary tree, invert the tree, and return its root.

## Explanation

Inverting a binary tree means swapping the left and right children of each node recursively.

Example 1:
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]

Example 2:
Input: root = [2,1,3]
Output: [2,3,1]

Example 3:
Input: root = []
Output: []

# Idea

Recursive Approach:

1. Swap the left and right children
2. Recursively invert the left subtree
3. Recursively invert the right subtree

# Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return None

        # swap the left and right children
        root.left, root.right = root.right, root.left

        # recursively invert the left and right tree
        self.invertTree(root.left)
        self.invertTree(root.right)

        return root



```
