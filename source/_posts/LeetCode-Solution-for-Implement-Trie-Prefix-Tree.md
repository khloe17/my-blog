---
title: LeetCode-Solution-for-Implement-Trie (Prefix Tree)
date: 2025-01-03 08:00:59
categories: [LeetCode, Algorithm]
tags: [Tree]
---

# Question

A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

Trie() Initializes the trie object.
void insert(String word) Inserts the string word into the trie.
boolean search(String word) Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.
boolean startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.

## Explanation

Input
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
Output
[null, null, true, false, true, null, true]

Implementation
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple"); // return True
trie.search("app"); // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app"); // return True

# Idea

```
Root
 └── a
     └── p
         └── p (is_end=True)  # "app" ends here
             └── l
                 └── e (is_end=True)  # "apple" ends here
                 └── y (is_end=True)  # "apply" ends here

```

1. Insert a Word
   When inserting a word, traverse the Trie character by character:
   If a character doesn't exist as a child, create a new node.
   If it exists, move to the next character.
   At the end of the word, mark the last node as is_end = True.

2. Search a Word
   When searching for a word:
   Traverse the Trie character by character.
   If any character doesn't exist, return False.
   At the last character, check if is_end = True.
3. Check a Prefix
   When checking for a prefix:
   Traverse the Trie character by character.
   If any character doesn't exist, return False.
   If you traverse all characters of the prefix successfully, return True.

Notice:
node.children is a dictionary of child nodes.
node.children[char] accesses the specific child node corresponding to the character char.

    children is a dictionary where:
    The keys are characters.
    The values are TrieNode objects (representing child nodes).

# Code

```python

class TrieNode:
    def __init__(self):
        self.children = {} # store child nodes
        self.is_end = False # mark if this node ends a word
class Trie:

    def __init__(self):
        self.root = TrieNode()


    def insert(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                # add a new node if the character doesn't exist
                node.children[char] = TrieNode()
            # move to the next node
            node = node.children[char]
        # mark the end of the word
        node.is_end = True


    def search(self, word: str) -> bool:
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            # move to the next node
            node = node.children[char]
        # check if the last node is the end of a word
        return node.is_end


    def startsWith(self, prefix: str) -> bool:
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            # move to the next node
            node = node.children[char]
        # if all characters are found, the prefix exists
        return True



# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```
