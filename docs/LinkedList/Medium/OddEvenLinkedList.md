# Odd Even Linked List

[Problem Link](https://leetcode.com/problems/odd-even-linked-list/){:target="_blank" rel="noopener noreferrer"}

### Description

Given the head of a singly linked list, group all nodes with odd indices together followed by the nodes with even indices, and return the reordered list. The first node is considered **odd**, the second node **even**, and so on. The relative order within both the odd and even groups should remain as in the original input.

!!! example "Test Cases"

    **Example 1:**
    Input: head = [1,2,3,4,5]
    Output: [1,3,5,2,4]

    **Example 2:**
    Input: head = [2,1,3,5,6,4,7]
    Output: [2,3,6,7,1,5,4]

### Approach: Separate and Merge

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Use two pointers: `odd` starts at the head, `even` starts at the second node. Traverse the list, linking odd nodes together and even nodes together. After the loop, connect the end of the odd list to the head of the even list.

```typescript
function oddEvenList(head: ListNode | null): ListNode | null {
    if (!head || !head.next) return head;
    let odd = head;
    let even = head.next;
    let evenHead = even;

    while (even && even.next) {
        odd.next = even.next;
        odd = odd.next;
        even.next = odd.next;
        even = even.next;
    }
    odd.next = evenHead;
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
let head = createLinkedList([1, 2, 3, 4, 5]);
let reordered = oddEvenList(head);
console.log(linkedListToArray(reordered)); // [1, 3, 5, 2, 4]
```
