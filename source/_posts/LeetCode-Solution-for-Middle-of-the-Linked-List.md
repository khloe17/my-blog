---
title: LeetCode-Solution-for-Middle-of-the-Linked-List
date: 2025-01-26 22:18:15
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

Given the head of a singly linked list, return the middle node of the linked list.

If there are two middle nodes, return the second middle node.

## Explanation

Example 1:
Input: head = [1,2,3,4,5]
Output: [3,4,5]
Explanation: The middle node of the list is node 3.

Example 2:
Input: head = [1,2,3,4,5,6]
Output: [4,5,6]
Explanation: Since the list has two middle nodes with values 3 and 4, we return the second one.

# Idea: Two pointers

1. Use two ponters, `slow` and `fast` to traverse the list.
2. Move the `slow` pointer one step at a time and move the `fast` pointer two steps at a time.
3. When fast reaches the end of the list (or `fast.next` is `None`), `slow` will be at the middle node.
4. Return the `slow` pointer.

# Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:

        slow = head
        fast = head

        while fast and fast.next:
            slow = slow.next # move slow pointer by 1 step
            fast = fast.next.next # move fast pointer by 2 steps

        # while fast reaches the end, slow is at the middle
        return slow


```
