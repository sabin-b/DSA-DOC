# Middle of the Linked List

[Problem Link](https://leetcode.com/problems/middle-of-the-linked-list/){:target="_blank" rel="noopener noreferrer"}

### Description

Given the head of a singly linked list, return the middle node of the linked list.

If there are two middle nodes, return the second middle node.

!!! example "Test Cases"

    **Example 1:**
    Input: head = [1,2,3,4,5]
    Output: [3,4,5]

    **Example 2:**
    Input: head = [1,2,3,4,5,6]
    Output: [4,5,6]

### Approach: Slow and Fast Pointer

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

We use two pointers:

- `slow` moves one step at a time.
- `fast` moves two steps at a time.

When `fast` reaches the end of the list, `slow` will be at the middle. For even-length lists, this naturally lands on the second middle node.

```typescript
function middleNode(head: ListNode | null): ListNode | null {
    let slow = head;
    let fast = head;
    while (fast && fast.next) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
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
let head1 = createLinkedList([1, 2, 3, 4, 5]);
let head2 = createLinkedList([1, 2, 3, 4, 5, 6]);

console.log(linkedListToArray(middleNode(head1))); // [3, 4, 5]
console.log(linkedListToArray(middleNode(head2))); // [4, 5, 6]
```
