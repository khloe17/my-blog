---
title: LeetCode-Solution-for-Linked-List-Cycle II
date: 2025-01-22 14:31:03
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to (0-indexed). It is -1 if there is no cycle. Note that pos is not passed as a parameter.

Do not modify the linked list.

## Explanation

Return the start position of the cycle if the cycle exists.

# Idea: Two pointers

1. Check if a cycle exists (slow move one step forward, fast move two steps forward)
2. Finding the Start of the Cycle:
   After detecting the cycle, initialize one pointer to the head of the list, while keeping the other pointer at the meeting point.
   Move both pointers one step at a time until they meet again. The meeting point is the start of the cycle.

When pointers meet, the `slow` pointer has taken `k` steps while the `fast` pointer must have taken `2k` steps.

![Local image ](./images/142_1.png "Linked list cycle explanation 1")

The `fast` pinter has taken `k` more steps than the `slow` pointer, which means these extra `k` steps are the laps the `fast` pointer has completed within the cycle. Therefore `k` is a multiple of the cycle's length.

Assuming the distance from the meeting point to the start of the cycle is `m`, the distance from the head node head to the start of the cycle would be `k - m`. This means moving forward `k - m` steps from head will reach the start of the cycle.

Interestingly, if you move `k - m` steps from the meeting point, you will also reach the start of the cycle. Referring to the fast pointer in the diagram, taking `k` steps from the meeting point returns to the meeting point itself, so `k - m` steps will definitely reach the start of the cycle:

![Local image](./images/142_2.png "Linked list cycle explanation 2")

# Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:

        slow, fast = head, head

        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

            if slow == fast:
                break

        if not fast or not fast.next:
            return None # no cycle

        # find the start of the cycle
        pointer1 = head
        pointer2 = slow
        while pointer1 != pointer2:
            pointer1 = pointer1.next
            pointer2 = pointer2.next

        return pointer1
```
