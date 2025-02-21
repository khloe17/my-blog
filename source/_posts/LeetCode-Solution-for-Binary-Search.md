---
title: LeetCode-Solution-for-Binary-Search
date: 2025-02-19 09:15:44
categories: [LeetCode, Algorithm]
tags: [Array]
---

# Question

Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.

You must write an algorithm with O(log n) runtime complexity.

## Explanation

Example 1:
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4

Example 2:
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1

# Idea: Binary search

# Code

```python
from typing import List

class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1

        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return mid  # ✅ Immediately return target index
            elif nums[mid] < target:
                left = mid + 1  # ✅ Move right
            else:
                right = mid - 1  # ✅ Move left

        return -1  # ✅ Target not found


```
