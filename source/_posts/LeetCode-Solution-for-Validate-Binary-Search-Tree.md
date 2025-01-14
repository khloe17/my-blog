---
title: LeetCode-Solution-for-Validate-Binary-Search-Tree
date: 2024-12-21 09:45:12
categories: [LeetCode, Algorithm]
tags: [Tree]
---

# Question

Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

    The left subtree of a node contains only nodes with keys less than the node's key.
    The right subtree of a node contains only nodes with keys greater than the node's key.
    Both the left and right subtrees must also be binary search trees.

## Explanation

Example 1:
Input: root = [2,1,3]
Output: true
2
/ \
1 3

Example 2:
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
5
/ \
1 4
/\
 3 6

# Idea: Recursion with valid range (Min/Max)

1. Traverse the tree using recursion
2. For each node: The value of the node should lie within the range (min_val, max_val).
   For the left child, the `max_val` should be the current node's value.
   For the right child, the `min_val` should be the current node's value.
3. If at any point a node violates the BST property, return False. If all nodes satisfy the conditions, return True.

# Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def helper(node, min_val, max_val):
            # base case: if we reach a null node, it's valid
            if not node:
                return True

            # check if the node value is within the min and max range
            if not (min_val < node.val < max_val):
                return False

            # recursively validate the left and right subtree
            return (helper(node.left, min_val, node.val) and helper(node.right, node.val, max_val))

        return helper(root, float('-inf'), float(inf))

```
