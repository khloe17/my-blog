---
title: LeetCode-Solution-for-Remove-Duplicates-from-Sorted-List
date: 2025-02-06 21:51:31
categories: [LeetCode, Algorithm]
tags: Linked List
---

# Question

Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

## Explanation

Input: head = [1,1,2,3,3]
Output: [1,2,3]

![Local image](./images/83_1.png "Linked list cycle explanation 2")

# Idea

Tips:

1. Mistake: Not Checking If current is None
   If current becomes None at any point, trying to access current.next will cause an AttributeError (NoneType object has no attribute 'next').

2. Mistake: else: current = current.next (Stop early, causing infinite loop)
   Why Is else Necessary?
   Without else, if current.val == current.next.val, we would only delete duplicates but never advance current, potentially causing an infinite loop.

# Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:

```
