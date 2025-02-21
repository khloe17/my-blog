---
title: LeetCode-Solution-for-Merge-Two-Sorted-Lists
date: 2025-01-22 21:39:04
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

## Explanation

已经给出两个排序的 linked list，现在需要合并这个两个 linked list，并给出返回后已排序的 linked list.

# Idea: Two pointers

1. Initialize a dummy node: serve as the start of new merged list (simplify handling the head of the new list, especially when adding nodes)
2. Use two pointers to traverse lists: at each step, compare the nodes of list1 and list2. Append the node with the smaller value and move the pointer in that list forward.
3. When reach the end of either list1 or list2: append the remaining nodes of the other list to the merged list (both lists are sorted at the start)

# Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        # create a dummy node as the start of the merged list
        dummy = ListNode()
        tail = dummy \ 这里dummy再赋值给tail的一个原因：如果不借助tail作为后续用来移动的指针，dummy的位置会不断向后移动，最后失去对链表开头的引用，导致无法返回完整的链表

        while list1 and list2:
            # compare the value of list1 and list2
            if list1.val < list2.val:
                tail.next = list1
                list1 = list1.next
            else:
                tail.next = list2
                list2 = list2.next
            # move the tail pointer forward in the merged list
            tail = tail.next

        # attach any remaining modes from list1 or list2
        if list1:
            tail.next = list1
        if list2:
            tail.next = list2

        # return the head of the merged list, which is next to the dummy node
        return dummy.next


```
