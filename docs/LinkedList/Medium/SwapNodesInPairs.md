# Swap Nodes in Pairs

[Problem Link](https://leetcode.com/problems/swap-nodes-in-pairs/){:target="_blank" rel="noopener noreferrer"}

### Description

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

!!! example "Test Cases"

    **Example 1:**
    Input: head = [1,2,3,4]
    Output: [2,1,4,3]

    **Example 2:**
    Input: head = []
    Output: []

    **Example 3:**
    Input: head = [1]
    Output: [1]

    **Example 4:**
    Input: head = [1,2,3]
    Output: [2,1,3]

### Approach 1: Iterative with Dummy Node

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Use a dummy node before the head so the first pair can be swapped like any other. Keep `prev` pointing at the node before the current pair, then rewire `prev.next`, `current.next`, and `next.next` to swap the pair. Move `prev` to `current` (the second node of the swapped pair) and continue. Return `dummy.next`, which is the new head — `prev` ends up at the tail of the swapped list.

```typescript
function swapPairs(head: ListNode | null): ListNode | null {
    if (!head || !head.next) return head;

    const dummy = new ListNode(0, head);

    let prev = dummy;
    let current: ListNode | null = head;
    let next: ListNode | null = head.next;

    while (current && next) {
        prev.next = next;
        current.next = next.next;
        next.next = current;

        prev = current;
        current = prev.next ?? null;
        next = current?.next ?? null;
    }

    return dummy.next;
}
```

### Approach 2: Recursive

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

Swap the first pair, then recurse on the rest of the list: `left.next` points to the result of swapping the remaining pairs, and `right.next` points back to `left`, making `right` the new head of this segment. Base case: fewer than two nodes left — return the list unchanged.

```typescript
function swapPairs(head: ListNode | null): ListNode | null {
    if (!head || !head.next) return head;
    let left = head;
    let right = head.next;
    left.next = swapPairs(right.next);
    right.next = left;
    return right;
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

### Example Usage

```typescript
// Helper function to create linked list from array
function createLinkedList(arr: number[]): ListNode | null {
    if (arr.length === 0) return null;
    let head = new ListNode(arr[0]);
    let current = head;
    for (let i = 1; i < arr.length; i++) {
        current.next = new ListNode(arr[i]);
        current = current.next;
    }
    return head;
}

// Helper function to convert linked list to array
function linkedListToArray(head: ListNode | null): number[] {
    const result: number[] = [];
    let current = head;
    while (current) {
        result.push(current.val);
        current = current.next;
    }
    return result;
}

// Test
let head = createLinkedList([1, 2, 3, 4]);
let result = swapPairs(head);
console.log(linkedListToArray(result)); // [2, 1, 4, 3]
```
