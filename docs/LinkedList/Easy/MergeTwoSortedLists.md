# Merge Two Sorted Lists

[Problem Link](https://leetcode.com/problems/merge-two-sorted-lists/){:target="_blank" rel="noopener noreferrer"}

### Description

You are given the heads of two sorted linked lists `list1` and `list2`. Merge the two lists into one **sorted** list. The list should be made by splicing together the nodes of the first two lists. Return the head of the merged linked list.

!!! example "Test Cases"

    **Example 1:**
    Input: list1 = [1,2,4], list2 = [1,3,4]
    Output: [1,1,2,3,4,4]

    **Example 2:**
    Input: list1 = [], list2 = []
    Output: []

    **Example 3:**
    Input: list1 = [], list2 = [0]
    Output: [0]

### Approach: Iterative with Dummy Node

- **Time Complexity:** O(m + n)
- **Space Complexity:** O(1)

Use a dummy node to simplify edge cases. Compare nodes from both lists, attaching the smaller one to the result. Once one list is exhausted, attach the remainder of the other list.

```typescript
function mergeTwoLists(list1: ListNode | null, list2: ListNode | null): ListNode | null {
    const dummy = new ListNode(0);
    let cur = dummy;

    while (list1 !== null && list2 !== null) {
        if (list1.val <= list2.val) {
            cur.next = list1;
            list1 = list1.next;
        } else {
            cur.next = list2;
            list2 = list2.next;
        }
        cur = cur.next;
    }

    cur.next = list1 !== null ? list1 : list2;
    return dummy.next;
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
let list1 = createLinkedList([1, 2, 4]);
let list2 = createLinkedList([1, 3, 4]);
let merged = mergeTwoLists(list1, list2);
console.log(linkedListToArray(merged)); // [1, 1, 2, 3, 4, 4]
```
