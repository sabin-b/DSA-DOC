# Add Two Numbers

[Problem Link](https://leetcode.com/problems/add-two-numbers/){:target="_blank" rel="noopener noreferrer"}

### Description

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list. You may assume the two numbers do not contain any leading zero, except the number 0 itself.

!!! example "Test Cases"

    **Example 1:**
    Input: l1 = [2,4,3], l2 = [5,6,4]
    Output: [7,0,8]
    Explanation: 342 + 465 = 807.

    **Example 2:**
    Input: l1 = [0], l2 = [0]
    Output: [0]

    **Example 3:**
    Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
    Output: [8,9,9,9,0,0,0,1]

### Approach: Iterative with Carry

- **Time Complexity:** O(max(m, n))
- **Space Complexity:** O(max(m, n))

Traverse both linked lists simultaneously, summing corresponding digits along with any carry from the previous addition. Create a new node for each digit of the result. If one list is shorter, treat missing digits as 0. If there's a carry after both lists are exhausted, append one final node.

```typescript
function addTwoNumbers(l1: ListNode | null, l2: ListNode | null): ListNode | null {
    let add = new ListNode();
    let addHead = add;
    let carry = 0;

    while (l1 || l2 || carry) {
        let sum = (l1 ? l1.val : 0) + (l2 ? l2.val : 0) + carry;
        carry = Math.floor(sum / 10);
        let digits = sum % 10;
        add.next = new ListNode(digits);
        add = add.next;
        l1 = l1 && l1.next;
        l2 = l2 && l2.next;
    }

    return addHead.next
};
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
let l1 = createLinkedList([2, 4, 3]);
let l2 = createLinkedList([5, 6, 4]);
let result = addTwoNumbers(l1, l2);
console.log(linkedListToArray(result)); // [7, 0, 8]
```
