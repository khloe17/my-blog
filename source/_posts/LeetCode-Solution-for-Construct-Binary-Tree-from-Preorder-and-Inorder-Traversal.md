---
title: LeetCode-Solution-for-Construct-Binary-Tree-from-Preorder-and-Inorder-Traversal
date: 2024-12-18 17:02:18
categories: [LeetCode, Algorithm]
tags: [Tree]
---

# Question

Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.

## Explanation

1. Given two integer arrays preorder and inorder where:

preorder is the preorder traversal of a binary tree (Root -> Left -> Right).
inorder is the inorder traversal of the same binary tree (Left -> Root -> Right).
Construct and return the binary tree.

e.g.
input: preorder = [3, 9, 20, 15, 7], inorder = [9, 3, 15, 20, 7]

output: [3,9,20,null,null,15,7]

2. In the preorder list: The first element is always the root of the tree or subtree.

In the inorder list: The elements to the left of the root are the nodes of the left subtree. The elements to the right of the root are the nodes of the right subtree.

# Idea

1. Identify the root: the first element in the preorder list.
2. Split the inorder list: find the root position in inorder list. The elements left of the root in inorder belong to the left subtree. The elements right of the root in inorder belong to the right subtree.
3. Recursively construct the left and right subtree.

# Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
      if not preorder or not inorder:
        return None

      # the first element in preorder is root
      root_val = preorder.pop(0)
      root = TreeNode(root_val)

      # find the root in inorder
      root_index = inorder.index(root_val)

      # split inorder into left and right subtree
      inorder_left = inorder[:root_index]
      inorder_right = inorder[root_index + 1 :]


      # recursively build left and right subtree
      root.left = self.buildTree(preorder, inorder_left)
      root.right = self.buildTree(preorder, inorder_right)

      return root

```
