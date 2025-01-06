---
title: LeetCode-Solution-for-Kth-Smallest-Element-in-a-BST
date: 2025-01-01 16:17:19
categories: [LeetCode, Algorithm]
tags: [Tree]
---

# Question

Given the root of a binary search tree, and an integer k, return the kth smallest value (1-indexed) of all the values of the nodes in the tree.

## Explanation

Example 1:
Input: root = [3,1,4,null,2], k = 1
Output: 1

Example 2:
Input: root = [5,3,6,2,4,null,null,1], k = 3
Output: 3

# Idea

Approach 1 (Recursive In-order Traversal):

1. In-order traversal is a way of visiting the nodes in a binary tree in a specific order:
   Visit the left subtree.
   Visit the root node.
   Visit the right subtree.
2. During the in-order traversal, maintain a counter to keep track of the number of elements visited so far.
3. When the counter equals k, return the current node's value.

Approach 2 (Optimized In-order Traversal (Early Stopping)):
Instead of generating the entire sorted list, we can optimize by stopping the traversal as soon as we find the kth smallest element.

1. Perform the in-order traversal.
2. Use a counter to track how many elements have been visited.
3. When the counter equals k, return the current node's value and stop traversal.

# Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        def in_order_traversal(node):
            # base case: return an empty list for None nodes
            if not node:
                return []

            # traverse left subtree, current node, then right subtree
            return in_order_traversal(node.left) + [node.val] + in_order_traversal(node.right)

        # get all elements in sorted order
        sorted_element = in_order_traversal(root)

        # return the kth element (1-based index)
        return sorted_element[k - 1]

```

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        # Initialize counter and result variable
        count = 0
        result = None

        def in_order(node):
            nonlocal count, result # to modify these variables inside the nested function
            if not node or result is not None: # base case: no node or we've already found the result
                return

            # traverse the left subtree
            in_order(node.left)

            # process the current node
            count += 1
            if count == k:
                result = node.val
                return # stop further traversal if the current node is the kth smallest

            # traverse the right subtree
            in_order(node.right)


        # start the in-order traversal
        in_order(root)
        return result


```
