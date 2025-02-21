---
title: LeetCode-Solution-for-Partition-List
date: 2025-01-23 20:09:22
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

Given the head of a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

## Explanation

Example 1:
![Local image](./images/86_1.png "Question example")

Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]

Example 2:
Input: head = [2,1], x = 2
Output: [1,2]

# Idea

1. Split the original list into two smaller lists: one with elements less than `x`, and the other with elements greater than or equal to `x`
2. Traverse the original linked list: If the current node's value is less than `x`, append it to the "less" list. Otherwise, append it to the "greater" list.
3. Connect these two lists together to achieve the desired result. Ensure the "greater" list ends with `null` to avoid cycles.

# Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        # dummy nodes for the two partitions
        less_head = ListNode(0)
        greater_head = ListNode(0)

        # pointers for the current nodes in the two partitions
        less = less_head
        greater = greater_head

        # traverse the original linked list
        while head:
            if head.val < x:
                less.next = head
                less = less.next
            else:
                greater.next = head
                greater = greater.next

            head = head.next # # Move the head pointer forward to avoid infinite loop
        # end the greater list
        greater.next = None
        # connect the two partitions
        less.next = greater_head.next

        # return the head of the modified list
        return less_head.next



```
