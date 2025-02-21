---
title: LeetCode-Solution-for-Remove-Nth-Node-From-End-of-List
date: 2025-01-22 20:10:33
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

Given the head of a linked list, remove the nth node from the end of the list and return its head.

## Explanation

Example 1:
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]

Example 2:
Input: head = [1], n = 1
Output: []

Example 3:
Input: head = [1,2], n = 1
Output: [1]

# Idea: Two pointers

双指针法的核心在于创建两个间隔为 n 的指针，然后同时移动两个指针，直到其中一个指针到达链表末尾，另一个指针会正好指向要删除节点的前一个节点。

1. Initialize a dummy node: create a dummy node and link it to the head dummy = ListNode(0, head) (创建 dummy 节点并将它直接指向 head，目的是简化删除操作，尤其是在需要删除头节点的情况下, 当 dummy 用作临时节点，不设计删除或者修改链表头节点时可以直接使用 dummy = ListNode())
2. Move the first pointer (将 first 指针向前移动 n+1 步，这样之后共同移动时，指针 first 和 second 之间就有了 n 个节点的距离)
3. Move the first and second pointers together until the first pointer reach the end of the linked list (when first pointer reach the None value, the second pointer points to the node just before the one to be removed.)
4. remove the target node by changing the pointer from second.next to second.next.next (改变节点指向，从而跳过目标节点，将其从链表中删除)

Tips:
Dummy node is used to solve edge cases:

1. n is equal to the length of the list:
   In this case, the head node itself is removed.
2. n=1:
   The last node of the list is removed.
3. The list has only one node:
   After removing the node, the result is an empty list.

如果不使用 dummy node，在处理某些特殊情况下（比如删除链表的头节点）会比较复杂，需要额外的判断逻辑来避免错误。

Dummy Node 的作用

1. 统一操作逻辑： 无论删除的是链表的头节点、中间节点还是尾节点，都可以通过调整 dummy.next 来修改链表头。
2. 避免特殊处理头节点： 如果删除的是头节点，直接通过 dummy.next = head.next 即可，而不需要单独判断。

如果不使用 Dummy Node 的问题

1. 删除头节点需要额外处理：
   如果删除的是头节点（比如 n 等于链表长度），直接通过 head = head.next 修改头节点。
   需要单独判断这种情况，否则 head 无法正确更新。
2. 逻辑复杂性增加：
   在没有 dummy 的情况下，我们必须手动检查删除的是头节点还是其他节点。

Why n+1 Steps:
简化想

1. Dummy Node Adds an Extra Step:
   The dummy node is added at the start of the list to simplify edge cases (like removing the head node).
   Because of this dummy node, both pointers start at the dummy node, and we need one extra step to ensure the second pointer stops just before the node to be deleted.

2. Gap of n Nodes:
   After the first pointer moves n+1 steps ahead, the second pointer will start moving.
   Since the first pointer is n steps ahead of the second pointer, when the first pointer reaches the end (null), the second pointer will point to the node just before the n-th node from the end.

# Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        first = dummy
        second = dummy

        # move the first pointer n+1 step to create a gap of n steps
        for _ in range(n+1):
            first = first.next

        # move both pointers until first pointer reach the end (None)
        while first:
            first = first.next
            second = second.next

        # remove the node by second pointer
        second.next = second.next.next

        return dummy.next



```
