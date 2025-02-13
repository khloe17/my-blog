---
title: LeetCode-Solution-for-Reverse-Nodes-in-k-Group
date: 2025-02-01 17:51:47
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

Given the head of a linked list, reverse the nodes of the list k at a time, and return the modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

## Explanation

Example 1:
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]

![Local image](./images/25_1.png "Reverse nodes in k-group explanation")

Example 2:
Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]

For each k elements, reverse the group and continue with next group with k elements. If the group num is less than k, then keep it.

# Idea

1. Initialize pointers:
   dummy: act as a new head before the original head
   `prev_group_end`: keep track of the last node before the current k-group
   `current`: point to the first node of the current k-group after reversal
   `tail`: point to the first node of the current k-group before reversal (it becomes the new "end" of the traversal group)
2. Count the total number of nodes in the list
3. Loop while at least k nodes remain:
   reverse the next k nodes
   connect the previous group's end to the new head
   move prev_group_end forward
4. Return dummy.next, which is the new head

```
We assume we are given the linked list:
1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → NULL
with k = 3, so we will reverse nodes in groups of 3.

Step 1: Reverse First k-Group (1 → 2 → 3)
After the reversal, we get:
3 → 2 → 1   4 → 5 → 6 → 7 → 8 → NULL

`prev` now points to 3 (new head of reversed group).
`tail` (before reversal) was 1, so it now represents the last node of the reversed group.
`current` now points to 4 (first node after the reversed group).
![Local image](./images/25_2.png "Reverse nodes in k-group table")

```

# Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        dummy = ListNode(0)
        dummy.next = head
        prev_group_end = dummy
        current = head

        # count the total number of nodes
        count = 0
        while current:
            count += 1
            current = current.next

        # reset the current pointer to process the first k-group
        current = head

        # loop through the reverse k-groups
        while count >= k:
            prev = None
            tail = current # the tail will be the new end after traversal

            # reverse k nodes
            for _ in range(k):
                temp = current.next
                current.next = prev
                prev = current
                current = temp

            # connect the previous part with the reversed group
            prev_group_end.next = prev # prev is the new head of reversed group
            tail.next = current # connect the reversed group to the remaining nodes

            # move prev_group_end to tail (which is the end of reversed part)
            prev_group_end = tail

            count -= k # reduce count by k since we processed k nodes
        return dummy.next

```
