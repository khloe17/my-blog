---
title: LeetCode-Solution-for-Reverse-Linked-List II
date: 2025-02-05 15:45:11
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

Given the head of a singly linked list and two integers left and right where left <= right, reverse the nodes of the list from position left to position right, and return the reversed list.

## Explanation

This problem requires us to reverse a sublist of a linked list from position left to right, while keeping the rest of the list unchanged.

Example 1:
Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]

Example 2:
Input: head = [5], left = 1, right = 1
Output: [5]

# Idea

1. Before position `left`, the list remains the same
2. Between `left` and `right`, we reverse the nodes
3. After `right`, the list remains unchanged

Tips:
`prev_left.next` corresponds to the node with value 2 because it was left before the reversal.
example: 1-2-3-4-5
after: 1-4-3-2-5

prev_left.next.next = current: 2-5 node are connected

# Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseBetween(self, head: Optional[ListNode], left: int, right: int) -> Optional[ListNode]:
        if not head or left == right:
            return head # no changes needed

        dummy = ListNode(0)
        dummy.next = head
        prev_left = dummy

        # move prev_left to just before the left position
        for i in range(left - 1):
            prev_left = prev_left.next

        prev = None
        current = prev_left.next # first node in the sublist
        for _ in range(right - left + 1):
            temp = current.next
            current.next = prev
            prev = current
            current = temp

        # reconnect the reversed sublist
        prev_left.next.next = current # connect the last node of the reversed sublist to the rest
        prev_left.next = prev # connect the start of the reversed sublist to the previous part



```
