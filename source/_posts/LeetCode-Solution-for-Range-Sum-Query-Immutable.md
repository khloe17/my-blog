---
title: LeetCode-Solution-for-Range-Sum-Query-(Immutable)
date: 2025-02-21 14:50:09
categories: [LeetCode, Algorithm]
tags: [Array]
---

# Question

Given an integer array nums, handle multiple queries of the following type:

Calculate the sum of the elements of nums between indices left and right inclusive where left <= right.
Implement the NumArray class:

NumArray(int[] nums) Initializes the object with the integer array nums.

- int sumRange(int left, int right) Returns the sum of the
- elements of nums between indices left and right inclusive (i.e. nums[left] + nums[left + 1] + ... + nums[right]).

## Explanation

Input
["NumArray", "sumRange", "sumRange", "sumRange"]
[[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]
Output
[null, 1, -1, -3]

Explanation
NumArray numArray = new NumArray([-2, 0, 3, -5, 2, -1]);
numArray.sumRange(0, 2); // return (-2) + 0 + 3 = 1
numArray.sumRange(2, 5); // return 3 + (-5) + 2 + (-1) = -1
numArray.sumRange(0, 5); // return (-2) + 0 + 3 + (-5) + 2 + (-1) = -3

# Idea

Brute force

1. Iterate through the given range and sum up the elements

Prefix sum

1. To compute sumRange(left, right), we use:
   `sumRange(left, right) = sumRange(left, right)=prefixSum[right+1]−prefixSum[left]` which avoids redundant calculations.

e.g. nums = [-2, 0, 3, -5, 2, -1]. We compute the prefix sum array:
![Local image ](./images/303_1.png "Prefix sum calculation example")

Tips:

1. Understand for `self`

In Python, self refers to the instance of the class. It is used to access instance variables and methods inside a class.

When Should You Use self?

1. Accessing Instance Variables

- You need self to refer to variables that belong to a particular instance of the class.

2. Calling Other Methods in the Class

- If you need to call another method within the same class, use self.method_name().

3. Storing Instance-Specific Data

- When you want each object (instance) of the class to have unique data, you store it in self.

# Code

```python
class NumArray:

    def __init__(self, nums: List[int]):
        self.nums = nums # store the given array

    def sumRange(self, left: int, right: int) -> int:
        return sum(self.nums[left:right+1])


# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(left,right)
```

```python
class NumArray:

    def __init__(self, nums: List[int]):
        self.prefixSum = [0] * (len(nums) + 1) # define the prefix sum array
        for i in range(len(nums)):
            self.prefixSum[i + 1] = self.prefixSum[i] + nums[i] # compute prefix sum

    def sumRange(self, left: int, right: int) -> int:
        return self.prefixSum[right + 1] - self.prefix[left]

```
