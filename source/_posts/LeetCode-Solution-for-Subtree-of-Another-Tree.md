---
title: LeetCode-Solution-for-Subtree-of-Another-Tree
date: 2024-12-18 15:25:57
categories: [LeetCode, Algorithm]
tags: [Tree]
---

# Question

Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.

## Explanation

1. Traverse the `root` tree and check if any subtree matches `subRoot`

2. For each node in `root`, use a helper function to determine if the subtree starting at that node is identical to `subRoot`

# Idea

1. Check for Subtree:

1) Recursively check each node of `root` to see if the subtree starting at that node matches `subRoot`
2) If we find a match, return True

2. Check for Identical Trees:

1) Create a helper function to compare two trees
2) The trees are identical if: both nodes have the same value, their left subtrees are identical, their right subtrees are identical.

3. Recursive Traversal:

1) If the current nodes don't match, recursively check the left and right children of `root`

# Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        if not root:
            return False
        # check if the current tree rooted at 'root' is the same as 'subRoot'
        if isSameTree(root, subRoot):
            return True

        # checks whether subRoot is a subtree of root
        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot) \ The or operator returns True if either of the recursive calls returns True.


    def isSameTree(self, s, t):
        # if both nodes are None, they are the same
        if not s and not t:
            return True

        # if one of them are None, or their values don't match, return False
        if not s or not t or s.value != t.value:
            return False
        # check left and right subtree recursively
        return self.isSameTree(s.left, t.left) and self.isSameTree(s.right, t.right)

```
