---
title: LeetCode-Solution-for-Move-Zeroes
date: 2025-01-19 17:26:34
categories: [LeetCode, Algorithm]
tags: [Array]
---

# Question

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

## Explanation

Example 1:
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]

Example 2:
Input: nums = [0]
Output: [0]

# Idea: Two pointers

# Code

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        # initialize the slow pointer
        slow = 0
        # move non-zero elements forward
        for fast in range(len(nums)):
            if nums[fast] != 0:
                nums[slow] = nums[fast]
                slow += 1

        # fill remaining positions with zeroes
        for i in range(slow, len(nums)):
            nums[i] = 0


```
