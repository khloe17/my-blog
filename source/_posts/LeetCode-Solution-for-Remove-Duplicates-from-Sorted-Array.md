---
title: LeetCode-Solution-for-Remove-Duplicates-from-Sorted-Array
date: 2025-01-19 12:32:39
categories: [LeetCode, Algorithm]
tags: Array
---

# Question

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.

## Explanation

Example 1:
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

Example 2:
Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

# Idea: Two pointers

1. Initialize two pointers:
   `slow` pointer: point to the position in `nums` where the next unique element should be placed
   `fast` pointer: traverse the array to check for new unique elements.
2. Start both pointers at the beginning of the array.
3. As `fast` pointer moves through the array:
   If the element at `fast` is different from the element at `slow`, update the position at `slow + 1` with `nums[fast]` (value update), and move `slow` one step forward.
4. Continue this process until `fast` has traversed the entire array
5. The number of unique element is `slow + 1`

# Code

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if not nums:
            return 0 # edge case: empty array

        # initialize the slow pointer
        slow = 0

        # iterate through the array with the fast pointer
        for fast in range (1, len(nums)):
            if nums[fast] != nums[slow]:
                # found a new unique element, move the slow pointer
                slow += 1
                nums[slow] = nums[fast]

        return slow + 1

```
