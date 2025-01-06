---
title: LeetCode-Solution-for-Design-Add-and-Search-Words-Data-Structure
date: 2025-01-04 17:17:53
tags:
---

# Question

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:

WordDictionary() Initializes the object.
void addWord(word) Adds word to the data structure, it can be matched later.
bool search(word) Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.

## Explanation

Input
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
Output
[null,null,null,null,false,true,true,true]

Implementation
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
wordDictionary.search("b.."); // return True

To solve this problem efficiently, a Trie (Prefix Tree) is the most suitable data structure because it:

Stores words in a way that allows efficient character-by-character traversal.
Handles wildcard searches naturally by exploring all possible branches for `.` (Wildcard Match).

# Idea

# Code

```python
class TrieNode:
    def __init__(self):
        self.children = {} # dictionary to store child nodes
        self.is_end = False # flag to indicate the end of a word


class WordDictionary:

    def __init__(self):
        self.root = TrieNode() # initialize the Trie with a root node

    def addWord(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                # add a new node for the character if it doesn't exist
                node.children[char] = TrieNode()
            # move to the next node
            node = node.children[char]
        # mark the end of the word
        node.is_end = True


    def search(self, word: str) -> bool:
        def dfs(index: int, node: TrieNode) -> bool:
            # base case: reach the end of the word
            if index == len(word):
                return node.is_end

            char = word[index]
            if char == '.':
                # if the character is '.', explore all possible child nodes
                for child in node.children.values():
                    if dfs(index + 1, child): # check each possible branch
                        return True
                return False
            else:
                # if the character is not '.', check if it exists as a child
                if char not in node.children:
                    return False
                # recursively check the next character
                return dfs(index + 1, node.children[char])

        # start DFS from the root
        return dfs(0, self.root)



# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```
