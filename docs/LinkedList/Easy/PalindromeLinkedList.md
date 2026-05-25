# Palindrome Linked List

[Problem Link](https://leetcode.com/problems/palindrome-linked-list/){:target="_blank" rel="noopener noreferrer"}

### Description

Given the head of a singly linked list, return `true` if it is a palindrome or `false` otherwise.

!!! example "Test Cases"

    **Example 1:**
    Input: head = [1,2,2,1]
    Output: true

    **Example 2:**
    Input: head = [1,2]
    Output: false

### Approach: Find Middle + Reverse

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Find the middle using slow/fast pointers, reverse the second half, then compare both halves node by node.

```typescript
function isPalindrome(head: ListNode | null): boolean {
    if (!head || !head.next) {
        return true;
    }

    // find middle node
    let slow: ListNode | null = head;
    let fast: ListNode | null = head;
    while (fast && fast.next) {
        slow = slow?.next || null;
        fast = fast.next.next;
    }

    // reverse second half
    let prev: ListNode | null = null;
    let current: ListNode | null = slow;
    while (current) {
        let next: ListNode | null = current.next;
        current.next = prev;
        prev = current;
        current = next;
    }

    // compare first half and reversed second half
    let first: ListNode | null = head;
    let second: ListNode | null = prev;
    while (second) {
        if (first?.val !== second?.val) {
            return false;
        }
        first = first.next;
        second = second.next;
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
let head1 = createLinkedList([1, 2, 2, 1]);
console.log(isPalindrome(head1)); // true

let head2 = createLinkedList([1, 2]);
console.log(isPalindrome(head2)); // false
```
