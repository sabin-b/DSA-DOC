# Intersection of Two Linked Lists

[Problem Link](https://leetcode.com/problems/intersection-of-two-linked-lists/){:target="_blank" rel="noopener noreferrer"}

### Description

Given the heads of two singly linked lists `headA` and `headB`, return the node at which the two lists intersect. If the two linked lists have no intersection, return `null`.

!!! example "Test Cases"

    **Example 1:**
    Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
    Output: Intersected at '8'

    **Example 2:**
    Input: intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
    Output: Intersected at '2'

    **Example 3:**
    Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
    Output: null

### Approach 1: HashSet

- **Time Complexity:** O(m + n)
- **Space Complexity:** O(m + n)

Traverse the first list, storing each node in a Set. Then traverse the second list — the first node found in the set is the intersection.

```typescript
function getIntersectionNode(
  headA: ListNode | null,
  headB: ListNode | null,
): ListNode | null {
  const nodes = new Set<ListNode>();
  let current = headA;
  while (current) {
    nodes.add(current);
    current = current.next;
  }

  current = headB;
  while (current) {
    if (nodes.has(current)) {
      return current;
    }
    current = current.next;
  }
  return null;
}
```

### Approach 2: Two Pointers

- **Time Complexity:** O(m + n)
- **Space Complexity:** O(1)

Two pointers `a` and `b` start at heads. When a pointer reaches its tail, redirect it to the other list's head. They meet at the intersection after at most m + n steps.

```typescript
function getIntersectionNode(
  headA: ListNode | null,
  headB: ListNode | null,
): ListNode | null {
  if (!headA || !headB) return null;
  let a: ListNode | null = headA;
  let b: ListNode | null = headB;
  while (a !== b) {
    a = a ? a.next : headB;
    b = b ? b.next : headA;
  }
  return a;
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

// Helper to build intersecting lists
function buildIntersectingLists(
    commonVals: number[],
    listAVals: number[],
    listBVals: number[],
): { headA: ListNode | null; headB: ListNode | null } {
    let commonHead: ListNode | null = null;
    if (commonVals.length > 0) {
        commonHead = createLinkedList(commonVals);
    }

    let headA = createLinkedList(listAVals);
    let headB = createLinkedList(listBVals);

    if (headA) {
        let cur = headA;
        while (cur.next) cur = cur.next;
        cur.next = commonHead;
    } else {
        headA = commonHead;
    }

    if (headB) {
        let cur = headB;
        while (cur.next) cur = cur.next;
        cur.next = commonHead;
    } else {
        headB = commonHead;
    }

    return { headA, headB };
}

// Test
let { headA, headB } = buildIntersectingLists([8, 4, 5], [4, 1], [5, 6, 1]);
let intersection = getIntersectionNode(headA, headB);
console.log(intersection ? intersection.val : null); // 8
```
