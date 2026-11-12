# Delete Node in a Linked List

[Problem Link](https://leetcode.com/problems/delete-node-in-a-linked-list/){:target="_blank" rel="noopener noreferrer"}

### Description

There is a singly-linked list `head`, and we want to delete a node `node` in it.

You are given the node to be deleted, `node`. You will not be given access to the first node of `head`.

All the values of the linked list are unique, and it is guaranteed that the given node `node` is not the last node in the linked list.

Delete the given node. Note that by deleting the node, we do not mean removing it from memory. We mean:

- The value of the given node should not exist in the linked list.
- The number of nodes in the linked list should decrease by one.
- All the values before `node` should be in the same order.
- All the values after `node` should be in the same order.

!!! example "Test Cases"

    **Example 1:**
    Input: head = [4,5,1,9], node = 5
    Output: [4,1,9]
    Explanation: You are given the second node with value 5, the linked list should become 4 -> 1 -> 9 after calling your function.

    **Example 2:**
    Input: head = [4,5,1,9], node = 1
    Output: [4,5,9]
    Explanation: You are given the third node with value 1, the linked list should become 4 -> 5 -> 9 after calling your function.

### Approach: Copy Next Node and Skip It

- **Time Complexity:** O(1)
- **Space Complexity:** O(1)

Since we only have the target node and not the head, we cannot rewire the previous node. Instead, copy the next node's value into the current node, then bypass the next node by linking `node.next` to `node.next.next`. The node object itself stays in memory, but its value is replaced and the duplicate next node is removed from the list. This relies on the guarantee that `node` is not the tail.

```typescript
function deleteNode(node: ListNode | null): void {
    node.val = node.next.val;
    node.next = node.next.next;
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
let head = createLinkedList([4, 5, 1, 9]);
deleteNode(head!.next);
console.log(linkedListToArray(head)); // [4, 1, 9]
```
