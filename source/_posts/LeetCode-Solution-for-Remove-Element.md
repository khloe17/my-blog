---
title: LeetCode-Solution-for-Remove-Element
date: 2025-01-19 17:07:21
categories: [LeetCode, Algorithm]
tags: Array
---

# Question

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.

Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
Return k.

## Explanation

Example 1:
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).

Example 2:
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
Note that the five elements can be returned in any order.
It does not matter what you leave beyond the returned k (hence they are underscores).

# Idea: Two pointers

1. Use a two-pointer approach:
   The `slow` pointer tracks the position where the next non-val element should be replaced
   The `fast` pointer traverses the array to find non-val elements
2. Iterate through the array with the `fast` pointer:
   If nums[fast] != val, copy nums[fast] to nums[slow], and increment the position of `slow`
3. After the loop ends, all non-val elements will be in the first k positions of the array, where k = `slow`

Tips:

Using slow:
In some algorithms (like 27. Remove Element), slow directly represents the number of valid elements.
This is because slow always points to the position just after the last valid element.
When the loop ends, slow already equals the length of the valid part of the array. No need to add 1.

Using slow + 1:
In other algorithms (like 26. Remove Duplicates from Sorted Array), slow points to the last valid element, not the length.
Therefore, to calculate the total number of valid elements, you must add 1 to account for the first valid element at index 0.

# Code

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        if not array:
            return 0

        slow = 0
        for fast in range(len(nums)):
            if nums[fast] != val:
                # copy the element to the slow pointer's position
                nums[slow] = nums[fast]
                slow += 1

        return slow
```
