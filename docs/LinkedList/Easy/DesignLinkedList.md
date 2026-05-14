# Design Linked List

[Problem Link](https://leetcode.com/problems/design-linked-list/){:target="_blank" rel="noopener noreferrer"}

### Description

Design your implementation of the linked list. You can choose to use a singly or doubly linked list.

A node in a singly linked list should have two attributes: `val` and `next`.

Implement the `MyLinkedList` class:

- `get(index)` returns the value of the `index`th node in the linked list. If the index is invalid, return `-1`.
- `addAtHead(val)` adds a node of value `val` before the first element of the linked list.
- `addAtTail(val)` appends a node of value `val` as the last element of the linked list.
- `addAtIndex(index, val)` adds a node of value `val` before the `index`th node in the linked list.
- `deleteAtIndex(index)` deletes the `index`th node in the linked list if the index is valid.

!!! example "Test Cases"

    **Example 1:**
    Input:
    ["MyLinkedList", "addAtHead", "addAtTail", "addAtIndex", "get", "deleteAtIndex", "get"]
    [[], [1], [3], [1, 2], [1], [1], [1]]
    Output:
    [null, null, null, null, 2, null, 3]

### Approach: Singly Linked List With Size Tracking

- **Time Complexity:**
  - `get(index)`: O(n)
  - `addAtHead(value)`: O(1)
  - `addAtTail(value)`: O(n)
  - `addAtIndex(index, value)`: O(n)
  - `deleteAtIndex(index)`: O(n)
- **Space Complexity:** O(n)

We maintain two things:

- A `head` pointer to the first node.
- A `size` variable to quickly validate indices.

For insertion or deletion in the middle, we traverse to the node just before the target position and then update pointers.

```typescript
class LinkNode {
    public val: number;
    public next: LinkNode | null;

    constructor(val: number, next?: LinkNode | null) {
        this.val = val;
        this.next = next ?? null;
    }
}

class MyLinkedList {
    public head: LinkNode | null;
    public size: number;

    constructor() {
        this.head = null;
        this.size = 0;
    }

    public get(index: number): number {
        if (index < 0 || index >= this.size) {
            return -1;
        }

        let current = this.head;
        for (let i = 0; i < index; i++) {
            current = current!.next;
        }

        return current!.val;
    }

    public addAtHead(value: number): void {
        this.head = new LinkNode(value, this.head);
        this.size++;
    }

    public addAtTail(value: number): void {
        const newNode = new LinkNode(value);

        if (!this.head) {
            this.head = newNode;
        } else {
            let current = this.head;
            while (current.next) {
                current = current.next;
            }
            current.next = newNode;
        }

        this.size++;
    }

    public addAtIndex(index: number, value: number): void {
        if (index < 0 || index > this.size) {
            return;
        }

        if (index === 0) {
            this.addAtHead(value);
            return;
        }

        if (index === this.size) {
            this.addAtTail(value);
            return;
        }

        let current = this.head;
        for (let i = 0; i < index - 1; i++) {
            current = current!.next;
        }

        current!.next = new LinkNode(value, current!.next);
        this.size++;
    }

    public deleteAtIndex(index: number): void {
        if (index < 0 || index >= this.size) {
            return;
        }

        if (index === 0) {
            this.head = this.head!.next;
            this.size--;
            return;
        }

        let current = this.head;
        for (let i = 0; i < index - 1; i++) {
            current = current!.next;
        }

        current!.next = current!.next!.next;
        this.size--;
    }
}
```

### Example Usage

```typescript
const linkedList = new MyLinkedList();

linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1, 2);

console.log(linkedList.get(1)); // 2

linkedList.deleteAtIndex(1);

console.log(linkedList.get(1)); // 3
console.log(JSON.stringify(linkedList));
```
