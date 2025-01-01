---
title: LeetCode-Solution-for-Serialize-and-Deserialize-Binary-Tree
date: 2024-12-17 09:47:01
categories: [LeetCode, Algorithm]
tags: [Tree]
---

# Question

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

Clarification: The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

## Explanation

1. We need to convert this list to a single string for two main reasons:

Storage or Transfer: A string is easier to store in a file or send over a network compared to a list.

Deserialization: When deserializing, it's easier to split a string back into a list of values.

2. How ",".join(result) Works

   The expression: ",".join(result)

Purpose: Joins all elements of the result list into a single string, with each element separated by a comma ,.

input:
result = ['1', '2', 'null', 'null', '3', '4', 'null', 'null', '5', 'null', 'null']
serialized_string = ",".join(result)

output:
"1,2,null,null,3,4,null,null,5,null,null"

3. Why Convert int to str in ",".join(result)?

The join() method in Python works with iterables of strings. It expects each item in the iterable (like a list) to be a string. If any element is not a string (e.g., an integer), Python raises a TypeError.

4. Explanation of nodes = deque(data.split(","))

The split(",") method breaks the string wherever it finds a comma and returns a list of substrings.

data.split(",") converts the serialized string into a list of node values.

deque(...) wraps the list into a deque for efficient processing.

5. Why deque?

A deque allows you to remove elements from the front efficiently using popleft().

Lists are less efficient for this operation because removing the first element of a list requires shifting all the other elements.

# Idea: Preorder Traversal

1. Serialization:

1) Traverse the tree using preorder traversal.
2) Convert each node to a string and append it to a list.
3) Use `"null"` for `None` (i.e., when there's no child).
4) Convert the list of strings into a single string using a delimiter (e.g., commas).

2. Deserialization

1) Split the serialized string by the delimiter to create a list.
2) Rebuild the tree by recursively processing the list using preorder traversal.
3) If an element is `"null"`, return `None` and move to the next element.

# Code

```python
from collections import deque

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        def dfs(node):
            if node is None:
                result.append("null")
            else:
                result.append(str(node.val)) # # Convert the integer to a string
                dfs(node.left)
                dfs(node.right)

        result = []
        dfs(root)
        return ",".join(result)


    def deserialize(self, data):
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        def dfs():
            val = nodes.popleft()
            if val == "null":
                return None
            node = TreeNode(int(val))
            node.left = dfs()
            node.right = dfs()
            return node


        nodes = deque(data.split(","))
        return dfs()


# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```
