# Reverse Linked List

[Problem Link](https://leetcode.com/problems/reverse-linked-list/){:target="_blank" rel="noopener noreferrer"}

### Description

Given the head of a singly linked list, reverse the list, and return the reversed list.

!!! example "Test Cases"

    **Example 1:**
    Input: head = [1,2,3,4,5]
    Output: [5,4,3,2,1]

    **Example 2:**
    Input: head = [1,2]
    Output: [2,1]

    **Example 3:**
    Input: head = []
    Output: []

### Approach: Iterative

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

We use three pointers: `prev` (initially null), `current` (initially head), and `temp` (to store the next node). We iterate through the list, reversing the links as we go.

```typescript
function reverseList(head: ListNode | null): ListNode | null {
    let prev = null;
    let current = head;
    while (current) {
        let temp = current.next;
        current.next = prev;
        prev = current;
        current = temp;
    }
    return prev;
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
let head = createLinkedList([1,2,3,4,5]);
let reversedHead = reverseList(head);
console.log(linkedListToArray(reversedHead)); // [5,4,3,2,1]
```