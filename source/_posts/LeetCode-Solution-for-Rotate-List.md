---
title: LeetCode-Solution-for-Rotate-List
date: 2025-02-13 20:59:30
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

Given the head of a linked list, rotate the list to the right by k places.

## Explanation

Example 1:
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]

Example 2:
Input: head = [0,1,2], k = 4
Output: [2,0,1]

# Idea: Convert to circular linked list

1. Find the length of the list.
2. If k >= n, compute `k % n` to avoid unnecessary rotations.
3. Make the list circular by linking the tail to the head.
4. Find the new tail (`n - k - 1`).
5. Break the cycle at the correct position.

Tips: Why is `n - k - 1` the New Tail?
The new tail is located at index n - k - 1 because it helps us correctly determine where to "cut" the circular linked list so that the last k elements move to the front.

# Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        if not head or not head.next or k == 0:
            return head # edge case: empty list, single node or no rotation needed

        # find the length of the linked list
        length = 1
        tail = head
        while tail.next:
            tail = tail.next
            length += 1

        # compute effective k
        k = k % length
        if k == 0:
            return head # no rotation needed

        # make the list circular
        tail.next = head # connect tail to head to form a circular linked list

        # find the new tail
        new_tail = head
        for _ in range(length - k - 1):
            new_tail = new_tail.next

        # break the cycle and set the new head
        new_head = new_tail.next
        new_tail.next = None # break the cycle

        return new_head

```
