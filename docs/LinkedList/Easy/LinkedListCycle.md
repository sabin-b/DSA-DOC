# Linked List Cycle

[Problem Link](https://leetcode.com/problems/linked-list-cycle/){:target="_blank" rel="noopener noreferrer"}

### Description

Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

!!! example "Test Cases"

    **Example 1:**
    Input: head = [3,2,0,-4], pos = 1
    Output: true
    Explanation: There is a cycle connecting the tail node back to the second node.

    **Example 2:**
    Input: head = [1,2], pos = 0
    Output: true

    **Example 3:**
    Input: head = [1], pos = -1
    Output: false

### Approach 1: Hash Set

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

Traverse the list and store each visited node in a `Set`. If a node is seen again, the list contains a cycle.

```typescript
function hasCycle(head: ListNode | null): boolean {
    if (!head) return false;

    const seenNodes = new Set<ListNode>();
    let current = head;

    while (current) {
        if (seenNodes.has(current)) return true;
        seenNodes.add(current);
        current = current.next;
    }

    return false;
}
```

### Approach 2: Floyd's Tortoise and Hare

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Use two pointers. `slow` moves one step at a time, while `fast` moves two steps. If there is a cycle, they will eventually meet.

```typescript
function hasCycle(head: ListNode | null): boolean {
    if (!head) return false;

    let slow = head;
    let fast = head.next;

    while (slow !== fast) {
        if (!fast || !fast.next) return false;
        slow = slow.next;
        fast = fast.next.next;
    }

    return true;
}
```

### Definition for singly-linked list:

```typescript
class ListNode {
    val: number;
    next: ListNode | null;
    constructor(val?: number, next?: ListNode | null) {
        this.val = (val === undefined ? 0 : val);
        this.next = (next === undefined ? null : next);
    }
}
```
