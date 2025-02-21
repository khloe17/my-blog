---
title: LeetCode-Solution-for-Find-Median-from-Data-Stream
date: 2025-01-12 17:39:45
categories: [LeetCode, Algorithm]
tags: [Heap]
---

# Question

The median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value, and the median is the mean of the two middle values.

For example, for arr = [2,3,4], the median is 3.
For example, for arr = [2,3], the median is (2 + 3) / 2 = 2.5.
Implement the MedianFinder class:

MedianFinder() initializes the MedianFinder object.
void addNum(int num) adds the integer num from the data stream to the data structure.
double findMedian() returns the median of all elements so far. Answers within 10^(-5) of the actual answer will be accepted.

## Explanation

Input
["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
[[], [1], [2], [], [3], []]
Output
[null, null, null, 1.5, null, 2.0]

Explanation
MedianFinder medianFinder = new MedianFinder();
medianFinder.addNum(1); // arr = [1]
medianFinder.addNum(2); // arr = [1, 2]
medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
medianFinder.addNum(3); // arr[1, 2, 3]
medianFinder.findMedian(); // return 2.0

# Idea

1. Use two heaps:

Store the smaller half of the numbers (`lower_half`) in a max-heap, so the largest number in the smaller half is always accessible at the root

Store the larger half of the numbers (`upper_half`)in a min-heap, so the smallest number in the larger half is always accessible at the root

2. Median calculation:

The median lies at the boundary of the two halves.

If the two heaps are of equal size: The median is the average of the max of `lower_half` and the min of `upper_half`.

If the heaps are unequal: The median is the root of the heap with more elements.

Tips:

1. Heap
   A specialized binary tree-based data structure that satisfies the heap property:
   Max-Heap: The parent node is always greater than or equal to its childeren.
   Min-Heap: The parent node is always less than or equal to its children.

The heap is commonly implemented as a binary tree but stored in array format for efficiency.

2. Python's `heapq` module only supports a min-heap, where the smallest element is at the root. We can use the negative transition to convert a min-heap into a max-heap.

3. `heappop` is part of Python's heapq module and is used to remove and return the smallest element from a heap.

# Code

```python
import heapq

class MedianFinder:

    def __init__(self):
        # max-heap for the lower half (store negative values to simulate a max-heap)
        self.lower_half = []
        # min-heap for the upper half
        self.upper_half = []


    def addNum(self, num: int) -> None:
        # simulate a max-heap in python
        heapq.heappush(self.lower_half, -num)

        # ensure all elements in lower_half are smaller than or equal to all elements in upper_half
        if self.lower_half and self.upper_half and (-self.lower_half[0] > self.upper_half[0]):
            heapq.heappush(self.upper_half, -heapq.heappop(self.lower_half))

        # balance the sizes of the two heaps
        if len(self.lower_half) > len(self.upper_half) + 1:
            heapq.heappush(self.upper_half, -heapq.heappop(self.lower_half))
        elif len(self.upper_half) > len(self.lower_half):
            heapq.heappush(self.lower_half, -heapq.heappop(self.upper_half))

    def findMedian(self) -> float:
        # if the heaps are equal size, return the average of the two middle elements
        if len(self.lower_half) == len(self.upper_half):
            return (-self.lower_half[0] + self.upper_half[0]) / 2.0
        # if the heaps are not equal, return the root of the larger heap
        return self.lower_half[0]




# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```
