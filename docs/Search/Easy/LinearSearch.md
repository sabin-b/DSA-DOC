# Linear Search

### Description

Given an array of integers and a target value, return the index of the target if it exists in the array. Otherwise, return -1.

Linear search is the simplest search algorithm that sequentially checks each element until a match is found or the entire array has been traversed.

!!! example "Test Cases"

    **Example 1:**
    Input: arr = [1, 2, 3, 4, 5], target = 3
    Output: 2
    Explanation: The target value 3 is found at index 2 (0-indexed).

    **Example 2:**
    Input: arr = [1, 2, 3, 4, 5], target = 6
    Output: -1
    Explanation: The target value 6 is not present in the array.

### Approach 1: Manual Iteration

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Iterate through each element in the array and check if it matches the target. Return the index when found, otherwise return -1 after the loop completes.

```typescript
function linearSearch(arr: number[], target: number): number {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
      return i;
    }
  }
  return -1;
}

console.log(linearSearch([1, 2, 3, 4, 5], 3)); // Output: 2
console.log(linearSearch([1, 2, 3, 4, 5], 6)); // Output: -1
```

### Approach 2: Using indexOf

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

JavaScript's built-in `indexOf` method provides a cleaner implementation. It returns the first index at which a given element can be found, or -1 if it is not present.

```typescript
function linearSearch2(arr: number[], target: number): number {
  return arr.indexOf(target);
}

console.log(linearSearch2([1, 2, 3, 4, 5], 3)); // Output: 2
console.log(linearSearch2([1, 2, 3, 4, 5], 6)); // Output: -1
```

This file is now ready to be added to your collection. Let me know if you need the `git` commands to commit it.
