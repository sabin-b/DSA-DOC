# Remove Duplicates from Sorted List

[Problem Link](https://leetcode.com/problems/remove-duplicates-from-sorted-list/){:target="_blank" rel="noopener noreferrer"}

### Description

Given the `head` of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

!!! example "Test Cases"

    **Example 1:**
    Input: head = [1,1,2]
    Output: [1,2]

    **Example 2:**
    Input: head = [1,1,2,3,3]
    Output: [1,2,3]

### Approach: Single Pointer

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Traverse the list with a single pointer. While the current node and next node exist, compare their values. If they match, skip the next node; otherwise, advance the pointer.

```typescript
function deleteDuplicates(head: ListNode | null): ListNode | null {
  if (!head) return null;

  let current = head;

  while (current && current.next) {
    if (current.val === current.next.val) {
      current.next = current.next.next;
    } else {
      current = current.next;
    }
  }

  return head;
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
let head1 = createLinkedList([1, 1, 2]);
let result1 = deleteDuplicates(head1);
console.log(linkedListToArray(result1)); // [1, 2]

let head2 = createLinkedList([1, 1, 2, 3, 3]);
let result2 = deleteDuplicates(head2);
console.log(linkedListToArray(result2)); // [1, 2, 3]
```
