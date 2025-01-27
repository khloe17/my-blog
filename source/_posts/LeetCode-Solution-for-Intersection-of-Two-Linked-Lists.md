---
title: LeetCode-Solution-for-Intersection-of-Two-Linked-Lists
date: 2025-01-22 18:23:57
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return null.

For example, the following two linked lists begin to intersect at node c1:

![Local image](./images/160_1.png "Question example")

The test cases are generated such that there are no cycles anywhere in the entire linked structure.

Note that the linked lists must retain their original structure after the function returns.

Custom Judge:

The inputs to the judge are given as follows (your program is not given these inputs):

intersectVal - The value of the node where the intersection occurs. This is 0 if there is no intersected node.
listA - The first linked list.
listB - The second linked list.
skipA - The number of nodes to skip ahead in listA (starting from the head) to get to the intersected node.
skipB - The number of nodes to skip ahead in listB (starting from the head) to get to the intersected node.
The judge will then create the linked structure based on these inputs and pass the two heads, headA and headB to your program. If you correctly return the intersected node, then your solution will be accepted.

## Explanation

Example 1:
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
Output: Intersected at '8'
Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,6,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.

- Note that the intersected node's value is not 1 because the nodes with value 1 in A and B (2nd node in A and 3rd node in B) are different node references. In other words, they point to two different locations in memory, while the nodes with value 8 in A and B (3rd node in A and 4th node in B) point to the same location in memory.

Example 2:
Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
Output: No intersection
Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.

# Idea

Approach 1: Length Alignment (Native method)

1. Find the lengths of both linked lists, `lenA` and `lenB`
2. Align the starting points by advancing the pointer of the longer list by |lenA - lenB| steps
3. Traverse both lists simultaneously and return the first node where they meet

Time complexity: O(m+n), where m and n are the lengths of `headA` and `headB`.

Approach 2: Two pointers (Optimal)

1. Initially set `pointerA` to the head of `headA` and `pointerB` to the head of `headB`
2. Traverse both lists:
   If `pointerA` reaches the end of its list, redirect it to the head of `headB`
   If `pointerB` reaches the end of its list, redirect it to the head of `headA`
3. If the lists intersect, the pointer will meet at the intersection node.
4. If the lists do not intersect, both pointers will eventually become `null`

![Local image](./images/160_2.png "How to reach the intersecting node by switching lists ")

The problem is solved with a space complexity of O(1) and a time complexity of O(N).

切换是为了平衡两条链表的长度，使得两个指针在第二轮遍历时能够同步。如果链表有交点，最终两个指针会在交点处相遇；如果没有交点，两个指针会同步到达 null。

# Code

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        if not headA or not headB:
            return None

        pointerA, pointerB = headA, headB

        # traverse both lists
        while pointerA != pointerB:
            pointerA = pointerA.next if pointerA else headB
            pointerB = pointerB.next if pointerB else headA

        # if they intersect, pointerA/pointerB is at the intersection node' otherwise, it's None
        return pointerA


```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        if not headA or not headB:
            return None
        # helper function to calculate the length of a list
        def get_length(self, head):
            length = 0

            while head:
                length += 1
                head = head.next

            return length

        # calculate the lengths of both lists
        lenA = get_length(headA)
        lenB = get_length(headB)

        # align the two lists
        while lenA > lenB:
            headA = headA.next
            lenA -= 1
        while lenA < lenB:
            headB = headB.next
            lenB -= 1

        while headA != headB:
            headA = headA.next
            headB = headB.next

        # return the intersection node or None if no intersection
        return headA
```
