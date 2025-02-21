---
title: LeetCode-Solution-for-Word-Search II
date: 2025-01-10 23:35:33
categories: [LeetCode, Algorithm]
tags: [Tries (Prefix Trees), DFS]
---

# Question

Given an m x n board of characters and a list of strings words, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

## Explanation

Given:
A 2D board of characters (e.g., board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]]).
A list of words to find (e.g., words = ["oath","pea","eat","rain"]).

Return:
A list of all words from the input that can be formed on the board.

# Idea

1. Use a Trie (Prefix Tree) to store all words for quick lookup (avoid repeatedly searching for prefixes of words).
2. For each cell in the board: start a DFS traversal. Use the Trie to check if the current path matches any word or prefix. Mark cells as visited to avoid reusing them during a single traversal.
3. If a valid word is found during DFS, add it to the result set.

simple logic: Build the Trie -> Start DFS for each cell -> Use backtracking

# Code

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root

        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]

        node.is_end = True


class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        # build a trie for all the words
        trie = Trie()
        for word in words:
            trie.insert(word)

        root = trie.root
        result = set() # use a set to avoid duplicate words
        rows, cols = len(board), len(board[0])

        def dfs(row, col, node, path):
            # base case: out of bounds or characters not in Trie node
            if row < 0 or col < 0 or row >= rows or col > cols or board[row][col] = "#" or board[row][col] not in node.children:
                return

            char = board[row][col] # represents the current character on the board
            node = node.children[char] # track the current position in the Trie
            path += char

            if node.is_end:
                result.add(path)

            # mark the cell as visited
            board[row][col] = "#" / why not `char` = "#" because char is a local variable and does not affect the board

            # explore all four directions
            for dr, dc in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
                dfs(row + dr, col + dc, node, path)

            # backtracking to restore the board to its original state for other DFS paths
            board[row][col] = char

        # start DFS from every cell in the board
        for r in range(rows):
            for c in range(cols):
                dfs(r, c, root, "")

        return list(result)






```
