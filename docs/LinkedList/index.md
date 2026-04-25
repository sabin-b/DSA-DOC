# Linked List vs Array

| Aspect | Linked List | Array |
| --- | --- | --- |
| Structure | Linear data structure | Linear data structure |
| Memory layout | Non-contiguous memory | Contiguous memory |
| Size | Dynamic size, can grow or shrink easily | Typically fixed size in basic implementations, though dynamic arrays can resize |
| Stored data | Each node stores a value and pointer(s) | Stores values directly |
| Accessing an element | Harder because traversal is needed | Easy with index-based access |
| Insertion and deletion | Easier after reaching the target position | More costly because elements may need to shift |
| Memory usage | Uses extra memory for pointer(s) | More memory efficient |

## Quick Summary

- Use a `linked list` when frequent insertion and deletion matter more than fast random access.
- Use an `array` when fast indexing and memory efficiency matter more.
