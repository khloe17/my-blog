---
title: LeetCode-Solution-for-Top-K-Frequent-Elements
date: 2025-01-12 03:53:07
categories: [LeetCode, Algorithm]
tags: [Bucket Sort]
---

# Question

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

## Explanation

Example 1:
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

Example 2:
Input: nums = [1], k = 1
Output: [1]

# Idea

Approach 1: Using sorting

1. Count frequencies: Use collections.Counter to count the frequency of each element.
2. Sort by frequency: Sort the items by frequency in descending order.
3. Return top K: Slice the first k elements.

Approach 2: Using bucket sort

1. Count frequencies: Use collections.Counter to count the frequency of each element
2. Bucket sort: Create a list of buckets, where the index represents the frequency, and the values are list of elements with that frequency.
3. Extract top K: Traverse the buckets from high to low frequency and collect elements until k elements are found.

tips:

1. Purpose of buckets (list of lists)
   The outer list is used to group numbers by their frequency.
   Each inner list contains all the numbers with the same frequency.

e.g. nums = [1, 1, 1, 2, 2, 3], k = 2

buckets = [[], [], [], []] # Indices correspond to frequencies 0, 1, 2, 3

buckets[3].append(1) # Number 1 has frequency 3
buckets[2].append(2) # Number 2 has frequency 2
buckets[1].append(3) # Number 3 has frequency 1

final buckets:
buckets = [[], [3], [2], [1]]

2. Difference between extend and append

extend:
Adds each element of the iterable (like a list) to the result list.
Merges the contents of the iterable into the list.

e.g.
result = [1]
bucket = [2, 3]
result.extend(bucket) # Adds each element of bucket to result
print(result) # Output: [1, 2, 3]

append:
Adds the entire iterable (e.g., the bucket list) as a single element to the result list.
The result list will now contain a nested list.

e.g.
result = [1]
bucket = [2, 3]
result.append(bucket) # Adds bucket as a single element
print(result) # Output: [1, [2, 3]]

3. Purpose for result[:k]:
   When processing a bucket, multiple elements with the same frequency may be added to result. This can cause result to exceed k elements, even with the len(result) >= k check.

# Code

```python
from collections import Counter

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # count frequencies
        count = Counter(nums) \ e.g. {1: 3, 2: 2, 3: 1}

        # sort items by frequency in descending order
        sorted_items = sorted(count.items(), key=lambdas x: x[1], reverse = True)

        # extract the top k elements
        return [num for num, freq in sorted_items[:k]]



```

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # count frequencies
        count = Counter(nums)

        # bucket sort based on frequency
        max_freq = max(count.values()) # maximum frequency is the largest value of frequency count dictionary
        buckets = [[] for _ in range(max_freq + 1)]
        for num, freq in count.values():
            buckets[freq].append(num)

        # extract top k elements
        results = []
        for freq in range(max_freq, 0, -1):
            results.extend(buckets[freq])
            if len(results) >= k: # performance optimization (reduce unnecessary process for buckets)
                break


        return results[:k]


```
