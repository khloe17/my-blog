---
title: LeetCode-Solution-for-Binary-Tree-Level-Order-Traversal
date: 2024-12-16 23:02:48
categories: [LeetCode, Algorithm]
tags: [Tree]
---

# Question

Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

## Explanation

Example 1:
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]

Example 2:
Input: root = [1]
Output: [[1]]

Example 3:
Input: root = []
Output: []

# Idea: BFS (Queue Data Structure)

Breadth-First Search (BFS) is suitable for level-order traversal because it explores each level of the tree before moving on to the next level.

1. Start with the root node and add it to a queue
2. Process nodes level by level (While the queue is not empty):
   1. at each level, get the number of nodes currently in the queue (`level_size`)
   2. for each node in this level: dequeue the node (remove it from the queue); add its value to the current level list (record its value); enqueue the left and right children if they are not null (add its children to the queue)
3. Repeat this process until all nodes are processed

# Code

```python
from collections import deque

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        # result to store level order traversal
        result = []

        # edge case: if the tree is empty
        if not root:
            return result

        # Initialize queue for BFS
        queue = deque([root])

        while queue:
            # list to store nodes at the current level
            level = []
            # number of nodes at the current level
            level_size = len(queue)

            for _ in range(level_size):
                # pop the front node of the queue
                current = queue.popleft()
                # add the node's value to the level list
                level.append(current.val)
                # add left child if it exists
                if current.left:
                    queue.append(current.left)
                # add right child if it exists
                if current.right:
                    queue.append(current.right)

            result.append(level)

        return result



```
