# Remove Nth Node From End of List

[Problem Link](https://leetcode.com/problems/remove-nth-node-from-end-of-list/){:target="_blank" rel="noopener noreferrer"}

### Description

Given the head of a linked list, remove the nth node from the end of the list and return its head.

!!! example "Test Cases"

    **Example 1:**
    Input: head = [1,2,3,4,5], n = 2
    Output: [1,2,3,5]

    **Example 2:**
    Input: head = [1], n = 1
    Output: []

    **Example 3:**
    Input: head = [1,2], n = 1
    Output: [1]

### Approach: Two-Pass with Sentinel

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

We use a sentinel node to handle edge cases (removing the head). First pass finds the length of the list. Second pass traverses to the node just before the target and removes it.

```typescript
function removeNthFromEnd(head: ListNode | null, n: number): ListNode | null {
    if (!head) return null;
    const sentinel = new ListNode(0, head);

    let length = 0;
    while (head) {
        head = head.next;
        length++;
    }

    let prevNodePos = length - n;
    let prevNode = sentinel;
    for (let i = 0; i < prevNodePos; i++) {
        if (prevNode.next) prevNode = prevNode.next;
    }

    if (prevNode && prevNode.next) prevNode.next = prevNode.next?.next;

    return sentinel.next;
}
```

### Approach 2: One-Pass with Two Pointers

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Uses two pointers with a gap of `n`. Move `fast` ahead by `n` steps, then advance both until `fast` reaches the end — `slow` ends up right before the target node, so we can remove it in one pass.

```typescript
function removeNthFromEnd(head: ListNode | null, n: number): ListNode | null {
    const sentinel = new ListNode(0, head);
    let slow = sentinel;
    let fast = sentinel;

    for (let i = 0; i < n; i++) fast = fast.next!;

    while (fast.next) {
        slow = slow.next!;
        fast = fast.next;
    }

    slow.next = slow.next?.next ?? null;
    return sentinel.next;
}
```

### Definition for singly-linked list:

```typescript
class ListNode {
    val: number;
    next: ListNode | null;
    constructor(val?: number, next?: ListNode | null) {
        this.val = (val===undefined ? 0 : val);
        this.next = (next===undefined ? null : next);
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
let head = createLinkedList([1, 2, 3, 4, 5]);
let result = removeNthFromEnd(head, 2);
console.log(linkedListToArray(result)); // [1, 2, 3, 5]
```
