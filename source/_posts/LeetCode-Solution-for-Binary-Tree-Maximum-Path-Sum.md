---
title: LeetCode-Solution-for-Binary-Tree-Maximum-Path-Sum
date: 2024-12-14 20:32:59
categories: [LeetCode, Algorithm]
tags: [Tree]
---

# Question

A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the root of a binary tree, return the maximum path sum of any non-empty path.

## Explanation

Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.

Input: root = [-10,9,20,null,null,15,7]
Output: 42
Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.

# Idea: DFS

1. We calculate the maximum path sum for the left and right subtree
2. We then consider the current node's contribution:
   include the left subtree
   include the right subtree
   include both left and right subtree
3. We'll track global maximum across all nodes as we traverse the tree.

Key Considerations:

1. If the left or right subtree's contribution is negative, we ignore it (e.g. treat it as zero)
2. Why Not Declare max_sum Inside dfs:
   Scope Limitation:
   Each call to dfs would create a new instance of max_sum because it's a local variable. This means that the state of max_sum wouldn't be shared across recursive calls, and we wouldn’t be able to track the maximum path sum across the entire tree.
   Lack of Persistence:
   When dfs completes, the local max_sum would be discarded, and the information about the maximum path sum found in one subtree would be lost.
   Incorrect Result:
   Since each dfs call would have its own max_sum, we'd only track the maximum path sum for that specific call, not for the entire tree.

# Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        # global variable to track the maximum path sum
        max_sum = float('-inf')

        def dfs(node):
            nonlocal max_sum

            # if the tree is empty or if the recursive call encounters a None child node
            if not node:
                return 0

            # compute the maximum path sum for the left and right subtree
            left_gain = max(dfs(node.left), 0) # ignore negative path
            right_gain = max(dfs(node.right), 0) # ignore negative path

            # path sum through the current node (including both left and right subtrees)
            current_path_sum = node.val + left_gain + right_gain

            # update the global maximum path sum if the current path sum is greater
            max_sum = max(max_sum, current_path_sum) # explore through left and right combination /\

            # return the maximum gain if we continue the path through the current node
            return node.val + max(left_gain, right_gain) # explore up /

        dfs(root)
        return max_sum

```
