---
title: LeetCode-Solution-for-Linked-List-Cycle
date: 2025-01-22 14:12:59
categories: [LeetCode, Algorithm]
tags: [Linked List]
---

# Question

Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail’s next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

# Explanation

判断给出的链表是否有环

# Idea: Two pointers

快慢指针：慢指针每次走一步，快指针每次走两步 （如果有环，则快慢指针在某一时刻一定会相遇）

Each time the slow pointer slow moves one step forward, the fast pointer fast moves two steps forward.

If fast can reach the end of the list normally, it indicates there is no cycle in the list. However, if fast eventually meets slow, it means fast is moving in circles within the list, indicating the list contains a cycle.

# Code

```python
def hasCycle(self, head: Optional[ListNode]) -> bool:
    # 初始化快慢指针在链表相同的位置
    slow = head
    fast = head
    # 用于确保快指针 fast 以及它的下一步 fast.next 都存在，这样快指针在循环内每次可以安全地前进两步而不引发错误
    while fast and fast.next: \ fast：在链表中，fast 指针会一次移动两步。我们需要确保 fast 指针还在链表内，即不为 None。fast.next：因为 fast 要前进两步，我们还需要检查 fast.next 是否存在。如果 fast.next 不存在，即 None，说明链表已经到尾部，fast 无法再移动两步。
        slow = slow.next
        fast = fast.next.next

        if slow == fast:
            return True

    return False



```
