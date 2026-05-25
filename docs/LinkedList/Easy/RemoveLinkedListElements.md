# Remove Linked List Elements

[Problem Link](https://leetcode.com/problems/remove-linked-list-elements/){:target="_blank" rel="noopener noreferrer"}

### Description

Given the `head` of a linked list and an integer `val`, remove all the nodes of the linked list that have `Node.val == val`, and return the new head.

!!! example "Test Cases"

    **Example 1:**
    Input: head = [1,2,6,3,4,5,6], val = 6
    Output: [1,2,3,4,5]

    **Example 2:**
    Input: head = [], val = 1
    Output: []

    **Example 3:**
    Input: head = [7,7,7,7], val = 7
    Output: []

### Approach 1: Sentinel Node

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Use a sentinel (dummy) node pointing to head to handle edge cases where the head itself needs removal. Traverse and skip matching nodes.

```typescript
function removeElements(head: ListNode | null, val: number): ListNode | null {
    if (!head) return null;

    let sentinel = new ListNode(0, head);
    let current: ListNode | null = sentinel;

    while (current && current.next) {
        if (current.next.val === val) {
            current.next = current.next.next;
        } else {
            current = current.next;
        }
    }

    return sentinel.next;
}
```

### Approach 2: Recursion

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

Recursively process the tail. If the current node's value matches, skip it by returning `next`; otherwise, link current node to the result of the recursive call and return it.

```typescript
function removeElements(head: ListNode | null, val: number): ListNode | null {
    if (!head) return null;
    head.next = removeElements(head.next, val);
    return head.val === val ? head.next : head;
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
let head1 = createLinkedList([1, 2, 6, 3, 4, 5, 6]);
let result1 = removeElements(head1, 6);
console.log(linkedListToArray(result1)); // [1, 2, 3, 4, 5]

let head2 = createLinkedList([7, 7, 7, 7]);
let result2 = removeElements(head2, 7);
console.log(linkedListToArray(result2)); // []
```
