---
title: Leetcode-Solution-for-Same-Tree
date: 2024-12-14 17:59:54
categories: [LeetCode, Algorithm]
tags: [Tree]
---

# Question

Given the roots of two binary trees p and q, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

## Explanation

Input:
p = [1, 2, 3]
q = [1, 2, 3]

Tree `p`:
1
/ \
2 3

Tree `q`:
1
/ \
2 3

Output: True

Input:
p = [1, 2]
q = [1, null, 2]

Tree `p`:
1
/
2

Tree `q`:
1
\
 2

Output: False

# Idea

Base Cases:

1. If both `p` and `q` are None, the trees are the same -> return True
2. If one of `p` or `q` is None (but not both), the trees differ -> return False
3. If the values at `p` and `q` are different, the trees differ -> return False

Recursive Step:

1. Recursively check if the left subtree of `p` and `q` are the same
2. Recursively check if the right subtree of `p` and `q` are the same
3. The trees are the same if both the left and right subtree checks return True

# Code

```python
from typing import Optional

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right


class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        # Base case: if both nodes are None, they are the same
        if not p and not q:
            return True

        # Base case: if one of them are None or the values are different, they are not the same
        if not p or not q or p.val != q.val: \ p.val != q.value will check the value of current nodes
            return False

        # Recursively check if left and right subtrees
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)

```
