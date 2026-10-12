# Linked List vs Arrays

Linked List and Arrays are both linear data structures, but they store and manage elements very differently.

## Structure

**Linked List** — nodes connected with pointers, starting from `Head`:

```mermaid
graph LR
  Head --> N1["3 | next"]
  N1 --> N2["4 | next"]
  N2 --> N3["5 | next"]
  N3 --> N4["1 | null"]
```

**Arrays** — values in contiguous boxes with indices `0, 1, 2, 3`:

| 0 | 1 | 2 | 3 |
| --- | --- | --- | --- |
| 3 | 4 | 5 | 1 |

## Differences

| Aspect | Linked List | Arrays |
| --- | --- | --- |
| Structure | Linear | Linear |
| Memory layout | Non-contiguous — nodes can live anywhere in memory | Contiguous — elements sit side by side |
| Size | Dynamic size, changes easily (grow / shrink by allocating nodes) | Fixed size (can be dynamic in dynamic-array implementations, at a resize cost) |
| Stored data | Node = value + pointer(s) | Just value |
| Getting element (fetching) | Hard — traversal from `Head` needed, O(n) | Easy — index-based access, O(1) |
| Insertion / deletion | Easy — relink pointers once the position is reached | Complex — elements may need to shift |
| Memory usage | Extra memory for pointer(s) per node | Memory efficient, no per-element pointer overhead |

## Quick Summary

- Use a `linked list` when frequent insertion and deletion matter more than fast random access.
- Use an `array` when fast indexing (`O(1)` fetch) and memory efficiency matter more.
