---
title: LeetCode-Solution-for-Merge-k-Sorted-Lists
date: 2025-01-23 19:02:02
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

## Explanation

Example 1:
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:

<pre>
[
  1->4->5,
  1->3->4,
  2->6
]
</pre>

merging them into one sorted list:
1->1->2->3->4->4->5->6

Example 2:
Input: lists = []
Output: []

Example 3:
Input: lists = [[]]
Output: []

# Idea: Heap-based (priority queue) method

1. Each of the k sorted linked lists has a head node (the smallest value in each list).
2. We push the head node of each list into the min-heap.
3. The min-heap automatically ensures the smallest node among all the heads is at the top.
4. We repeatedly extract the smallest node from the heap and append it to the result list.
5. After extracting a node, if the extracted node has a next node, we push that next node into the heap.
6. Repeat this process until the heap is empty.

Tips:

1. A Min-Heap is a binary tree where:
   A min-heap is a data structure where the smallest element is always at the root. Operations like inserting an element or extracting the smallest element are efficient, with a time complexity of O(log k), where k is the number of elements in the heap.

2. Detailed explanation:
   Step 1: Initialize the Min-Heap
   Push the head node of each list into the min-heap.
   Each entry in the heap is a tuple (node_value, list_index, node):
   node_value: The value of the node (used for sorting in the heap).
   list_index: An identifier for which list this node belongs to (to handle duplicate values correctly).
   node: The actual node reference.
   Heap after initialization:
   [(1, 0, list1), (1, 1, list2), (2, 2, list3)]
   (Note: The heap organizes itself so the smallest value is always on top.)

   Step 2: Extract the Smallest Node
   Extract the smallest node (value 1 from list1) from the heap.
   Append this node to the result linked list.
   Push the next node of the extracted node (4 from list1) into the heap.
   [(1, 1, list2), (2, 2, list3), (4, 0, list1)]

   Step 3: Repeat the Process
   Extract the smallest node (value 1 from list2) from the heap.
   Append it to the result list.
   Push the next node of the extracted node (3 from list2) into the heap.

   Step 4: Continue Until Heap is Empty

3. Complexity Analysis
   Time Complexity
   Each of the N nodes is processed once (inserted into and extracted from the heap).
   Each heap operation (insert or extract) takes O(logk), where k is the number of lists.
   Total time complexity: O(Nlogk), where N is the total number of nodes across all lists.

   Space Complexity
   The heap stores at most k elements at any time (one for each list).
   Space complexity: O(k).

# Code

```python
import heapq

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        if not lists:
            return None

        # min-heap
        heap = []
        dummy = ListNode()
        current = dummy

        # push the head of each list into the heap
        for i, lst in enumerate(lists):
            if lst:
                heapq.heappush(heap, (lst.val, i, lst)) # tuple (node_value, list_index, node)

        # process the heap
        while heap:
            val, i, node = heapq.heappop(heap) # get the smallest node
            current.next = node
            current = current.next
            if node.next: # push the next node of this list into the heap
                heapq.heappush(heap, (node.next.val, i, node.next))# index i serves as a unique identifier to track which linked list a node belongs to

        return dummy.next





```
