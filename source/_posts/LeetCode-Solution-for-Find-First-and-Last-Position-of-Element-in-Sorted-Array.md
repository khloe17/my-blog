---
title: LeetCode-Solution-for-Find-First-and-Last-Position-of-Element-in-Sorted-Array
date: 2025-02-18 14:27:34
categories: [LeetCode, Algorithm]
tags: [Array]
---

# Question

Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

You must write an algorithm with O(log n) runtime complexity.

## Explanation

Example 1:
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]

Example 2:
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]

Example 3:
Input: nums = [], target = 0
Output: [-1,-1]

# Idea: Binary search

1. Use binary search to find the first occurrence of target:
   If nums[mid] == target, move right pointer left (right = mid - 1) to find the first occurrence.
2. Use binary search to find the last occurrence of target:
   If nums[mid] == target, move left pointer right (left = mid + 1) to find the last occurrence.

Tips:
Why Move right Pointer Left When Finding the First Occurrence?

In binary search, when we find `nums[mid] == target`, we still need to check if there is an earlier occurrence.

To do this:

Move right left (right = mid - 1), instead of stopping immediately or moving left.
This ensures that we continue searching for the leftmost occurrence of target.

# Code

```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        # helper function to find the first occurrence
        def find_first(nums, target):
            left, right = 0, len(nums) - 1
            first_pos = -1

            while left <= right:
                mid = (left + right) // 2 # mid should be updated inside the loop in every iteration
                if nums[mid] == target:
                    first_pos = mid # update the first position
                    right = mid - 1 # keep searching on the left side
                elif nums[mid] < target:
                    left = mid + 1
                else:
                    right = mid - 1

            return first_pos

        # helper function to find the first occurrence
        def find_last(nums, target):
            left, right = 0, len(nums) - 1
            last_pos = -1

            while left <= right:
                mid = (left + right) // 2
                if nums[mid] == target:
                    last_pos = mid # update last position
                    left = mid + 1 # keep searching on the right side
                elif nums[mid] < target:
                    left = mid + 1
                else:
                    right = mid - 1

            return last_pos

        first = find_first(nums, target)
        last = find_last(nums, target)

        return [first, last]


```
