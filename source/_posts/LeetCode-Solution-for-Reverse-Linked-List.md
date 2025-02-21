---
title: LeetCode-Solution-for-Reverse-Linked-List
date: 2025-02-01 17:41:46
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

Given the head of a singly linked list, reverse the list, and return the reversed list.

## Explanation

Example 1:
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

Example 2:
Input: head = [1,2]
Output: [2,1]

# Idea

We maintain three pointers:

1. prev → Keeps track of the reversed part.
2. current → The node we are currently processing.
3. temp → The next node, so we don’t lose the reference.

# Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:

        prev = None
        current = head
        while current:
            temp = current.next # Step 1: Store next node
            current.next = prev # Step 2: Reverse the pointer
            prev = current # Step 3: Move prev forward
            current = temp # Step 4: Move current forward
        return prev # prev is the new head
```
