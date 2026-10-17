# Rotate List

[Problem Link](https://leetcode.com/problems/rotate-list/){:target="_blank" rel="noopener noreferrer"}

### Description

Given the `head` of a linked list, rotate the list to the right by `k` places.

!!! example "Test Cases"

    **Example 1:**
    Input: head = [1,2,3,4,5], k = 2
    Output: [4,5,1,2,3]

    **Example 2:**
    Input: head = [0,1,2], k = 4
    Output: [2,0,1]

### Approach: Two Pointers with Length and Modulo

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

First traverse the list to find its length `len`. Rotating by `k` where `k >= len` is the same as rotating by `k % len`, so reduce `k` with the modulo. Then start a fast pointer `f` that is `k % len` steps ahead of a slow pointer `s`, and move both until `f` reaches the tail. At that point `s` is the new tail: link the old tail to the head, break the list after `s`, and return `s.next` as the new head.

```typescript
function rotateRight(head: ListNode | null, k: number): ListNode | null {
    if (!head || !head.next) return head;
    let len = 1;
    let curr = head;

    while (curr.next) {
        len++;
        curr = curr.next;
    }

    let n = Math.floor(k % len);
    let s = head;
    let f = head;

    for (let i = 0; i < n; i++) {
        f = f.next;
    }

    while (f.next) {
        f = f.next;
        s = s.next;
    }

    f.next = head;
    let newhead = s.next;
    s.next = null;

    return newhead;
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
let head = createLinkedList([1, 2, 3, 4, 5]);
let result = rotateRight(head, 2);
console.log(linkedListToArray(result)); // [4, 5, 1, 2, 3]
```
