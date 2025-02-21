---
title: LeetCode-Solution-for-Palindrome-Linked-List
date: 2025-01-31 20:15:28
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

Given the head of a singly linked list, return true if it is a
palindrome or false otherwise.

## Explanation

Example 1:
Input: head = [1,2,2,1]
Output: true

Example 2:
Input: head = [1,2]
Output: false

# Idea

Approach 1: Convert to array (Brute Force)

1. Store the linked list values in an array
2. Use two pointers (one from start and one from end to check for palindrome)

Approach 2: Reverse the second half

1. Find the middle of the linked list using the slow-fast pointer approach
2. Reverse the second half of the list
3. Compare the first and second half
4. (Optional) Restore the list to its original form

# Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        values = []
        current = head
        while current:
            values.append(current.val)
            current = current.next

        # two pointer technique to check for palindrome
        left, right = 0, len(values) - 1
        while left < right:
            if values[left] != values[right]:
                return False
            left += 1
            right -= 1

        return True

```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        if not head or not head.next:
            return True  # Empty or single-node lists are palindromes

        # step 1: find the middle
        slow, fast = head, head

        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # step 2: reverse the second half
        prev = None
        while slow:
            next_temp = slow.next # temporarily store the next node before breaking the link
            slow.next = prev # flip the link, making the node point to the previous one
            prev = slow # move prev forward
            slow = next_temp # move slow forward to continue reversing

        # compare first half and reversed second half
        left, right = head, prev # prev is now the head of the reversed half
        while right: # use second half to check
            if left.val != right.val:
                return False
            left = left.next
            right = right.next

        return True


```
