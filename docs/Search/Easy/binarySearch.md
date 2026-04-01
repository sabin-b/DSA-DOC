# Binary Search

[Problem Link](https://leetcode.com/problems/binary-search/){:target="_blank" rel="noopener noreferrer"}

### Description

Given a sorted array of integers `numbers` in ascending order and a target value `target`, return the index of `target` if it exists in the array. Otherwise, return `-1`.

Binary search works by repeatedly comparing the target with the middle element and discarding half of the remaining search space each time.

!!! example "Test Cases"

    **Example 1:**
    Input: numbers = [-1, 0, 3, 5, 9, 12], target = 9
    Output: 4
    Explanation: The target value 9 is present at index 4.

    **Example 2:**
    Input: numbers = [-1, 0, 3, 5, 9, 12], target = 2
    Output: -1
    Explanation: The target value 2 is not present in the sorted array.

    **Example 3:**
    Input: numbers = [5], target = 5
    Output: 0
    Explanation: With only one element in the array, the target is found immediately.

### Approach 1: Iterative Binary Search

- **Time Complexity:** O(log n) - Each loop removes half of the remaining search space.
- **Space Complexity:** O(1) - Only a few pointer variables are used regardless of input size.

This is the classic binary search approach. We keep two pointers, `leftIndex` and `rightIndex`, and repeatedly check the middle element.

If the middle element matches the target, we return its index. If the target is smaller, we search the left half. If the target is larger, we search the right half.

```typescript
function search(numbers: number[], target: number): number {
  let leftIndex = 0;
  let rightIndex = numbers.length - 1;

  while (rightIndex >= leftIndex) {
    const middle = Math.floor((leftIndex + rightIndex) / 2);

    // Return the index as soon as the target is found.
    if (target === numbers[middle]) return middle;
    else if (target < numbers[middle]) rightIndex = middle - 1;
    else leftIndex = middle + 1;
  }

  return -1;
}

console.log(search([-1, 0, 3, 5, 9, 12], 9)); // 4
console.log(search([-1, 0, 3, 5, 9, 12], 2)); // -1
```

### Approach 2: Recursive Binary Search

- **Time Complexity:** O(log n) - Each recursive call halves the remaining range.
- **Space Complexity:** O(log n) - Recursive calls use stack space for each level.

This approach uses the same idea as the iterative version, but expresses the shrinking search range through recursive function calls.

```typescript
function searchRecursive(numbers: number[], target: number): number {
  function binarySearch(leftIndex: number, rightIndex: number): number {
    // Stop when the search range becomes invalid.
    if (leftIndex > rightIndex) {
      return -1;
    }

    const middle = Math.floor((leftIndex + rightIndex) / 2);

    // Return the middle index when the target is found.
    if (numbers[middle] === target) {
      return middle;
    }

    // Search the left half when the target is smaller.
    if (target < numbers[middle]) {
      return binarySearch(leftIndex, middle - 1);
    }

    // Search the right half when the target is larger.
    return binarySearch(middle + 1, rightIndex);
  }

  return binarySearch(0, numbers.length - 1);
}

console.log(searchRecursive([-1, 0, 3, 5, 9, 12], 9)); // 4
console.log(searchRecursive([-1, 0, 3, 5, 9, 12], 2)); // -1
```
